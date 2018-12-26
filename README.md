# Intro

The high demand for Data Engineers 🔢 👨‍🔧 👨‍🔧 may motivate software-savvy people to venture into the world of data. There is so much to learn, so little time. That is why concise summaries and code examples can be a useful mean to ease the strain on human's inherently limited memory.

**Tip:** look up unfamiliar words in the [jargon](jargon.md).

## 1. Intro of the Intro

Data Scientist 👨‍🔧 and Data Scientist 👩‍🔬 are new job titles, where Data Analyst, BI Developer, and Software Engineer are well known titles. 

* **Data Analyst:** has the understanding of intermediate statistics, data mining tools, SQL, and data visualizations.
* **BI Developer:** works closely with stakeholders to design and build reporting dashboards, integrating data from different sources, aggregating data with SQL, but not performing data analysis.
* **Data Scientists:** turns raw data into pure insights using advanced statistics, math, and machine learning, cooperating with Data Engineers as some machine learning techniques require big and fast data.
* **Software Engineer:** designs, writes, and aims to improve quality characteristics of software for computers or other electronic devices.
* **Data Engineers:** a Software Engineer that writes programs to automate data aggregation, [batch](https://www.quora.com/What-are-the-differences-between-batch-processing-and-stream-processing-systems) processing, [streaming](https://www.quora.com/What-are-the-differences-between-batch-processing-and-stream-processing-systems) fast data processing, and helps to deploy and scale machine learning models into production.

So what are companies looking for? They are looking for **professionals**! People with a desire to learn and master new stuff, and then become an authority in their field.

## 2. Love-Hate Relationship 👨‍🔧 💔 👩‍🔬

Data science and data engineering go hand in hand. A Data Engineer may aggregate batches of data overnight, so that the Data Scientist may train a machine learning model with it in a [jupyter notebook](https://jupyter.org/), after which the 👨‍🔧 and 👩‍🔬 sit around the table to extract and refactor the useful bits of the code to forge a contract and automate the process of deploying the model. Let's specify this process:

* **Data Discovery:** automatically discover data needed to train machine learning models.
* **Data Ingestion \(ETL\):** the act of moving \(and transforming\) data - especially unstructured data - from where it is originated, into a system where it can be stored and analyzed such as [Hadoop](technologies/hadoop.md).
* **Data Exploration:** visualizing the relationships of interest within the source data.
* **Data Preprocessing:** encoding categorical variables, imputing missing variables, executing other corrections and augmentations.
* **Feature Engineering:** deciding what features to create and check whether features work for a ML model. 
* **Algorithm Selection:** selecting the most optimal algorithm for a given feature set.
* **Training:** training the ML model \(may sometimes take a long time\)
* **Evaluation:** determine whether the model's accuracy, efficiency is sufficient.
* **Hyperparameter Tuning:** choosing the set of optimal [hyperparameters](https://en.wikipedia.org/wiki/Hyperparameter_%28machine_learning%29) using methods such as:
  * Grid search
  * Random search
  * Bayesian optimization
  * Evolutionary optimization
  * Gradient-based optimization
* **Testing:** writing tests to determine whether functionalities such as cleaning, encoding, test-train splitting, serializing, training, etc still work as intended.
* **Refactoring:** transforming jupyter notebooks / scripts to a sound code project that can handle the data volume and velocity of the production environment.
* **Deployment:** 
  * create a REST API that exposes a model over http
  * dockerizing the project so that it can scale and run in isolation
  * applying continuous integration to automate collaboration
  * apply continuous deployment so that new versions of the project are tested, built and deployed automatically
  * exposing the model to the systems that need it
* **Provisioning:** using Kubernetes or [Docker Swarm](technologies/docker.md#2-2-scale-service-multiple-containers-single-node) to automatically scale up or down the service.

It is understood that 👨‍🔧 are often critical of the code quality and scalability of the piece of code delivered by 👩‍🔬, which in return are unhappily surprised when they have to adjust their code only because the 👨‍🔧 is overly critical, all the while the data provided by the 👨‍🔧 wasn't all that well prepared. But despite the hate, there exists love when they work as a team, and get that model deployed successfully!

## 3. Big Data

Where Data Analysts and BI Developers dealt with Data Warehouses with static structured Terabytes of data, Data Engineers deal with:

* **Volume:** petabytes of data
* **Variety:** structured and unstructured data of any type and format
* **Velocity:** flowing streams of fast data

Organizations grow into [Big Data](https://github.com/onurakpolat/awesome-bigdata#readme) as they become experienced with processing data into valuable information, from left to right:

|  | Exploring | Learning | Doing | Mastering | Teaching |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Phase | Discovery | Developing | Defined | Managed | Optimized |
| Structure | Siloed and hierarchical | Transitioning | Empowered | Self steering | Holocracy |
| Process | Waterfall | Hybrid | Agile | DevOps | BizDevOps |
| People | Individual heroes | Small team | Teams in BU's | Organizational team | Enterprise wide staff trained |
| Decisionmaking | Opinions and experience | Ad hoc report requests | Dashboards | Real time data insights | Automated decision making based on predictive analysis |
| Knowledge | Fragmented legacy DB's | Centralized legacy DB | iOT and Sensors | Data lake | Semantic knowledge store |
| Tooling | Desktop toolings | Legacy centralized | Ad hoc | Data science tools | Data science platform |
| Architecture | Monolith | ESB | Miniservices | Microservices | Self discoverable microservices |
| Infrastructure | Classic data centre | "Lift and shift" | Hybrid | Automated | Infrastructure as code in the cloud |
|  |  |  |  |  |  |

From here on, this gitbook will focus on two sets of skills:

* Architecture, Consulting, Project Management, Collaboration, Mature Decisions
* Technologies, Services

The first set of skills is something that professionals should strive to master. The second set contains summaries of technologies that will continuously change over time.

