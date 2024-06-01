# Analytical Data Engineering Project

## Project Overview
This project involves typical Analytical Data Engineering tasks, such as data ingestion, transformation, and preparation for Business Intelligence (BI) usage. Data from various sources is ingested and loaded into a Snowflake data warehouse, where it undergoes a series of transformations. The BI tool Metabase connects to this data warehouse to generate dashboards and reports.

## Data Sources
### Data Background
The dataset used in this project originates from TPCDS, which focuses on Retail Sales. It includes sales records from websites and catalogs, inventory levels for each item within every warehouse, and 15 dimensional tables containing information about customers, warehouses, items, and more.

### Data Storage
- **RDS:** Most tables (except inventory) are stored in a Postgres database on AWS RDS. These tables are refreshed daily.
- **S3 Bucket:** The inventory table is stored in an S3 bucket, with a new file containing the most recent data deposited daily.

## Business Requirements
### Metabase Requirements
- Determine top and bottom-performing items of the week by sales amounts and quantities.
- Show items with low inventory levels weekly.
- Identify items with low stock levels, including the associated week and warehouse numbers, marked as "True".

### Snowflake Data Warehouse Requirements
To meet BI requirements, new tables are created in the Snowflake data warehouse:
- Consolidate customer-related tables into a single table.
- Establish a new weekly fact table with metrics such as sum of sales quantities, sales amounts, net profits, average daily sales quantities, inventory on hand, weeks of supply, and a low stock weekly flag.

## Project Infrastructure
- **Servers:** Multiple servers are created on AWS.
- **Tools:** Airbyte for data ingestion, Metabase for BI.
- **Cloud Data Warehouse:** Snowflake for data storage and transformation.
- **AWS Lambda:** Serverless service to ingest data from AWS S3.

## Project Steps

### Chapter 1: Data Ingestion

#### Section 1: Airbyte Setup
1. **Prerequisites:** AWS account, Ubuntu EC2 instance setup, Docker knowledge.
2. **Snowflake Setup:** Create database and schema, set up tables.
3. **EC2 Instances:** Launch and configure two EC2 instances for Airbyte and Metabase.
4. **Docker Installation:** Install Docker and Docker Compose on both instances.

#### Section 2: AWS Lambda Function
1. **Download Inventory Data:** Use Lambda to download `inventory.csv` from S3 and upload to Snowflake.
2. **Snowflake Integration:** Set up schema, file format, stage, and copy commands.
3. **Scheduling:** Schedule Lambda function to run daily at 2 am (Riyadh time).

#### Section 3: Airbyte Installation and Configuration
1. **Install Airbyte:** Use script to install Airbyte on EC2.
2. **Configure Airbyte:** Set up sources and destinations, configure connections and sync schedules.

### Chapter 2: Data Transformation

#### Data Modeling
1. **Explore Data:** Review tables in Snowflake, identify key metrics and dimensions.
2. **Create Data Model:** Develop a new data model in Snowflake with required metrics and consolidated customer dimensions.

#### ETL and Data Loading
1. **ETL Scripts:** Create scripts to populate data from raw tables to the new data model.
2. **Scheduling:** Use Snowflake tasks and stored procedures to automate daily and weekly data aggregation and loading.

### Chapter 3: Data Visualization
1. **Metabase Integration:** Connect Metabase to Snowflake and create dashboards and reports based on the data model.

## Detailed Instructions
### Setting Up Airbyte
1. **Launch EC2 Instances:** Create and configure two EC2 instances (t2.small for Metabase, t2.large for Airbyte).
2. **Install Docker and Docker Compose:** Follow provided commands to install Docker on both instances.
3. **Install Airbyte:** Download and run the Airbyte installation script on the Airbyte instance.
4. **Configure Sources and Destinations:** Set up Postgres as the source and Snowflake as the destination in Airbyte.

### Creating AWS Lambda Function
1. **Download Inventory Data:** Write Lambda function to download inventory data from S3 and upload to Snowflake.
2. **Create Snowflake Stages and Copy Commands:** Set up Snowflake stages, file formats, and copy commands to ingest data.
3. **Schedule Lambda Function:** Use AWS EventBridge to schedule the Lambda function to run daily.

### Data Transformation in Snowflake
1. **Create Data Model:** Develop the data model schema and tables in Snowflake.
2. **Write ETL Scripts:** Write SQL scripts to transform and load data from raw tables to the data model.
3. **Automate with Snowflake Tasks:** Create stored procedures and tasks to automate the ETL process.

### Data Visualization with Metabase
1. **Connect to Snowflake:** Configure Metabase to connect to the Snowflake data warehouse.
2. **Create Dashboards:** Develop dashboards and reports based on the transformed data in Snowflake.

## Conclusion
This project demonstrates the full lifecycle of data engineering, from data ingestion and transformation to visualization and reporting. By following the outlined steps, you can set up a robust data pipeline and generate insightful BI reports using Metabase.



