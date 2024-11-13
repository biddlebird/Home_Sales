# Home Sales Analysis

This project performs analysis on home sales data using SparkSQL to generate key insights into home pricing trends. The analysis includes partitioning data, caching tables, and timing query performance, focusing on Spark's ability to handle and optimize large datasets.

## Project Structure

- **Home_Sales.ipynb**: Jupyter Notebook containing the code for data analysis, queries, caching, partitioning, and runtime analysis.
- **home_sales_revised.csv**: The CSV data file used for analysis (downloaded directly in the notebook from an AWS S3 bucket).

## Prerequisites

Ensure that the following are installed and configured:

1. **Java**: Spark requires Java. Install via:
   ```bash
   sudo apt install openjdk-11-jdk
   ```
2. **Apache Spark**: Download and install the latest Spark 3.x release:
   ```bash
   wget https://archive.apache.org/dist/spark/spark-3.4.0/spark-3.4.0-bin-hadoop3.tgz
   tar xvf spark-3.4.0-bin-hadoop3.tgz
   ```
3. **PySpark**: Install the Python package to run Spark within Jupyter:
   ```bash
   pip install pyspark
   ```
4. **FindSpark**: To locate the Spark installation in Jupyter:
   ```bash
   pip install findspark
   ```

## Data Analysis Steps

1. **Set up SparkSession**: Initialize a SparkSession for SparkSQL operations.

2. **Data Import**: The home sales data is read from a CSV file in an AWS S3 bucket into a Spark DataFrame.

3. **Create a Temporary Table**: A Spark temporary table, `home_sales`, is created for SQL queries.

4. **Analysis Queries**:
   - **Average Price of Four-Bedroom Houses Sold Per Year**: Calculates the average sale price of four-bedroom houses for each year, rounded to two decimal places.
   - **Average Price of Three-Bedroom, Three-Bathroom Homes Per Build Year**: Calculates the average price for houses with three bedrooms and three bathrooms, grouped by the year the home was built.
   - **Average Price of Homes with Specific Features**: Calculates the average price of homes with three bedrooms, three bathrooms, two floors, and over 2,000 square feet.
   - **Average Price by View Rating**: For homes with an average price above $350,000, calculates the average price per "view" rating and logs the runtime.

5. **Table Caching**: Caches the `home_sales` table to improve query performance and verifies the cache.

6. **Query Optimization and Runtime Comparison**:
   - Compares the runtime of the "Average Price by View Rating" query before and after caching.
   - Runs the same query on partitioned data stored in Parquet format, comparing performance across different storage and caching strategies.

7. **Partitioning and Uncaching**:
   - Partitions the dataset by the `date_built` column and stores the data in Parquet format.
   - Creates a temporary table from the partitioned Parquet data and runs the same query.
   - Uncaches the `home_sales` table and confirms that the table is no longer cached.

## Running the Notebook

1. Ensure the necessary files (`Home_Sales.ipynb` and `home_sales_revised.csv`) are in your working directory.
2. Start a Jupyter Notebook environment and open `Home_Sales.ipynb`.
3. Run each cell sequentially to conduct the analysis, ensuring all dependencies are installed.

## Results

The project provides insights into home sale trends, the impact of caching and partitioning on query performance, and demonstrates how SparkSQL can be used to optimize operations on large datasets.
