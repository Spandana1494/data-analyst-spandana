# 📊 Understanding Public Inquiry Patterns Using 3-1-1 Dataset (City of Vancouver)

## 📘 Project Description
This project presents a comprehensive descriptive analysis of the 3-1-1 Inquiry Volume dataset sourced from the City of Vancouver's Open Data Portal. The analysis focuses on understanding how public inquiries related to city services are distributed over time, by department, type, and communication channel. The study zeroes in on inquiries managed by the **Real Estate & Facilities Management (REFM)** department to inform staffing, resource allocation, and service delivery planning.

The 3-1-1 system serves as a vital communication bridge between citizens and the municipal government. This analysis enables data-driven decisions that enhance the city's operational efficiency and public service responsiveness.

---

## 🌟 Objective
The primary objective is to uncover key patterns and trends in public inquiries to:
- Determine peak periods of public demand.
- Support resource allocation and workforce planning.
- Improve city responsiveness by forecasting trends.
- Establish a basis for future predictive models and automated decision-making.

---

## 📂 Dataset Overview

**Source**: City of Vancouver Open Data Portal  

**Attributes Included**:
- `Department`: The city division responsible for handling the request.
- `Request Type`: The nature of the inquiry (e.g., maintenance, inspection).
- `Year and Month`: Timestamp when the inquiry was logged.
- `Channel`: Method through which the inquiry was made (e.g., phone, email).
- `Number of Records`: Count of inquiries received in a given period.

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/csv.png)
**Figure-1**: _Sample preview of raw 3-1-1 dataset showing major columns and sample data_

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/draw_io.png)
**Figure-2**: _Draw.io file_

---

## 🛠️ Methodology

### 🗂 Week 2 – Data Collection and Preparation
- **Infrastructure Setup**: AWS infrastructure was established using VPC and EC2 to securely manage data flow.
- **S3 Bucket Creation**: An S3 bucket named `cityofvan-raw-spa` was created to store raw data.
- **Folder Structure**: A logical folder structure was implemented in the bucket for easy data retrieval and pipeline integration.
- **Data Upload**: The structured CSV file was uploaded, enabling subsequent steps like profiling and transformation.

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/VPC_configuration.png)
**Figure-3**: _VPC Configuration_

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/Launching_VPC.png)
**Figure-4**: _Launching VPC_

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/S3_raw_bucket.png)
**Figure-5**: _S3 Raw Bucket_

---

### 🔬 Week 3 – Data Profiling and Cleaning

#### Data Profiling
- Conducted using **AWS Glue DataBrew**.
- A sample of 20,000 rows was analyzed.
- Key findings:
  - No missing or null values.
  - All fields correctly typed and categorized.
  - 11 outliers in `Number_of_Records` retained to maintain data integrity.

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/data_profiling.png)
**Figure-6**: _data_profiling_

#### Data Cleaning
- **Transformations Applied**:
  - Whitespace removed from textual fields.
  - Columns renamed for compatibility and clarity.
  - `Year_Month` reformatted to `yyyy-MM`.
  - Retained valid outliers to reflect real public activity spikes or declines.

- **Outputs**:
  - Cleaned CSV (user-friendly)
  - Cleaned PARQUET (system-friendly for querying)

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/receipe_job.png)
**Figure-7**: _Job-Receipe_

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/cleaned_csv.png)
**Figure-8**: _cleaned_csv_

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/cleaned_parquet.png)
**Figure-9**: _cleaned_parquet_

---

### 📃 Week 4 – Data Cataloging and Analysis

#### Data Cataloging
- Used **AWS Glue Crawler** to register the cleaned dataset into a centralized **Glue Data Catalog**.
- Schema including columns, types, and partitions was automatically generated.
- Enabled discoverability and consistency in querying.

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/data_catalog.png)
**Figure-10**: _data_catalog_  

#### Visual ETL Pipeline
- Built using **AWS Glue Studio**.
- Key transformations:
  - Split `Year_Month` into separate `Year` and `Month` fields.
  - Renamed columns (`Number_of_Records → num_records`).
  - Applied filters to isolate REFM-specific requests.
  - Converted year/month into integers for sorting.
  - Appended a processing timestamp.

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/visual-etl-pipeline.png)
**Figure-11**: _visual-etl-pipeline_

#### Athena Query Execution
- SQL queries executed using **Amazon Athena**:
  - Calculated average monthly inquiry volume.
  - Identified the highest volume month.
  - Determined total annual requests.
  - Pinpointed periods with minimum and maximum demand.

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/athena-query-results.png)
**Figure-12**: _athena-query-results_

---

## 📊 Descriptive Analysis Results

- **Total Inquiries by Year**: Revealed the workload handled annually.
- **Average Monthly Volume**: Enabled staffing models based on mean demand.
- **Peak Months**: Highlighted the need for extra support during summer and year-end.
- **Channel Analysis**: Showed phone and email as dominant channels.
- **Request Type and Department**: Validated the focus on REFM maintenance inquiries.

---

## 📄 Insights and Findings

- **High-Demand Months**: Typically occurred in June, July, and December.
- **Department Load**: REFM received considerable volume in maintenance-type requests.
- **Stable Trends**: General inquiry volume was consistent year-to-year, supporting long-term planning.
- **Outliers Valid**: Months with exceptionally low/high requests reflect realistic operational cycles and holidays.

---

## 🚀 Recommendations

- **Dynamic Staffing**: Allocate extra staff during months with high volume.
- **Automation**: Use chatbots or auto-responders to handle frequent inquiries.
- **Predictive Planning**: Implement forecasting tools using historical trends.
- **Channel Optimization**: Streamline services around preferred communication channels.

---

## 🛠️ Tools and Technologies Used

- **Cloud Infrastructure**: AWS S3, EC2, VPC  
- **ETL and Cleaning**: AWS Glue, Glue DataBrew  
- **Querying and Analytics**: AWS Glue Catalog, Amazon Athena  
- **Storage Formats**: CSV (user-readable), PARQUET (machine-readable)

---

## 📦 Deliverables

- ✅ Cleaned and structured dataset in S3 (CSV + PARQUET)  
- ✅ AWS Glue visual ETL pipeline  
- ✅ SQL queries and results using Athena  
- ✅ Data catalog with searchable schema  
- ✅ Documentation and detailed project report

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/s3_c_u.png)
**Figure-13**: _s3-curated-user_

![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/s3-curated-system.png)
**Figure-14**: _s3-curated-system_

---

# Module 1: AWS Deployment and Service Models

## Case Study 1: Traditional vs. Cloud Computing

This case study examines the architectural, security, and operational contrasts between traditional computing and cloud-based computing using AWS in a financial operations setting.

In the traditional model, data is stored in on-site servers, providing tight physical control but poor global accessibility. Data access is limited to on-premises networks or VPNs, making it less efficient in distributed work environments. Security in this model heavily relies on physical barriers and internal governance policies.

In contrast, AWS cloud computing decentralizes data while maintaining security through identity-based access and encryption protocols. IAM (Identity and Access Management) allows finely-tuned access control. AWS provides encryption both at rest and in transit, bolstering privacy.

Key Observations:

- Location: Traditional systems tie data to one physical place; AWS uses availability zones and regions.
- Access: Traditional = limited to local/VPN; Cloud = global, secure, role-based access.
- Security: Traditional relies on hardware; AWS provides encryption, IAM, and policies.

Conclusion: For finance operations requiring flexibility, availability, and compliance, AWS cloud infrastructure delivers significant operational advantages.

**Result**: _case_study_1_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_1.png)

## Case Study 2: Cloud Deployment Models

This case study explores how University Canada West (UCW) implements different AWS deployment models—Private, Public, Hybrid, and Multi-cloud—to support financial operations securely and efficiently.

Private Cloud is used for confidential datasets, ensuring control and compliance by maintaining local isolation.

Public Cloud enables quick scaling and cost efficiency for general-purpose financial operations.

Hybrid Cloud integrates traditional and cloud environments to gradually transition legacy systems.

Multi-Cloud leverages services from multiple providers, increasing system resilience and flexibility.

Conclusion: UCW's approach demonstrates how tailoring deployment models enhances both data security and service agility.

**Result**: _case_study_2_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_2.png)

## Case Study 3: Cloud Service Models (IaaS, PaaS, SaaS)

This study analyzes the use of AWS's core service models at UCW to address different requirements of the finance department.

IaaS (e.g., EC2) gives full infrastructure control, suitable for hosting secure apps.

PaaS (e.g., Elastic Beanstalk) abstracts the OS and infrastructure, allowing quick application deployment.

SaaS (e.g., QuickSight) offers plug-and-play financial software for fast analytics.

Conclusion: Each model represents a tradeoff between control and convenience. UCW uses all three to balance flexibility, scalability, and data governance.

**Result**: _case_study_3_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_3.png)
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_3_2.png)

---

# Module 2: AWS Cost Analysis

## Case Study 4: Total Cost of Ownership (TCO)

Delaware North transitioned from a legacy infrastructure to AWS to reduce costs and increase IT agility.

The phased migration approach included:

- Piloting 50 non-critical web functions.
- Utilizing EC2 Reserved Instances to reduce operational expenses.
- Implementing AWS Systems Manager to automate patching.
- Centralizing billing via AWS Organizations.

Conclusion: TCO reduction was achieved by reducing maintenance, hardware, and staffing costs. Migration helped Delaware North enhance governance and scalability.

**Result**: _case_study_4_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_4.png)

## Case Study 5: AWS Pricing Calculator

UCW's finance team used AWS Pricing Calculator to estimate costs for building a cloud-based data pipeline.

Pipeline services included:

- Amazon S3 (storage)
- AWS Glue (ETL jobs)
- Amazon Athena (data analysis)

The estimate factored in:

- Usage-based pricing
- Free Tier offerings
- Reserved capacity for cost savings

Conclusion: This exercise enabled realistic budget forecasts while encouraging efficient cloud usage.

**Result**: _case_study_5_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_5.png)

---

# Module 3: AWS Global Infrastructure

## Case Study 7: Global Architecture for Finance Operations

This case demonstrates how UCW improved student financial data access through a globally distributed AWS setup.

Regions used: North Virginia and Oregon

Services: EC2, EBS for core workloads, and CloudFront for caching

Added TLS security and signed URLs

Conclusion: Students experienced faster access times and better service availability with minimal latency.

**Result**: _case_study_7_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_7.png)
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_7_2.png)

---

# Module 4: AWS Identity and Access Management (IAM)

## Case Study 8: AWS Shared Responsibility Model

The study outlines which responsibilities lie with AWS and which lie with the user:

AWS: Physical infrastructure, network security

User: OS patches, firewall configs, encryption, IAM policies

Conclusion: Security success depends on the user's ability to configure and monitor their part of the stack.

**Result**: _case_study_8_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_8.png)

## Case Study 9: IAM Practice Lab

This hands-on lab involved:

- Creating users, groups, and policies
- Applying the principle of least privilege
- Testing real-time access

Conclusion: The exercise demonstrated how IAM enforces structured, secure access based on roles.

**Result**: _case_study_9_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_9.png)

---

# Module 5: AWS VPC

## Case Study 10: Build Your VPC Lab

This lab entailed creating a fully functional VPC with high availability:

- Public and Private Subnets across 2 AZs
- Configured Internet Gateway and NAT Gateway
- Launched EC2 with HTTP access via Security Groups

Conclusion: The lab highlighted how VPCs isolate environments while still enabling secure internet access.

**Result**: _case_study_10_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_10.png)

---

# Module 6: AWS Lambda

## Case Study 11: Lambda Function Automation

A Lambda function was built to stop EC2 instances on a schedule:

- Runtime: Python 3.11
- Scheduled via Amazon EventBridge (every minute)
- IAM Role defined minimal access needed

Conclusion: Demonstrated serverless cost efficiency and automated resource management.

**Result**: _case_study_11_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_11.png)

---

# Module 7: AWS EBS

## Case Study 12: Working with Amazon EBS

In this lab, EBS was tested for reliability and backup:

- Created and mounted EBS volumes
- Made snapshots and restored data
- Demonstrated persistence across reboots

Conclusion: EBS volumes offer durable, scalable storage crucial for high-availability applications.

**Result**: _case_study_12_
![Alt text](https://raw.githubusercontent.com/Spandana1494/data-analyst-spandana/main/images/case_study_12.png)
