# Docker

## 1. Introduction

This chapter is a condensed walk-through of the official Docker [Getting Started Guide](https://docs.docker.com/get-started/), making use of an example repository [Python-Vscode](https://github.com/Menziess/Python-Vscode) to demonstrate some basic docker commands. Now what's the main difference between a VM and Docker?

![Docker virtualizes just the app and its dependencies.](../.gitbook/assets/image%20%285%29.png)

## 2. Installation

The installation steps may vary between distributions and OS's. Follow the steps to install `docker-ce` from the [official documentation](https://docs.docker.com/install/#supported-platforms).

After that, pull the repository that is used in this tutorial from [https://github.com/Menziess/Python-Vscode](https://github.com/Menziess/Python-Vscode):

```bash
git clone git@github.com:Menziess/Python-Vscode.git
cd Python-Vscode
```

## 3. Run and Deploy

Develop, deploy, and run applications with containers.

1. **Image:** a blueprint for a container
2. **Container:** a unit of software \(instance of an image\) that packages all its dependencies so that it run smoothly and reliably
3. **Swarm:** a cluster of nodes \(running Docker\)
4. **Service:** a collection of containers running the same image
5. **Stack:** multiple services, possibly sharing dependencies, to be scaled and orchestrated together

For example: an application, or a stack, may contain a database service, and a web-app service, described by their respective images, each having three containers \(6 in total\), running distributed on a swarm.

### 2.1 Build Image

Verify that the Dockerfile exists:

```bash
$ ls
Dockerfile        app.py            requirements.txt
```

Build the image from the dockerfile:

```bash
docker build -t menziess/python-vscode:latest .
```

Show the image that has been built:

```bash
$ docker image ls

REPOSITORY             TAG                 IMAGE ID
menziess/python-vscode latest              326387cea398
```

Run the app in detached mode:

```bash
docker run -p 80:80 menziess/python-vscode
```

Show the running containers:

```bash
$ docker container ls
CONTAINER ID        IMAGE                  COMMAND             CREATED
1fa4ab2cf395        menziess/python-vscode "python app.py"     28 seconds ago
```

Stop the running container:

```bash
docker container stop 1fa4ab2cf395
```

Push container to your own dockerhub repository:

```bash
docker login
docker push <dockerhub-username>/python-vscode
```

### 2.2 Scale Service \(Multiple Containers - Single Node\)

Verify that the `docker-compose.yml` file exists:

```bash
$ ls
Dockerfile        app.py            requirements.txt      docker-compose.yml
```

We initialize a swarm \(of one node, our local computer\):

```bash
docker swarm init
```

Then we deploy our service:

```bash
docker stack deploy -c docker-compose.yml getstartedlab
```

And we scale it by increasing the number of replicas in the .yml file, and simply run the previous command again:

```bash
docker stack deploy -c docker-compose.yml getstartedlab
```

We take down the app, and leave the swarm:

```bash
docker stack rm getstartedlab
docker swarm leave --force
```

### 2.3 Distributed Swarm \(Containers Across Cluster - Multiple Nodes\)

Start two VM's using virtualbox and docker-machine:

```bash
docker-machine create --driver virtualbox myvm1
docker-machine create --driver virtualbox myvm2
```

Initialize the first VM as a swarm manager, as we did in 3.2:

```bash
docker-machine ls
docker-machine ssh myvm1 "docker swarm init --advertise-addr <myvm1 ip>"
```

Copy the command that is show in terminal, and ssh into the second VM, then paste the command to add it as a worker to the swarm:

```bash
docker-machine ssh myvm2 "<the command that is shown>"
```

Show all the nodes in the swarm:

```bash
docker-machine ssh myvm1 "docker node ls"
```

Now you can walk through 3.2 again, and deploy the stack, but on the distributed swarm this time. If you do this, run `docker-machine ls` to reveal the VM ip addresses to access the application in the browser.

Finally, we can leave the swarm from within each VM, remove the stack:

```bash
docker-machine ssh myvm2 "docker swarm leave"
docker-machine ssh myvm1 "docker swarm leave --force"

docker stack rm getstartedlab
docker-machine stop myvm1
docker-machine stop myvm2
```

### 2.4 Stack Services \(Adding Database\)

We will expand our `docker-compose.yml` file by adding more services. We will add a docker visualizer and a redis database. The database will require a volume that is stored on the swarm manager called `/data`, let's make that folder and redeploy:

```bash
docker-machine ssh myvm1 "mkdir ./data"
docker stack deploy -c docker-compose.yml getstartedlab
```

Our application should now display the number of visits.

## 4. Containers For Development

It is sometimes useful to develop apps in a docker container to ensure consistency between different developers' environments.

### 4.1 Docker Approach

A container can be run with a shared volume, so that code changes are immediately visible, and the container is deleted after use. Create a docker image with debug enabled by setting the `ENV FLASK_DEBUG` flag to `1`, then run:

```bash
docker run -p 80:80 --rm menziess/python-vscode
```

### 4.2 Traditional Approach

Create a virtual environment with a tool such as 'virtualenv' in the root folder, and run:

```bash
source ./development.sh
```

This will activate the virtual environment and install dev dependencies and command-line tools. Run the flask app:

```bash
flask run
```

## 5. Useful Dockerfiles

{% code-tabs %}
{% code-tabs-item title="Installing java" %}
```bash
ENV JAVA_HOME=/usr/lib/jvm/jdk1.8.0_111/
RUN mkdir -p /usr/share/man/man1 && \
  apt-get update && \
  apt-get -y --no-install-recommends install openjdk-8-jdk-headless
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Installing pipenv dependencies" %}
```bash
WORKDIR /app
COPY Pipfile /app
COPY Pipfile.lock /app
RUN pip install pipenv
RUN pipenv install -d --system --deploy --ignore-pipfile
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Installing pybuilder whl program, running with entry shell script" %}
```bash
WORKDIR /app

COPY Pipfile /app
COPY Pipfile.lock /app

RUN pip3 install pipenv

COPY /target/dist/Pybuilder-1.0.dev0/dist/Pybuilder-1.0.dev0-py3-none-any.whl /app

RUN pipenv install --system
RUN pip3 install /app/Pybuilder-1.0.dev0-py3-none-any.whl

ENTRYPOINT [ "entry" ] # Calls entry script built by pybuilder as entrypoint 
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Installing pip requirements.txt" %}
```bash
# Only copy requirements
COPY requirements.txt /app

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Installing hadoop" %}
```bash
FROM kovarn/python-java

# Set environmental variables
ENV HADOOP_HOME /localhadoop/hadoop-2.9.2
ENV JAVA_HOME=/usr/lib/jvm/jdk1.8.0_111/
ENV PATH ${HADOOP_HOME}/bin:${PATH}

# Downloading hadoop and installing config file
RUN wget http://apache.40b.nl/hadoop/common/hadoop-2.9.2/hadoop-2.9.2.tar.gz &&   tar xzf hadoop-2.9.2.tar.gz && \
  rm -rf hadoop-2.9.2.tar.gz

# Create localhadoop folder
RUN mkdir localhadoop && \
  mv -v /hadoop-2.9.2 /localhadoop/hadoop-2.9.2

# Create config folder
RUN mkdir localhadoop/conf && \
  cp -R ${HADOOP_HOME}/etc/hadoop/* localhadoop/conf && \
  wget https://gist.githubusercontent.com/Menziess/52f1064f3b77b4b0b3655ca270a38b6b/raw/cba6dcd237f89538d5a03c57b27278eb15b6d314/hdfs-site.xml -O localhadoop/conf/hdfs-site.xml

RUN hdfs dfs -mkdir localhdfs
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="Installing pyspark" %}
```bash
FROM python:3.6.7-slim-stretch

WORKDIR /app

COPY Pipfile /app
COPY Pipfile.lock /app
RUN pip install pipenv

RUN pipenv install --system

RUN apt update && \
  mkdir -p /usr/share/man/man1 && \
  apt install -y openjdk-8-jre-headless

ENTRYPOINT ["pyspark"] # Expects pipfile contains pyspark
```
{% endcode-tabs-item %}
{% endcode-tabs %}

