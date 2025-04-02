# Azure Olympic Project

The **Azure Olympic Project** is a data pipeline built using **Azure Data Factory (ADF)**, **Azure Data Lake**, and **Databricks**. It processes and transforms Olympic-related datasets, organizing them into three layers: **Bronze**, **Silver**, and **Gold**. Initially, raw data is stored in **Parquet** format in the Bronze layer. Then, using **Databricks**, the data undergoes transformations and is loaded into the **Silver** layer as Delta tables. For loading data from the Silver to Gold layer, the project uses **Delta Live Tables (DLT)** and **Change Data Feed (CDF)** for efficient processing. The project also uses **Unity Catalog** for managing and securing the data within Databricks.

## Tools Used

- Azure Data Factory (ADF)
- Databricks
- Unity Catalog
- Delta Lake
- Delta Live Tables
- Apache Spark
- PySpark
- Azure DevOps for CI/CD

## Data Ingestion

The data ingestion process involves two main sources: **GitHub** and **Azure Data Lake**, which both load data into the **Bronze Layer** in **Azure Data Lake**. The process is divided into two pipelines: one for ingesting data from GitHub and another for ingesting data from the Data Lake.

### Steps Involved:
1. **Create Linked Services**:
   - Created **Linked Services** in **Azure Data Factory (ADF)** to connect to both GitHub and Azure Data Lake.

2. **Create Datasets**:
   - Created **datasets** to define the structure and location of the data in both sources (GitHub and Data Lake).

3. **Pipeline 1: GitHub to Bronze Layer**:
   - Used **HTTP Activity** to retrieve data from GitHub.
   - Created a pipeline that connects to GitHub and ingests the data into the **Bronze Layer** in **Parquet** format.

## Bronze to Silver Layer

The **Bronze to Silver** process involves reading raw data from the **Bronze Layer**, transforming the data using **Spark** in **Databricks**, and then loading it into the **Silver Layer** in **Delta** format. This transformation is carried out using two separate notebooks:

### Notebooks Used:

1. **Notebook 1: parameter_for_silvernb.ipynb (Parameterized Notebook)**
   - This notebook is used to read data from the **Bronze Layer** and process it dynamically based on parameters.
   - **Files read**: Two files are loaded dynamically using **parameterized input**.
   
```python
# notebook 1: parameter_for_silvernb.ipynb

# Define input parameters
dbutils.widgets.text('source_container','')
dbutils.widgets.text('sink_container','')
dbutils.widgets.text('source_folder','')
```

## Silver to Gold Layer

The **Silver to Gold** process involves using **Delta Live Tables (DLT)** to transform and curate the data from the **Silver Layer** and load it into the **Gold Layer**. **DLT** is used to simplify the pipeline and ensure high-quality, reliable, and consistent data for downstream use.

### Steps Involved:

1. **Delta Live Tables (DLT)**:
   - **DLT** allows the transformation of data in an automated and declarative manner.
   - The data from the **Silver Layer** is transformed and loaded into the **Gold Layer** for business-ready, curated data.

2. **Curated Data Transformation**:
   - The transformations applied in **DLT** help refine the data further, making it ready for reporting and analytics.

3. **Loading to Gold Schema**:
   - After applying the transformations, the curated data is written into the **Gold Layer** in **Delta** format.


