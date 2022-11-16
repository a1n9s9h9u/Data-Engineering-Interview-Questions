## Data Engineering Interview Questions

#### Azure Data Factory

Azure Data Factory is the cloud-based ETL and data integration service that allows you to create data-driven workflows for orchestrating data movement and transforming data at scale. Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores. You can build complex ETL processes that transform data visually with data flows or by using compute services such as Azure HDInsight Hadoop, Azure Databricks, and Azure SQL Database.

Additionally, you can publish your transformed data to data stores such as Azure Synapse Analytics for business intelligence (BI) applications to consume. Ultimately, through Azure Data Factory, raw data can be organized into meaningful data stores and data lakes for better business decisions.

#### Pipeline, Activities, Datasets, and Linked services

A data factory might have one or more pipelines. A pipeline is a logical grouping of activities that performs a unit of work. Together, the activities in a pipeline perform a task.

Activities represent a processing step in a pipeline. For example, you might use a copy activity to copy data from one data store to another data store.

Datasets represent data structures within the data stores, which simply point to or reference the data you want to use in your activities as inputs or outputs.

Linked services are much like connection strings, which define the connection information that's needed for Data Factory to connect to external resources. Think of it this way: a linked service defines the connection to the data source, and a dataset represents the structure of the data.

For example, an Azure Storage-linked service specifies a connection string to connect to the Azure Storage account. Additionally, an Azure blob dataset specifies the blob container and the folder that contains the data.

#### Integration runtime

In Data Factory, an activity defines the action to be performed. A linked service defines a target data store or a compute service. An integration runtime provides the bridge between the activity and linked Services. It's referenced by the linked service or activity, and provides the compute environment where the activity either runs on or gets dispatched from. This way, the activity can be performed in the region closest possible to the target data store or compute service in the most performant way while meeting security and compliance needs.

#### Triggers

Triggers represent the unit of processing that determines when a pipeline execution needs to be kicked off.

#### Incrementally load data

#### Delta data loading from database by using a watermark

A watermark is a column that has the last updated time stamp or an incrementing key. The delta loading solution loads the changed data between an old watermark and a new watermark.

#### Delta data loading from SQL DB by using the Change Tracking technology

Change Tracking technology is a lightweight solution in SQL Server and Azure SQL Database that provides an efficient change tracking mechanism for applications. It enables an application to easily identify data that was inserted, updated, or deleted.

#### Loading new and changed files only by using LastModifiedDate

You can copy the new and changed files only by using LastModifiedDate to the destination store. ADF will scan all the files from the source store, apply the file filter by their LastModifiedDate, and only copy the new and updated file since last time to the destination store.

#### Loading new files only by using time partitioned folder or file name

You can copy new files only, where files or folders has already been time partitioned with timeslice information as part of the file or folder name (for example, /yyyy/mm/dd/file.csv). It is the most performant approach for incrementally loading new files.

#### Azure Databricks

Azure Databricks is a data analytics platform optimized for the Microsoft Azure cloud services platform. Azure Databricks offers three environments for developing data intensive applications: Databricks SQL, Databricks Data Science & Engineering, and Databricks Machine Learning.

Databricks SQL provides an easy-to-use platform for analysts who want to run SQL queries on their data lake, create multiple visualization types to explore query results from different perspectives, and build and share dashboards.

Databricks Data Science & Engineering provides an interactive workspace that enables collaboration between data engineers, data scientists, and machine learning engineers. For a big data pipeline, the data (raw or structured) is ingested into Azure through Azure Data Factory in batches, or streamed near real-time using Apache Kafka, Event Hub, or IoT Hub. This data lands in a data lake for long term persisted storage, in Azure Blob Storage or Azure Data Lake Storage. As part of your analytics workflow, use Azure Databricks to read data from multiple data sources and turn it into breakthrough insights using Spark.

Databricks Machine Learning is an integrated end-to-end machine learning environment incorporating managed services for experiment tracking, model training, feature development and management, and feature and model serving.

#### Azure Blob storage

Azure Blob storage is Microsoft's object storage solution for the cloud. Blob storage is optimized for storing massive amounts of unstructured data. Unstructured data is data that doesn't adhere to a particular data model or definition, such as text or binary data.

#### Azure Data Lake Storage Gen2

Blob storage supports Azure Data Lake Storage Gen2, Microsoft's enterprise big data analytics solution for the cloud. Azure Data Lake Storage Gen2 offers a hierarchical file system as well as the advantages of Blob storage, including:

Low-cost, tiered storage
High availability
Strong consistency
Disaster recovery capabilities

#### Storage account

A storage account provides a unique namespace in Azure for your data. Every object that you store in Azure Storage has an address that includes your unique account name. The combination of the account name and the Blob Storage endpoint forms the base address for the objects in your storage account.

#### Container

A container organizes a set of blobs, similar to a directory in a file system. A storage account can include an unlimited number of containers, and a container can store an unlimited number of blobs.

#### Azure Storage supports three types of blobs:

Block blobs store text and binary data. Block blobs are made up of blocks of data that can be managed individually. Block blobs can store up to about 190.7 TiB.

Append blobs are made up of blocks like block blobs, but are optimized for append operations. Append blobs are ideal for scenarios such as logging data from virtual machines.

Page blobs store random access files up to 8 TiB in size. Page blobs store virtual hard drive (VHD) files and serve as disks for Azure virtual machines.

#### Create mount point for blob storage:
```pyspark
dbutils.fs.mount(
  source = "wasbs://<container-name>@<storage-account-name>.blob.core.windows.net",
  mount_point = "/mnt/iotdata",
  extra_configs = {"fs.azure.account.key.<storage-account-name>.blob.core.windows.net":dbutils.secrets.get(scope = "<scope-name>", key = "<key-name>")})
```
#### Run a databricks notebook from another notebook:
```pyspark
dbutils.notebook.run("notebook-name", 60, {"argument": "data", "argument2": "data2", ...})
```
#### Get output from a databricks notebook:
```pyspark
dbutils.notebook.exit("returnValue")
```
#### Types of IR

Data Factory offers three types of Integration Runtime (IR), and you should choose the type that best serves your data integration capabilities and network environment requirements. The three types of IR are:

Azure
Self-hosted
Azure-SSIS

#### An Azure integration runtime can:

Run Data Flows in Azure
Run copy activities between cloud data stores

Azure Integration Runtime is managed by Microsoft. All the patching, scaling and maintenance of the underlying infrastructure is taken care of. The IR can only access data stores and services in public networks.

Self-hosted Integration Runtimes use infrastructure and hardware managed by you. You’ll need to address all the patching, scaling and maintenance. The IR can access resources in both public and private networks.

Azure-SSIS Integration Runtimes are VMs running the SSIS engine which allow you to natively execute SSIS packages. They are managed by Microsoft. As a result, all the patching, scaling and maintenance is taken care of. The IR can access resources in both public and private networks.

#### Azure data bricks, cluster and its modes and types

Azure Databricks supports three cluster modes: Standard, High Concurrency, and Single Node. The default cluster mode is Standard. Standard and Single Node clusters terminate automatically after 120 minutes by default. High Concurrency clusters do not terminate automatically by default. You cannot change the cluster mode after a cluster is created. If you want a different cluster mode, you must create a new cluster.

A Standard cluster is recommended for a single user. Standard clusters can run workloads developed in any language: Python, SQL, R, and Scala.

A High Concurrency cluster is a managed cloud resource. The key benefits of High Concurrency clusters are that they provide fine-grained sharing for maximum resource utilization and minimum query latencies.

A Single Node cluster has no workers and runs Spark jobs on the driver node. In contrast, a Standard cluster requires at least one Spark worker node in addition to the driver node to execute Spark jobs.

#### Append Variable activity in Azure Data Factory

Use the Append Variable activity to add a value to an existing array variable defined in a Data Factory or Synapse Analytics pipeline.

#### Filter activity in Azure Data Factory

You can use a Filter activity in a pipeline to apply a filter expression to an input array.

#### Switch activity in Azure Data Factory

The Switch activity provides the same functionality that a switch statement provides in programming languages. It evaluates a set of activities corresponding to a case that matches the condition evaluation.

#### What happens in the back-end when you submit a Spark Job?

When a client submits a spark user application code, the driver implicitly converts the code containing transformations and actions into a logical directed acyclic graph (DAG). At this stage, the driver program also performs certain optimizations like pipelining transformations, and then it converts the logical DAG into a physical execution plan with a set of stages. After creating the physical execution plan, it creates small physical execution units referred to as tasks under each stage. Then tasks are bundled to be sent to the Spark Cluster.

The driver program then talks to the cluster manager and negotiates for resources. The cluster manager then launches executors on the worker nodes on behalf of the driver. At this point the driver sends tasks to the cluster manager based on data placement. Before executors begin execution, they register themselves with the driver program so that the driver has holistic view of all the executors. Now executors start executing the various tasks assigned by the driver program. At any point of time when the spark application is running, the driver program will monitor the set of executors that run. Driver program in the spark architecture also schedules future tasks based on data placement by tracking the location of cached data. When driver program main () method exits or when it call the stop () method of the Spark Context, it will terminate all the executors and release the resources from the cluster manager.

#### What is the optimized way of loading data to Azure Synapse from Azure Data Factory?

Polybase is the most efficient way to move data into Azure Synapse Analytics. Use the staging blob feature to achieve high load speeds from all types of data stores, including Azure Blob storage and Data Lake Store. (Polybase supports Azure Blob storage and Azure Data Lake Store by default.)

#### How to improve or resolve performance based issues in ETL processes?

#### Make Partitions of Large Tables

Large tables can take a long time to move from one database to another. If the process breaks, you have to reload the whole table again and this is time consuming. To improve the processing time, simply partition the large tables. You can use any key value to partition the tables, either by date, or by the middle value, or by an index number.

#### Tackle Bottlenecks

Find out which process takes the most resources in the overall ETL process. There will be tasks such as transformations of larger tables that may consume more resources at a single time. Pin point all these processes and address the one that consumes the most resources. Maybe there is a faster way to solve the issue. Maybe you can create a separate workflow and run both processes in parallel.

#### Eliminate database Reads/Writes

While applying transformations to the data, you may have to stage data and perform read/write operations on the database. Databases can have more overhead costs. So, ETL teams can dump all this data into flat files and then use those flat files to load data into the data warehouse. Flat files are lighter and easier to load. With a lot of tables to be loaded, the process becomes easier and takes less time.

#### Cache the Data

Caching data in advance can speed up the whole ETL process, but it would require more storage and RAM.

#### Use Parallel Processing

The best way to improve ETL process performance is by processing in parallel. Transformation processes like sort and aggregate functions on one workflow can be done in parallel with another workflow that loads data directly to the data warehouse.

#### Filter Unnecessary Datasets

Reduce the number of rows processed in the ETL workflow. You can do this by filtering datasets that don’t need to be transformed and then passing them directly, while creating a separate transformation cycle for datasets that do need filtering. This will reduce time in the number crunching process.

#### Load Data Incrementally

Loading all of the data from the data mart at a single time can involve multiple resources. It is better to segment data that is essential for the data warehouse and load it in batches. This would reduce the load time and increase performance considerably. Moreover, it will also take away the burden of resource blockage once and for all.

#### ETL Scheduling

If you are still processing all the ETL jobs manually then that is the biggest performance hindrance. Modern ETL performance testing and data integration tools are equipped with job schedulers that you can use to automate data integration tasks. It would mean that you will no longer have to manually start the process every week.

#### How do I deploy microservices in Azure?

To deploy your microservices, you need to create an Azure Container Registry in the same location where your services are deployed, and link the registry to a resource group. Your registry will manage container instances that will be deployed to a Kubernetes cluster.

Azure Kubernetes Service (AKS). AKS is a managed Kubernetes cluster hosted in the Azure cloud. When using AKS, Azure manages the Kubernetes API service, and you only need to manage the agent nodes.

Avoid storing persistent data in local cluster storage because that ties the data to the node. Instead, use an external service such as Azure SQL Database or Cosmos DB. Another option is to mount a persistent data volume to a solution using Azure Disks or Azure Files.

#### Types of index:

Clustered Index: A clustered index defines the order in which data is physically stored in a table. Table data can be sorted in only one way, therefore, there can be only one clustered index per table. The primary key constraint automatically creates a clustered index on that particular column.

Non-Clustered Indexes: A non-clustered index doesn’t sort the physical data inside the table. In fact, a non-clustered index is stored at one place and table data is stored in another place. This is similar to a textbook where the book content is located in one place and the index is located in another. This allows for more than one non-clustered index per table.

#### Operation affecting performance of index:

The number of indexes on a table is the most dominant factor for insert performance. The more indexes a table has, the slower the execution becomes. The insert statement is the only operation that cannot directly benefit from indexing because it has no where clause.

#### What is partition and bucketing?

Partitioning helps in elimination of data, if used in WHERE clause, where as bucketing helps in organizing data in each partition into multiple files, so as same set of data is always written in same bucket. Partition divides large amount of data into multiple slices based on value of a table column(s). Bucketing decomposes data into more manageable or equal parts.

With partitioning, there is a possibility that you can create multiple small partitions based on column values. If you go for bucketing, you are restricting number of buckets to store the data. This number is defined during table creation scripts.

#### In which scenario partition is neglected and bucketing is suitable?

Partitioning helps in elimination of data, if used in WHERE clause, whereas bucketing helps in organizing data in each partition into multiple files, so the same set of data is always written in the same bucket. Helps a lot in joining columns.

#### What is a small file issue in hive?

A small file is one which is significantly smaller than the HDFS block size (default 64MB). Map tasks usually process a block of input at a time (using the default FileInputFormat). If the file is very small and there are a lot of them, then each map task processes very little input, and there are a lot more map tasks, each of which imposes extra bookkeeping overhead. Compare a 1GB file broken into 16 64MB blocks, and 10,000 or so 100KB files. The 10,000 files use one map each, and the job time can be tens or hundreds of times slower than the equivalent one with a single input file.

#### In which cases dynamic partitioning is suitable?

Dynamic Partition takes more time in loading data compared to static partition. When you have large data stored in a table then the Dynamic partition is suitable. If you want to partition a number of columns but you don't know how many columns then also dynamic partition is suitable.

#### How is Cosmos DB different from Synapse or SQL Database?

Azure Cosmos DB is Microsoft’s NoSQL database as a service (DaaS), designed to take advantage of elasticity and flexibility and to satisfy the needs of IoT and global-facing, cloud-based applications. It offers access methods, consistency models, cost structures and ways of looking at data that are different from a relational database management system (RDBMS) like SQL Server.

The two platforms differ around scalability because of their basic design: SQL Server was built with data consistency and integrity as the No. 1 mission, while Cosmos DB was designed for geographic distribution and speed, moving the data closer to the user and with features tightly coupled with the needs of IoT systems. Like all NoSQL database platforms, eventual consistency is a primary principle for Cosmos DB.

In SQL Server, to ensure data consistency and integrity, transactions are handled sequentially and almost always committed to a single server. If you need more power or throughput, you add more hardware (CPU, memory, disk speed, disk size, network bandwidth).

#### Which distribution type would be optimal for Azure Synapse analytics staging table?

A round-robin table is the most straightforward table to create and delivers fast performance when used as a staging table for loads. A round-robin distributed table distributes data evenly across the table but without any further optimization.

#### What type of triggers we have in azure BI components.

Schedule trigger: A trigger that invokes a pipeline on a wall-clock schedule.

Tumbling window trigger: A trigger that operates on a periodic interval, while also retaining state.

Event-based trigger: A trigger that responds to an event.

#### Define azure storage key.

Azure storage key is used for authentication for validating access for the azure storage service to control access of data based on the project requirements. 2 types of storage keys are given for the authentication purpose -

Primary Access Key
Secondary Access Key

The main purpose of the secondary access key is for avoiding downtime of the website or application.

#### What are the differences between the Azure Table Storage and the Azure SQL service?

#### Table Storage Service

This follows a NoSQL type of storage on Azure.

The data is stored in key-value format and is referred to as Entity.

The relationship between tables is not possible.

The partition and row key combination are considered unique for each entity.

#### Azure SQL Table

This follows the relational storage structure on Azure.

The data here is stored in rows and columns combination in the SQL table.

Relationships between tables are defined by means of the foreign keys.

Uniqueness can be defined by the user by means of a primary key or unique key.

#### When copying data from or to an Azure SQL Database using Data Factory, what is the firewall option that we should enable to allow the Data Factory to access that database?

Allow Azure services and resources to access this server firewall option.

#### If we need to copy data from an on-premises SQL Server instance using Data Factory, which Integration Runtime should be used and where should it be installed?

Self-Hosted Integration Runtime should be installed on the on-premises machine where the SQL Server instance is hosted.

#### What is the difference between the Mapping data flow and Wrangling data flow transformation activities in Data Factory?

Mapping data flow activity is a visually designed data transformation activity that allows us to design a graphical data transformation logic without the need to be an expert developer, and executed as an activity within the ADF pipeline on an ADF fully managed scaled-out Spark cluster.

Wrangling data flow activity is a code-free data preparation activity that integrates with Power Query Online in order to make the Power Query M functions available for data wrangling using spark execution.

#### Which Data Factory activity is used to run an SSIS package in Azure?

Execute SSIS Package activity.

#### Which Data Factory activity can be used to get the list of all source files in a specific storage account and the properties of each file located in that storage?

Get Metadata activity.

#### Which Data Factory activities can be used to iterate through all files stored in a specific storage account, making sure that the files smaller than 1KB will be deleted from the source storage account?

ForEach activity for iteration.

Get Metadata to get the size of all files in the source storage.

If Condition to check the size of the files.

Delete activity to delete all files smaller than 1KB.

#### Any Data Factory pipeline can be executed using three methods. Mention these methods:

Under Debug mode.

Manual execution using Trigger now.

Using an added scheduled, tumbling window or event trigger.

#### Data Factory supports four types of execution dependencies between the ADF activities. Which dependency guarantees that the next activity will be executed regardless of the status of the previous activity?

Completion dependency.

#### Data Factory supports four types of execution dependencies between the ADF activities. Which dependency guarantees that the next activity will be executed only if the previous activity is not executed?

Skipped dependency.

#### From where we can monitor the execution of a pipeline that is executed under the Debug mode?

The Output tab of the pipeline, without the ability to use the Pipeline runs or Trigger runs under the ADF Monitor window to monitor it.

#### What do you understand by Data Modelling?

Data modeling is the process of documenting complicated software design as a plan so that anyone can quickly grasp it. It is a conceptual illustration of data objects that are incorporated between several data objects and the rules.

#### Name different sorts of design schemas in the Data Modelling.

There are generally two kinds of schemas in the data modelling:

Star schema
Snowflake schema.

#### What is the boundary on the number of integration runtimes?

There is no limit on the amount of integration runtime cases in a data factory. There is, nonetheless, a limit on the amount of VM cores that the integration runtime can work per subscription for SSIS package performance.

#### As a certified data engineer in a global company, you are asked to transfer 18 OLTP databases to Microsoft Azure. While most of the days, the database utilization is not large. But while few days from every week, a large number of records will be stored in these databases, needing extra resources to place and prepare the data. What is the target Azure data program that you will work to satisfy your requirements?

I will use Azure SQL Database Elastic Pools. It is the good choice for the hosting databases with unstable workload in Azure.

#### List the 4 V’s of big data.

Velocity: Velocity, or speed, refers to the enormous speed with which data is generated and processed.

Volume: It is not surprising that Big Data is large in volume. It is estimated that we create 2.3 trillion gigabytes of data every day. And that will only increase. This increase is of course partly caused by the gigantic mobile telephone network.

Variety: The high speed and considerable volume are related to the variety of forms of data. After all, smart IT solutions are available today for all sectors, from the medical world to construction and business.

Veracity: How truthful Big Data is remains a difficult point. Data quickly becomes outdated and the information shared via the internet and social media does not necessarily have to be correct.

#### What is the difference between Azure Data Lake store and Blob storage?

#### Azure Data Lake Storage

Optimized storage for big data analytics workloads.

Hierarchical file system.

Batch, interactive, streaming analytics, and machine learning data such as log files, IoT data, clickstreams, large datasets.

#### Azure Blob Storage

General-purpose object store for a wide variety of storage scenarios, including big data analytics.

Object store with flat namespace.

Any type of text or binary data, such as application back end, backup data, media storage for streaming, and general-purpose data. Additionally, full support for analytics workloads; batch, interactive, streaming analytics, and machine learning data such as log files, IoT data, clickstreams, large datasets.

#### What are data masking features available in Azure?

Dynamic data masking plays various significant roles in data security. It restricts sensitive information to some specific set of users.

It is available for Azure SQL Database, Azure SQL Managed Instance and Azure Synapse Analytics.

It can be implemented as a security policy on all the SQL Databases across an Azure subscription.

Users can control the level of masking as per their requirements.

#### What is Azure Databricks, and how is it different from regular data bricks?

It is the Azure implementation of Apache Spark that is an open-source big data processing platform. In the data lifecycle, Azure Databricks lies in the data preparation or processing stage. First of all, data is ingested in Azure using Data Factory and stored in permanent storage (such as ADLS Gen2 or Blob Storage). Further, data is processed using Machine Learning (ML) in Databricks and then extracted insights are loaded into the Analysis Services in Azure like Azure Synapse Analytics or Cosmos DB. Finally, insights are visualised and presented to the end-users with the help of Analytical reporting tools like Power BI.

#### What are multi-model databases?

Cosmos DB is Microsoft’s premier NoSQL service offering on Azure. It is the first globally distributed, multi-model database offered on the cloud by any vendor. It is used to store data in various data storage models such as Key-value pair, document-based, graph-based, column-family based, etc. Low latency, consistency, global distribution and automatic indexing features are the same no matter what data model the customer chooses.

H#### ow Does Microsoft Azure Compare to Aws?

In my opinion Azure is a better choice because it’s a Microsoft product, making it easier for organizations already using Windows Server, SQL Server, and Exchange to move to the cloud. In addition, because of Microsoft’s deep knowledge of developer tools, Azure offers multiple app deployment options for developers, which makes it stand out against AWS.

Although I like to be open minded and I want to work on different clouds as well so I will be happy if I have to work on another cloud because of some project requirements.

#### What are the instance types offered by Azure?

General Purpose - CPU to memory ratio is balanced. Provides low to medium traffic web servers, small to medium databases and is ideal for testing and development.

Compute Optimized - High CPU to memory ratio. Best suited for medium traffic web servers, application servers, batch processes, and network appliances.

Memory-Optimized - High memory to CPU ratio. Best suited for relational database servers, in-memory analytics, and medium to large caches.

Storage Optimized - Provides high disk IO and throughput. Best suited for Big Data, NoSQL and SQL Databases.

GPU - Virtual Machines that specialize in heavy graphic rendering and video editing. It also helps with model training and inferencing with deep learning.
Why you will use the data flow from the Azure data factory?

#### Data flow

Data flow is used for a no-code transformation. For example when you are doing any ETL operation that you wanted to do a couple of transformations and put some logic on your input data. You may have not found it comfortable to type the query or when you are using the files as input then in that case you cannot write the query at all. Hence data flow will come as a Savior in this situation. Using the data flow you can just do drag and drop and write almost all your business logic without writing any code. Behind the scene, data flow get converted into the spark code and it will run on the cluster.

#### What is the foreach activity in the data factory?

In the Azure data factory whenever you have to do some of the work repetitively then probably you will be going to use the foreach activity. In the foreach activity, you pass an array and the foreach loop will run for all the items of this array.

#### What is the get metadata activity in the Azure data factory?

In the Azure data factory get metadata activity is used to get the information about the files. For example, in some cases, you want to know the name of the file you want to know, the size of the file, or maybe you want to know the last modified date of a file. So all those kinds of metadata information about the file you can get it using the get metadata activity.

#### What is the custom activity in the Azure data factory?

Custom activity is used in the Azure data factory to execute the Python or a PowerShell script. Assume that you have some code that is written in the Python or PowerShell script and you wanted to execute as a part of your pipeline. Then you can use a custom activity that will help you to execute the code.

#### How you can connect the Azure data factory with the Azure Databricks?

To connect to Azure databricks we have to create a linked service that will point to the Azure databricks account. Next in the pipeline, you will be going to use the notebook activity there you will provide the linked service created for Databricks.

#### Is it possible to connect MongoDB DB from the Azure data factory?

Yes, it is possible to connect MongoDB from the Azure data factory. You have to provide the proper connection information about the MongoDB server. In case if this MongoDB server is residing outside the Azure workspace then probably you have to create a self-hosted integration runtime, and through which you can connect to the Mongo DB server.

#### How to connect Azure data factory to GitHub?

Azure data factory can connect to GitHub using the GIT integration. You probably have using the Azure DevOps which has git repo. We can configure the GIT repository path into the Azure data factory. So that all the changes we do in the Azure data factory get automatically sync with the GitHub repository.

#### How you can move your changes from one environment to another environment for the Azure data factory?

We can migrate the code from one environment to another environment for the Azure data factory using the ARM template. ARM template is the JSON representation of the pipeline that we have created.

#### How you can use Apache Spark through Azure Synapse Analytics?

In Azure analytics, you can run the spark code either using the notebook or you can create a job that will run the spark code. For running the Spark code you need a Spark pool which is nothing just a cluster of the nodes having a spark installed on it.

#### What is Delta Lake?

Delta Lake is an open-source storage layer that brings ACID (atomicity, consistency, isolation, and durability) transactions to Apache Spark and big data workloads. The current version of Delta Lake included with Azure Synapse has language support for Scala, PySpark, and .NET.

#### Can you run machine learning algorithm using Azure Synapse Analytics?

Yes, it is possible to run the machine learning algorithm using Azure synapse Analytics. In the Azure synapse analytics, we have an Apache Spark and there we can write the machine learning code and which can be executed on the Spark cluster.

#### What are the two different types of execution modes provided by the Databricks?

You can run the Spark code in two modes that are interactive mode or job scheduled mode. In the interactive mode, you can run the code line by line and see the output. In the job scheduled mode, it will run all code together, and then you will see the output.

#### What are the two different types of the cluster provided by the Databricks?

Two different types of the cluster provided by the Databricks are the interactive cluster and the job cluster. To run the interactive notebook you will be going to use an interactive cluster and to run the job, we will use the job cluster.

#### How you can run the python code in the SCALA notebook in the Azure Databricks?

We can run the python code in the SCALA notebook by typing ‘%python’ at the start of the cell. This will prompt the notebook to treat this cell as the python code instead of the SCALA code.

#### Difference Between Fact Table and Dimension Table

Fact table contains measurements, metrics, and facts about a business process while the Dimension table is a companion to the fact table which contains descriptive attributes to be used as query constraining.

Fact table is located at the center of a star or snowflake schema, whereas the Dimension table is located at the edges of the star or snowflake schema.

Fact table helps to store report labels whereas Dimension table contains detailed data.

Fact table does not contain a hierarchy whereas the Dimension table contains hierarchies.

#### Azure Cosmos DB

Azure Cosmos DB is a fully managed NoSQL database for modern app development. Single-digit millisecond response times, and automatic and instant scalability, guarantee speed at any scale. As a fully managed service, Azure Cosmos DB takes database administration off your hands with automatic management, updates and patching. It also handles capacity management with cost-effective serverless and automatic scaling options that respond to application needs to match capacity with demand.

Any web, mobile, gaming, and IoT application that needs to handle massive amounts of data, reads, and writes at a global scale with near-real response times for a variety of data will benefit from Cosmos DB's guaranteed high availability, high throughput, and low latency.

#### Azure Cosmos DB offers multiple database APIs, which include the Core (SQL) API, API for MongoDB, Cassandra API, Gremlin API, and Table API:

By using these APIs, you can model real world data using documents, key-value, graph, and column-family data models. These APIs allow your applications to treat Azure Cosmos DB as if it were various other databases technologies, without the overhead of management, and scaling approaches.

Core(SQL) API stores data in document format. It offers the best end-to-end experience as we have full control over the interface, service, and the SDK client libraries. Any new feature that is rolled out to Azure Cosmos DB is first available on SQL API accounts. Azure Cosmos DB SQL API accounts provide support for querying items using the Structured Query Language (SQL) syntax.
If you are migrating from other databases such as Oracle, DynamoDB, HBase etc. and if you want to use the modernized technologies to build your apps, SQL API is the recommended option.

API for MongoDB stores data in a document structure. It is compatible with MongoDB wire protocol; however, it does not use any native MongoDB related code. This API is a great choice if you want to use the broader MongoDB ecosystem and skills, without compromising on using Azure Cosmos DB features such as scaling, high availability, geo-replication, multiple write locations, and more.

You can use your existing MongoDB apps with API for MongoDB by just changing the connection string.

Cassandra API stores data in column-oriented schema. Apache Cassandra offers a highly distributed, horizontally scaling approach to storing large volumes of data while offering a flexible approach to a column-oriented schema. Cassandra API in Azure Cosmos DB aligns with this philosophy to approaching distributed NoSQL databases.

You should consider Cassandra API if you want to benefit the elasticity and fully managed nature of Azure Cosmos DB and still use most of the native Apache Cassandra features, tools, and ecosystem. This means on Cassandra API you don't need to manage the OS, Java VM, garbage collector, read/write performance, nodes, clusters, etc.

Gremlin API allows users to make graph queries and stores data as edges and vertices. Use this API for scenarios involving dynamic data, data with complex relations, data that is too complex to be modeled with relational databases, and if you want to use the existing Gremlin ecosystem and skills. The Azure Cosmos DB Gremlin API combines the power of graph database algorithms with highly scalable, managed infrastructure. It provides a unique, flexible solution to most common data problems associated with lack of flexibility and relational approaches.

Table API stores data in key/value format. If you are currently using Azure Table storage, you may see some limitations in latency, scaling, throughput, global distribution, index management, low query performance. Table API overcomes these limitations and it's recommended to migrate your app if you want to use the benefits of Azure Cosmos DB.

#### Explain the differences between NoSQL and relational databases:

Relational Database provide store of related tables while NoSQL stores the unstructured or semi-structured data in the form of key/value or JSON documents.

Relational DB has fixed schema while NoSQL DB has dynamic schema.

Relational DB use SQL (Structured Query Language) to manage the data, NoSQL DB have many models for managing and accessing the data.

Relational Tables provide ACID guarantees but NoSQL does not provide ACID guarantees beyond the scope of single DB partition.

Relational DBs are mature, proven and widely used where as NoSQL is high performance database with ease-of-use, resilience, scalability and availability characteristics.

#### What do you think about HIPAA compliances for Azure Cosmos DB ?

HIPAA establishes the standards to use, safeguarding and disclose the identifiable health information of any individual. Azure Cosmos DB fully supports HIPAA Compliance or it's HIPAA compliant.

#### Is there any storage limit of Cosmos DB?

There is no storage limit for a Cosmos container. It can store any amount of data.

#### What is azure cosmos db container?

CosmosDB containers are the database units that determine scalability in terms of both throughput and storage. Containers are partitioned horizontally and then replicated across different regions.

#### What do you mean by partitioning in Cosmos DB?

Azure Cosmos DB uses partitioning to scale individual containers in a database to meet the performance needs of your application. In partitioning, the items in a container are divided into distinct subsets called logical partitions. Logical partitions are formed based on the value of a partition key that is associated with each item in a container. All the items in a logical partition have the same partition key value.

For example, a container holds items. Each item has a unique value for the UserID property. If UserID serves as the partition key for the items in the container and there are 1,000 unique UserID values, 1,000 logical partitions are created for the container.

In addition to a partition key that determines the item's logical partition, each item in a container has an item ID (unique within a logical partition). Combining the partition key and the item ID creates the item's index, which uniquely identifies the item.

A container is scaled by distributing data and throughput across physical partitions. Internally, one or more logical partitions are mapped to a single physical partition. Typically smaller containers have many logical partitions but they only require a single physical partition. Unlike logical partitions, physical partitions are an internal implementation of the system and they are entirely managed by Azure Cosmos DB.

#### How Does Azure Cosmos Db Offer Predictable Performance?

A request unit (RU) is the measure of throughput in Azure Cosmos DB. A 1-RU throughput corresponds to the throughput of the GET of a 1-KB document. Every operation in Azure Cosmos DB, including reads, writes, SQL queries, and stored procedure executions, has a deterministic RU value that's based on the throughput required to complete the operation. Instead of thinking about CPU, IO, and memory and how they each affect your application throughput, you can think in terms of a single RU measure.

You can reserve each Azure Cosmos DB container with provisioned throughput in terms of RUs of throughput per second. For applications of any scale, you can benchmark individual requests to measure their RU values, and provision a container to handle the total of request units across all requests. You can also scale up or scale down your container's throughput as the needs of your application evolve.

#### What are the different distribution techniques while you ingest the data in SQL dedicated pool?

#### A hash distributed table can deliver the highest query performance for joins and aggregations on large tables.

To shard data into a hash-distributed table, dedicated SQL pool uses a hash function to deterministically assign each row to one distribution. In the table definition, one of the columns is designated as the distribution column. The hash function uses the values in the distribution column to assign each row to a distribution.

#### A round-robin table is the simplest table to create and delivers fast performance when used as a staging table for loads.

A round-robin distributed table distributes data evenly across the table but without any further optimization. A distribution is first chosen at random and then buffers of rows are assigned to distributions sequentially. It is quick to load data into a round-robin table, but query performance can often be better with hash distributed tables. Joins on round-robin tables require reshuffling data, which takes additional time.

#### A replicated table provides the fastest query performance for small tables.

A table that is replicated caches a full copy of the table on each compute node. So, replicating a table removes the need to transfer data among compute nodes before a join or aggregation. Replicated tables are best utilized with small tables. Extra storage is required and there is additional overhead that is incurred when writing data, which make large tables impractical.

#### What is DWU in Azure synapse?

Data Warehouse Units are compute scale units that combine CPU, memory, and I/O resources (DWUs). A DWU is a normalised, abstract measure of compute resources and performance.

#### What is difference between Azure Databricks and azure synapse?

Azure Synapse combines enterprise data warehouse and big data analytics into a single platform. Whereas Databricks not only performs big data analytics but moreover enables users to create complicated machine learning (ML) solutions at scale.

#### What is a Data Lakehouse?

A data lakehouse is a new, open data management architecture that combines the flexibility, cost-efficiency, and scale of data lakes with the data management and ACID transactions of data warehouses, enabling business intelligence (BI) and machine learning (ML) on all data.

#### What is HTAP?

HTAP stands for Hybrid Transactional and Analytical Processing. HTAP is used to describe the capability of a single database that can perform both online transaction processing (OLTP) and online analytical processing (OLAP) for the purpose of real-time operational intelligence processing.

#### What is PolyBase?

PolyBase allows processing data using native SQL queries from the external data sources. PolyBase allows you to join data from a SQL Server instance with external data. PolyBase is the fastest and most scalable way to load data. PolyBase can read data from several file formats and data sources. The data warehouse component of Azure Synapse Analytics service is a relational big data store that uses a massively parallel processing (MPP) architecture.

#### How to recover the data when you delete the external table?

Whenever you delete the external table your data won’t get deleted because we just point to the data location in the external table. Data will still be there on the referenced location. Here you have to just recreate the external table, pointing to the same location and you will be able to access the data once again.

#### CSV vs Parquet

In a CSV file (remember, row-oriented) each record is a row. In Parquet, however, it is each column that is stored independently. The most extreme difference is noticed when, in a CSV file, we want to read only one column. Although we only want to access the information of one column, because of the format type, we inevitably have to read all the rows of the table. When using Parquet format, each column is accessible independently from the rest.

Another feature of Parquet is that it is a self-describing data format that embeds the schema or structure within the data itself. That is, properties (or metadata) of the data such as the type (whether it is an integer, a real or a string), the number of values, the type of compression (data can be compressed to save space), etc. are included in the file itself along with the data as such. In this way, any program used to read the data can access this metadata, for example, to determine unambiguously what type of data is expected to be read in a given column.

#### ADLS Gen1 vs ADLS Gen2

Azure Data Lake Gen 1 is file system storage in which data is distributed in blocks in a hierarchical file system. Azure Data Lake Gen 2 contains both file system storage for performance & security and object storage for scalability.

Azure Data Lake Gen1 does not support Hot/Cold and Redundant storage. Whereas Azure Data Lake Gen2 supports Hot/Cold and Redundant storage.

#### spill to disk and shuffle write are two different things

spill to disk - Data move from Host RAM to Host Disk - is used when there is no enough RAM on your machine, and it place part of its RAM into disk

shuffle write - Data move from Executor(s) to another Executor(s) - is used when data needs to move between executors (e.g. due to JOIN, groupBy, etc)

#### Data Lake vs Data Warehouse vs Data Lakehouse vs Data Mesh vs Data Fabric

Data Warehouse is the central Repository for clean and organized business operational data.

Data Lake dumps all the data into one place from where all the analysis can be done to abstract data insights.

Data Lakehouse is the open data management architecture that combines Data Warehouse with DataLake.

Data Mesh is the new age architecture in which we divide data ownership with individual teams called data products and consume data from there unlike central ownership of data in the data lake platform.

Data Fabric can access data from different sources like EDW, different cloud platforms, RDBMS, SAAS applications, flat files, etc. It helps in maintaining data privacy by offering different features like masking, editing sensitive data, etc.
