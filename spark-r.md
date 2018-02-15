![](/assets/sr1.png)



 SparkR is a R package

that provides a light-weight front-end to users of Apache Spark from R. R is a popular

statistical programming language with a number of extensions that support data processing

and machine learning tasks. However, interactive data analysis in R is usually limited, as

the run time is single threaded and can only process data sets that fit in a single machines

memory. SparkR, and R package initially developed in the AMP lab, provides a front-end to Apache

Spark. And using Sparks distributed computation engine allows us to run large-scale data analysis

from the R shell. In Spark 1.61, SparkR provides a distributed dataframe implementation. And

this is the central component of SparkR. Dataframes are a fundamental data structure used for data

processing in R, and the concept of data frames has been extended to other languages with

libraries like Pandas. The distributed dataframe implementation supports R operations like

selection, filtering, aggregation, and so on, but on large data sets. Projects like

dplyr have further simplified expressing complex data manipulation tasks on data frames. SparkR

data frames present an API similar to dplyr and local R data frames that can scale to

large datasets using support for distributed computation in Spark. A data frame is a distributed

collection of data, organized into named columns. It is conceptually equivalent to a table in

a relational database, or a data frame in R. Both with optimizations under the hood.

Data frames can be constructed from a wide array of sources such as structured data files,

tables in Hive, external databases, or existing local R data frames. SparkR also supports

distributed machine learning using MLlib. As we can see in the diagram on the left hand

side, we have the R environment, with the Spark Context, the JVM, and the Java Spark

Context. And then on the right hand side, we have the task distributed across the cluster

so that we are not limited to single threading, or resourced on a single unit, a single machine.

We can use as many machines that are in the cluster. So, that raises a question, why would

you use SparkR? R, as we notice in the previous slide is restricted to single thread and the

amount of memory on a single machine. So using R on Big Data is very difficult. SparkR is

multi--threaded across many machines, as many machines as there are in the cluster, as well

as having access to the memory and all machines in that cluster. A typical example would be

where there's a large amount of initial data which needs cleaning, filtering, and aggregating

before the statistical analysis can be performed. This means reducing the volume of raw data

to a relevant subset, which can fit onto a single machine, where R can apply the statistical

learning model. This is very difficult, if not impossible in R. Once we have the set

of data we're going to work on, we need to train the model. Model training involves applying

a number of parameters to learn which parameter value works best. Most users want to do this

parameter tuning in parallel, and aggregate the parameters to find the best model for

the dataset. Performance in R is constrained by having to do this work on a single machine.

SparkR can do this across multiple nodes in a cluster, improving performance by several

orders of magnitude. When the raw data is very large, and the user wants to apply a

number of features to the whole dataset, and so a distributed machine learning algorithm

is needed. R cannot do this, but SparkR comes with a machine learning library and Spark

operates in a distributed environment, so large scaled machine learning is now possible

with R.



