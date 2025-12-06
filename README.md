# AWS Athena Project: Querying Multiple CSV Datasets

## TL;DR:

First hands-on AWS project using **S3, Glue, and Athena** to ingest, organize, and query multiple CSV datasets. Demonstrates cloud data management and analytics skills with serverless AWS services.

**Key Highlights:**

* Serverless data pipeline using S3 → Glue → Athena

* Automatic schema detection with Glue Crawlers

* Query large CSV datasets directly in Athena without managing servers

* Hands-on experience with IAM roles, permissions, and query result management

## Table of Contents

1. [Cost](#cost)

2. [Project Goal](#project-goal)

3. [Datasets](#datasets)

4. [Architecture](#architecture)

5. [Setup](#setup)

    * [S3](#s3)

    * [Glue](#glue)

    * [Athena](#athena)

6. [Conclusion](#conclusion)

7. [Next Step/Extensions](#next-stepsextensions)

8. [Acknowledgments](#acknowledgments)

## Cost

All services used in this project are covered under the [AWS Free Tier](https://aws.amazon.com/free/).

**PSA:** Make sure to delete everything to avoid incurring costs if you leave these services running.

## Project Goal

Demonstrate the ability to ingest, structure, and query multiple CSV datasets in AWS using serverless services, showcasing cloud data management and analytics skills.

## Datasets

**Source:**[Datablist](https://www.datablist.com/learn/csv/download-sample-csv-files#products-dataset)

**Size:**

* 100,000 Customers
  
*  100,000 Leads
  
*  10,000 Products

**CSV Files:**

* [Customers CSV](https://drive.google.com/uc?id=1N1xoxgcw2K3d-49tlchXAWw4wuxLj7EV&export=download)

* [Leads CSV](https://drive.google.com/uc?id=1mCFMwc_Y0nU8G99-AUznqqBvh6t2Kg8B&export=download)

* [Products CSV](https://drive.google.com/uc?id=1BE-dfkrb6oyLKDuqXAq2fDYMkDz2f9hM&export=download)

## Architecture

<img width="1297" height="748" alt="image" src="https://github.com/user-attachments/assets/29b56848-6b93-4724-8f27-9e46e4d1c1d7" />

**Pipeline Overview:**

1. CSV datasets uploaded to S3 buckets

2. Glue Crawlers catalog datasets automatically

3. Data queried in Athena

## Setup

### S3

I created two buckets:

* **companyx-athena:** stores query results (Athena output)

* **companyx-aws-analytics:** stores source CSV datasets, organized in folders

<img width="1263" height="369" alt="image" src="https://github.com/user-attachments/assets/c28055cf-4238-4ceb-b897-38f3c633a78d" />

**Folders:**

* customers/
  
* leads/
  
* products/
<img width="1911" height="618" alt="image" src="https://github.com/user-attachments/assets/42239b40-05ef-4dfa-8c9d-76cead855c93" />


**CSV files in folders:**

**Customers CSV**
<img width="1910" height="526" alt="image" src="https://github.com/user-attachments/assets/af3cf29f-02bc-4ae0-a73a-c5edc5d2fe42" />

**Leads CSV**
<img width="1899" height="544" alt="image" src="https://github.com/user-attachments/assets/8036ce1d-7991-4b8a-9733-e93d9c6a24f6" />

**Products CSV**
<img width="1893" height="551" alt="image" src="https://github.com/user-attachments/assets/3960f037-f925-4c20-b8d7-86b779fd925b" />

Next, I cataloged these CSV files in AWS Glue.

### GLUE

**Step 1: IAM Role**

* Role: companyx-etl-role

* Permissions: AdministratorAccess
  
* Trusted entity: Glue service
<img width="1903" height="718" alt="image" src="https://github.com/user-attachments/assets/1ae9ba4d-3a15-4469-ac60-7ddc18910712" />

**Step 2: Glue Database**

* Database: companyx_db

* Purpose: Acts as catalog for datasets
<img width="1919" height="213" alt="image" src="https://github.com/user-attachments/assets/a50d08d1-78c0-4463-b43f-1eaecad2f93f" />

**Step 3: Crawlers**

* Crawlers: customers-raw, leads-raw, products-raw

* Auto-detect schema enabled

* Run crawlers → populate Glue Data Catalog
<img width="1914" height="397" alt="image" src="https://github.com/user-attachments/assets/6036ab65-6d48-4759-90d7-f6df07a62460" />

**Crawler Results:**

* **Customers-raw**
<img width="1906" height="803" alt="image" src="https://github.com/user-attachments/assets/a29246d3-6b85-49d4-aa0e-e1d3377130f7" />

* **Leads-raw**
<img width="1898" height="799" alt="image" src="https://github.com/user-attachments/assets/e45a0a86-3854-4b35-b586-15e64b91647d" />

* **Products-raw**
<img width="1898" height="805" alt="image" src="https://github.com/user-attachments/assets/1d87a780-3639-4768-b734-05da76cb5877" />

**Notes:**

* Tables reflect CSV columns and data types

* Glue automatically inferred column names and types
<img width="1918" height="401" alt="image" src="https://github.com/user-attachments/assets/7c09e91b-1577-4cd5-8126-f43b3073319c" />


With the tables now in the Glue Data Catalog, I could query them directly in Athena.

### Athena


**Step 1: Set Query Result Location**

* All query outputs stored in companyx-athena bucket
<img width="1912" height="455" alt="image" src="https://github.com/user-attachments/assets/9d819fd7-d2c6-4f21-b3d7-c7d07d482c95" />

**Step 2: Query Tables**

* Tables visible in Athena from Glue catalog

* Limit set to 20 rows for quick verification
<img width="1899" height="797" alt="image" src="https://github.com/user-attachments/assets/984a9f3a-d7e9-46d1-b195-33e7a40ec647" />

**Query Results:**

* **Customers Query Results** 
<img width="1881" height="738" alt="image" src="https://github.com/user-attachments/assets/16c5128e-f489-4c60-9f16-d6cb8fc6081a" />

* **Leads Query Results**
<img width="1873" height="779" alt="image" src="https://github.com/user-attachments/assets/0cfd0921-e138-468b-b5e2-176e5e707d58" />

* **Products Query Results**
<img width="1888" height="786" alt="image" src="https://github.com/user-attachments/assets/bd994ce0-ef88-4ab8-9fad-1e2a24dc7fee" />

**Notes:**

* Datasets now queryable for aggregations, joins, and analytics directly in the cloud

## Conclusion

This project demonstrates how to ingest, catalog, and query multiple CSV datasets in AWS using serverless services.

**Skills gained:**

* Organizing and storing datasets in S3

* Creating IAM roles and managing permissions

* Cataloging data with Glue and inferring schema automatically

* Querying and exploring datasets in Athena

## Next Steps/Extensions

* Automate Glue crawlers with **CloudWatch** for scheduled updates

* Perform transformations with **Glue ETL jobs**

* Visualize Athena query results with **QuickSight** or **Python notebooks**

* Partition large datasets in S3 to improve query performance

## Acknowledgments

Datasets sourced from [Datablist](https://www.datablist.com/learn/csv/download-sample-csv-files#products-dataset)
