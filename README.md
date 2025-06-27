# 📊 Understanding Public Inquiry Patterns Using 3-1-1 Dataset (City of Vancouver)

## 📘 Project Description
This project focuses on conducting a **descriptive analysis** of public service inquiries using the **3-1-1 Inquiry Volume dataset** from the City of Vancouver Open Data Portal. The analysis identifies monthly trends and patterns in city maintenance inquiries to help optimize resource allocation and staffing for the city's 3-1-1 contact center, specifically focusing on the **Real Estate & Facilities Management (REFM)** department.

---

## 🎯 Objective
To analyze public inquiry patterns to:
- Identify peak public inquiry periods.
- Support efficient resource planning and budgeting.
- Reveal long-term trends.
- Provide data-driven recommendations to enhance city services.

---

## 📂 Dataset

**Source**: City of Vancouver Open Data Portal  
**Key Features**:
- `Department`: Handling department for each inquiry  
- `Request Type`: Category (e.g., maintenance, inspection)  
- `Year and Month`: Time of inquiry  
- `Channel`: Inquiry method (phone, email, chat, social media)  
- `Number of Records`: Volume of inquiries  

📷 _Image Suggestion_: Screenshot of the raw CSV preview showing column structure

---

## 🔧 Methodology

### 🗂 Week 2 – Data Collection and Preparation
- Downloaded dataset and uploaded it to **Amazon S3** (`cityofvan-raw-spa`)
- Set up AWS infrastructure:
  - Created a **VPC** and **EC2 instance**
  - Defined folder path:  
    `CityOfVan/311InquiryVolume/Year=25/Quarter=Q2/Month=June/server=CVVS-Spa/CSV`

📷 _Image Suggestions_:  
- VPC setup  
- EC2 instance  
- S3 bucket structure  

---

### 🧪 Week 3 – Data Profiling and Cleaning

#### 🔍 Data Profiling
- Used **AWS Glue DataBrew** to profile 20,000 sample rows  
- Found 0 missing/null values; 100% valid data  
- 11 outliers in `Number_of_Records` retained for integrity

📷 _Image Suggestions_:  
- Data profiling summary  
- Column statistics chart  

#### 🧹 Data Cleaning
- Used Glue DataBrew recipes:
  - Removed whitespaces
  - Renamed columns (`Year Month → Year_Month`, `Number of Records → Number_of_Records`)
  - Reformatted `Year_Month` as `yyyy-MM`
  - Retained outliers

📷 _Image Suggestions_:  
- Data cleaning job  
- Cleaned CSV + PARQUET S3 outputs  

---

### 🧰 Week 4 – Data Cataloging and Analysis

#### 📚 Data Cataloging
- Created **AWS Glue Crawler** (`cityofvan-crawler-spa`)
- Registered schema to **Glue Data Catalog**

#### ⚙️ Visual ETL Pipeline
- Created pipeline in **Glue Studio**:
  - Split `Year_Month` into `Year` and `Month`
  - Simplified column names
  - Applied filters for REFM requests
  - Added timestamps and saved to S3

📷 _Image Suggestions_:  
- Glue Data Catalog  
- Glue ETL workflow  

#### 🔎 Analysis with Amazon Athena
- Executed SQL queries to answer:
  - Monthly average inquiries
  - Peak volume months
  - Yearly totals

📷 _Image Suggestions_: Athena query output table

---

## 📈 Descriptive Statistics
- **Average Monthly Volume**: Calculated via SQL
- **Peak Inquiry Month**: Identified from volume sorting
- **Yearly Trends**: Aggregated using `GROUP BY Year`

---

## 📊 Visual Insights (Optional)
Use **Power BI**, **Tableau**, or **Matplotlib** to generate:
- Line chart for monthly trends
- Bar chart of request channels
- Pie chart for request types

📷 _Image Suggestions_:  
- Time-series graph  
- Bar chart  
- Pie chart  

---

## 💡 Insights and Findings
- Peak inquiries observed in **summer and year-end** months
- **Email and phone** are dominant communication channels
- REFM sees periodic spikes → suggests need for dynamic staffing
- Long-term trends show slight fluctuation with consistent demand

---

## 🛠 Tools & Technologies Used
- **AWS S3** – Storage  
- **AWS Glue / DataBrew** – ETL and profiling  
- **AWS Glue Catalog** – Schema registration  
- **AWS Athena** – SQL analysis  
- **EC2, VPC** – Infrastructure  
- Optional: **Power BI / Tableau / Matplotlib** – Visualizations

---

## 📦 Deliverables
- ✅ Cleaned dataset (CSV and PARQUET)
- ✅ AWS ETL pipeline (Glue)
- ✅ SQL queries and insights (Athena)
- ✅ Full documentation and visualizations

📷 _Image Suggestions_: Final curated S3 outputs (user-friendly and system folders)

---

## 📌 Recommendations
- Allocate **additional staff** during peak periods.
- **Automate** common request types.
- Implement **predictive analytics** for future planning.
- Adjust communication methods based on **channel usage trends**.

---
