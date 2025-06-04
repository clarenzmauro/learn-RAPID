Apache Spark and PySpark
- Apache Spark:
    - a fast and general-purpose cluster computing system.
    - designed for big data processing and analytics.
    - can run in various environments like Kubernetes.
    - provides high-level APIs in Java, Scala, Python (PySpark), and R.
    - Key features: in-memory processing, fault tolerance, scalability.

- PySpark
    - the Python API for Sparl
    - allows you to leverage the power of Spark using Python
    - you can write Spark apps using Python code, which then get executed on the Spark cluster.

- core spark concepts:
    - RDD (Resilient Distributed Dataset): the original core abstraction in Spark. It's an immutable, distributed collection of objects. 
    - DataFrame: a distributed collection of data organized into named columns. It's conceptually equivalent to a table in a relational database or a data frame in R/pandas, but with optimizations for distributed processing.
    - SparkSession: the entry point to Spark functionality. You create a SparkSession object to interact with Spark.

setting up a local pyspark env
you can run pyspark in local mode on your machine without needing a full spark cluster.

1. Java Development Kit (JDK): Spark runs on the Java Virtual Machine so you need a JDK installed.
2. Install PySpark
    - best to do this in a dedicated Python virtual environment.

basic DataFrame operations
- reading data
- show(): displays the first few rows of a DataFrame
- printSchema(): shows the DataFrame's schema
- select(): select specific columns
- filter() or where(): filter rows based on a condition
- groupBy(): groups rows based on some criteria
- aggregations like count(), avg(), sum(), min(), max()

mini project
1. create dummy submission data
2. create a pyspark script
3. run the pyspark script
