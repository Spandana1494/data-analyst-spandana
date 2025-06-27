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



# AWS Case Studies Summary

## Module 1: AWS Deployment and Service Models

### Case Study 1: Traditional vs. Cloud Computing
**Scenario:** Comparison of financial operations infrastructure  
**Key Points:**
- Traditional: On-site servers, VPN access, physical security  
- AWS Cloud: IAM access controls, global availability, encryption  
**Conclusion:** AWS provides better flexibility and compliance for finance operations  

### Case Study 2: Cloud Deployment Models
**Organization:** University Canada West (UCW)  
**Models Implemented:**
1. Private Cloud: For confidential data isolation  
2. Public Cloud: Scalable general operations  
3. Hybrid Cloud: Legacy system transition  
4. Multi-Cloud: Resilience through provider diversity  
**Conclusion:** Tailored deployments enhance security and agility  

### Case Study 3: Cloud Service Models
**UCW Finance Department Use Cases:**
- **IaaS (EC2):** Full infrastructure control  
- **PaaS (Elastic Beanstalk):** Rapid app deployment  
- **SaaS (QuickSight):** Instant analytics tools  
**Conclusion:** Balanced approach optimizes control vs convenience  

## Module 2: AWS Cost Analysis

### Case Study 4: Total Cost of Ownership (TCO)
**Company:** Delaware North  
**Migration Strategy:**
- Piloted 50 non-critical functions  
- Used EC2 Reserved Instances  
- Automated patching with Systems Manager  
- Centralized billing via AWS Organizations  
**Outcome:** Reduced maintenance/hardware costs by 60%  

### Case Study 5: AWS Pricing Calculator
**Project:** UCW Data Pipeline Cost Estimation  
**Services Analyzed:**
- S3 Storage  
- Glue ETL Jobs  
- Athena Analytics  
**Key Factors:** Usage-based pricing, Free Tier, Reserved Capacity  
**Result:** Accurate budget forecasting achieved  

## Module 3: AWS Global Infrastructure

### Case Study 7: Global Architecture
**UCW Student Finance System:**
- **Regions:** N. Virginia & Oregon  
- **Services:** EC2, EBS, CloudFront  
- **Security:** TLS + Signed URLs  
**Improvement:** 40% faster student access globally  

## Module 4: AWS IAM

### Case Study 8: Shared Responsibility Model
**Division:**
- **AWS:** Physical infrastructure/network  
- **User:** OS patches, IAM, encryption  
**Critical Success Factor:** Proper user configuration  

### Case Study 9: IAM Practice Lab
**Activities:**
- Created granular user groups  
- Implemented least privilege policies  
- Tested real-world access scenarios  
**Outcome:** Demonstrated role-based security effectiveness  

## Module 5: AWS VPC

### Case Study 10: VPC Lab
**Built:**
- Public/Private subnets across 2 AZs  
- Internet & NAT Gateways  
- EC2 with HTTP access  
**Takeaway:** Secure isolation with controlled internet access  

## Module 6: AWS Lambda

### Case Study 11: Serverless Automation
**Function:** Scheduled EC2 stopper  
**Components:**
- Python 3.11 runtime  
- EventBridge triggers (minutely)  
- Minimal IAM permissions  
**Result:** 80% cost reduction for non-production instances  

## Module 7: AWS EBS

### Case Study 12: EBS Lab
**Tests Performed:**
- Volume creation/mounting  
- Snapshot backups  
- Cross-reboot persistence  
**Conclusion:** High-availability storage solution verified  
