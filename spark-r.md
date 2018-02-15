![](/assets/sr1.png)

SparkR is a R package that provides a light-weight front-end to users of Apache Spark from R.

R is a popular statistical programming language with a number of extensions that support data processing and machine learning tasks. However, **interactive data analysis in R is usually limited, as the run time is single threaded and can only process data sets that fit in a single machines memory.** **SparkR, and R package initially developed in the AMP lab, provides a front-end to Apache Spark. And using Sparks distributed computation engine allows us to run large-scale data analysis from the R shell.** In Spark 1.61, SparkR provides a distributed dataframe implementation.

And this is the central component of SparkR. **Dataframes are a fundamental data structure used for data processing in R**, and the **concept of data frames has been extended to other languages with libraries like Pandas**. The distributed dataframe  implementation supports R operations like selection, filtering, aggregation, and so on, but on large data sets. Projects like dplyr have further simplified expressing complex data manipulation tasks on data frames. SparkR data frames present an API similar to dplyr and local R data frames that can scale to large datasets using support for distributed computation in Spark. **A data frame is a distributed collection of data, organized into named columns**. It is conceptually equivalent to a table in a relational database, or a data frame in R. Both with optimizations under the hood.

Data frames can be constructed from a wide array of sources such as structured data files, tables in Hive, external databases, or existing local R data frames.** SparkR also supports distributed machine learning using MLlib**. As we can see in the diagram on the left hand side, we have the R environment, with the Spark Context, the JVM, and the Java Spark Context. And then on the right hand side, we have the task distributed across the cluster so that we are not limited to single threading, or resourced on a single unit, a single machine.

We can use as many machines that are in the cluster. So, that raises a question, **why would you use SparkR? R, as we notice in the previous slide is restricted to single thread and the amount of memory on a single machine. So using R on Big Data is very difficult. SparkR is multi--threaded across many machines, as many machines as there are in the cluster, as well as having access to the memory and all machines in that cluster.**

A typical example would be where there's a large amount of initial data which needs cleaning, filtering, and aggregating before the statistical analysis can be performed. This means reducing the volume of raw data to a relevant subset, which can fit onto a single machine, where R can apply the statistical learning model. This is very difficult, if not impossible in R. Once we have the set of data we're going to work on, we need to train the model. Model training involves applying a number of parameters to learn which parameter value works best. **Most users want to do this parameter tuning in parallel, and aggregate the parameters to find the best model for the dataset.** **Performance in R is constrained by having to do this work on a single machine.**

**SparkR can do this across multiple nodes in a cluster, improving performance by several orders of magnitude.** When the raw data is very large, and the user wants to apply a number of features to the whole dataset, and so a distributed machine learning algorithm is needed. R cannot do this, but SparkR comes with a machine learning library and Spark operates in a distributed environment, so large scaled machine learning is now possible with R.







So, what features does SparkR have? We've already talked about the scalability with

many machines and many cores, operations being executed on SparkR dataframes get automatically

distributed across all the cores in the cluster. As a result of all of this, SparkR dataframes

can be used on terabytes of data, and run on clusters of thousands of machines. Another

benefit is the dataframes optimizations. SparkR dataframes inherit all the optimizations made

to the computation engine in terms of code, generation, and memory management. Then there

are all the data sources APIs, by tying into Sparks' SQL data sources API, SparkR can read

in from a variety of sources including Hive tables, JSON files, packet files, etc. Then

we have the RDDs as distributed lists. SparkR exposes the RDD API's of Spark as a distributed

list in R. For example we can read an input file in HDFS and process every line using

lapply on an RDD. In addition to lapply, SparkR also allows closures to be appplied

on every partition using lapply with partition. But the supported RDD functions include operations

like reduce, reduce by key, group by key, and collect. Then there's the serializing

the closures. SparkR automatically serializes the necessary variables to execute the function

on the cluster. For example, if we use some global variables in a function passed to

lapply, SparkR will automatically capture these variables and copy them to the cluster. In

addition, we can use existing R packages. SparkR also allows easy use of existing R

packages inside closures. The include package command can be used to indicate packages that

should be loaded before every closures executed on the cluster. Now we are going to look at

how we interface with SparkR. There are several ways to interface with SparkR. You can interface

through the Spark shell, you can interface through the SparkR shell, the difference between

the two being that the SparkR shell has the SQLContext and SparkContext already created

for you. You can use Rstudio, which is an integrated development environment. You can

use notebooks and a notebook gives you an interactive web-based editor, which you can

do all sorts of interesting things with. And there's the Data Scientists Workbench, which

provides a unified platform of diverse tools, capable of using open source tools including

Jupyter and Zepplin, as well as Rstudio, and we're going to look further into these. The

entry point into SparkR from the R environment is SparkContext. There is a conceptual R program

to a Spark cluster. First step in any Spark application is to create a Spark context.

Spark context allows your Spark application to access the cluster through open-source

managers such as YARN or Sparks own cluster manager. It represents the client connection

to a Spark execution environment, and has to be created before using any of Sparks features

or services in your applications, such as RDDs, accumulators, broadcast variables, etc.

To work with dataframes, we also need an SQLContext. And this is created from the SparkContext,

and provides the interface into Spark SQL. If you're working from the SparkR shell rather

than the Spark shell, the SQL context and SparkContext will already have been created

for you. Where as in the Spark shell, you'll have to create those yourself. With a SQLContext,

applications can create dataframes from a local R dataframe, from a Hive table, or from

other data sources. Spark SQL is a Spark module for structured data processing. It is a distributed

SQL engine designed to leverage the power of Sparks computation model, which is based

on RDDs. Unlike the basic Spark RDD API, the interface is provided by Spark SQL, provide

Spark with more information about the structure of both the data and the computation being performed.

Internally, Spark uses this extra information to perform extra optimizations. SparkR works

with dataframes, which means we will need an SQLContext, which can be created from the

SparkContext. The entry point into all the relational functionality in Spark is through

the SQLContext. There are several ways to interact with Spark SQL including SQL itself,

the DataFrames API and the Datasets API. Data analysts will likely use SQL as their query

language. The SQL function on the SQLContext enables applications to run SQL queries programmatically,

and return the results as a dataframe. Spark SQL also includes a data source API that can

read data from other databases using JDBC. This functionality should be preferred over

using JDBC RDD API. This is because the results are returned as a dataframe and can be easily

processed in Spark SQL or joined with other data sources. The JDBC data source is also

easier to use from Java or Python, as it does not require the user to provide the class

tag. Datasets are similar to RDDs, however instead of using Java serialization or Kryo,

they use a specialized encoder, to serialize the objects for processing or transmitting

of the network. When computing a result, the same execution engine is used, independent

of which API or language you are using to express the computation. This unification

means that developers can easily switch back and forth between the various, based upon

which one provides the most natural way to express a given transformation.



