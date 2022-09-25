# EDA_HRA_Records_Spark_SQL

## Description

An HRA (Human Resources Analytics) data with over 5 million records is taken from SQL server using Pyodbc and then the dataframes / varialble are converted to Spark for further computations / EDA.

The idea is to extrapolate the existing data - in Jupyter Notebook / or any ide due to the fact that majority of times - the data on databases are mostly Raw data and we are not allowed to change / explore within.

### Dependencies

* You would require Pyodbc library ie.  **pip install pyodbc**
* For this project, I have used Jupyter Notebook - you can also use Google Colab.
* Please install Apache Spark (I have installed 3.2.2 version) from the below mentioned website:  https://spark.apache.org/downloads.html
* It's advised to have Java 8 or Java 11 for efficient use of Spark - the newer Java versions may or may not suppprt some features yet.
* You can refer to this article to set up spark env paths and other dependencies accordingly:  https://naomi-fridman.medium.com/install-pyspark-to-run-on-jupyter-notebook-on-windows-4ec2009de21f

<br><br>

## Getting Started

* 1) A table by the name "HRA_Records" is created with the mentioned excel file within "EMP_DETAILS" database in SQL Server.
* <br>
* ![pic1](https://user-images.githubusercontent.com/72039550/192141984-aa8778db-e093-48d1-a0ea-886673b4e2da.png)

<hr>

* 2) After necessary libraries are loaded, I have configured and named the app as "SparkODBC" in Spark as shown below
* <br>
![pic2](https://user-images.githubusercontent.com/72039550/192142048-caca28b1-a067-48a8-977e-1592228d8961.png)

<br>
<hr>
3) The following code show's how to connect to datasbe using pyodbc and then the concat values are saved to spark dataframe called "HRA_Records". To avoid / reduce memory issues that may occur, only 1 million records are being downloade din chunks so the memory si released after every download.
<br>
With the help of predefined Spark Schema, the data that is being saved in Spark Dataframe now has specific datatypes suited to its needs.
<br>

![pic3](https://user-images.githubusercontent.com/72039550/192142272-b574f94a-faca-431e-ae88-2ce3eb7c90ce.png)
<br><br>

## Executing program

* The data is currently in the form of dataframe and to query on the same I have used the function **CreateOrReplaceTempView** which creates a virtual table from the existing dataframe. Then we can perform functions / queries within **spark.sql()** that are pretty similar to that of **regular SQL**
<br>

![pic4](https://user-images.githubusercontent.com/72039550/192142446-0aaf8171-de86-4e4a-9ecd-a0d2e26ff6f6.png)


<br> For further queries used, kindly refer to the script attached in this repository.

<hr>

