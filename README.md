# Data_warehouse_creation_for_a_healthcare_organisation
## I. Star schema design
### 1. Case study
North and West Yorkshire CCG is seeking a health and social care system that integrates data from care homes and social care services. Leeds City Council operates six care homes providing extended support for elderly patients. 
The system aims to assess care home effectiveness, review recovery periods and bed occupancy, and facilitate collaboration between doctors and social care services. 
Due to the case study, some requirements and characteristics of integrated data system can be deduced as below: 
-	Centralised data system works with data from many sources 
-	The dataset of care homes and social services care grows minutes by minutes due to the increasing in the number and information of patients, thus, this dataset is very huge
-	The durability of data system is important, as this is a long-term project which will last many years and update continuously.
  
### 2. Identify stakeholders, main objective and reports
From the objective of the data system that needs to be built, many objectives and related stakeholders can be chosen to deliver information and insights. However, this project focuses on:  
-	**Objective**: Bed occupancy assessment
-	**Stakeholder**: Care home managers

For the KPI defined above, there are some reports can be made as below to provide information and insights to hospital managers to assess bed occupancy: 
-	Average number of available and occupied beds per month per year
-	The highest/lowest number of occupied beds per ward per care home per year
-	Average occupancy rate per care home per year (this is for managers to know that they are running enough/exceeding bed or not)
-	The Average waiting time of patients (between booking date and admission date) in WYR home care
  
### 3. Solution proposal
With the objective to integrate data from care homes and social service, and the reports that had to be made, a data warehouse is needed. 
As the KPI, stakeholder and reports that are figured out above is the direction to determine which tables had to be included. They are time, care home, and ward dimension.  The general centralised database solution is proposed as follows: 

The tables care_home, ward, time (dimension tables) will connect with one center table. That centered table can extract data from dimension table to calculate or aggregate and retrieve the required reports. 

To build this data warehouse, the data is organized in some concepts: star schema, snowflake schema, and fact constellations (Karmani, 2020). All types of schemas can generate required reports. Although, snowflake and fact constellations schema can eliminate data redundancy which may happen in star schema, they are far more complex in query and time execution as well as the size of data warehouse (Karmani, 2020). Thus, star scheme might be a reasonable pick. 

### 4. Star schema and data dictionary
In the previous section, reports to support objectives of North and West Yorkshire CCG are identified. From those, star schema is designed with dimensions (time, ward, care home) and a fact table. Details of them are shown in tables below: 

![image](https://github.com/user-attachments/assets/9149d9ff-2a57-4e98-befe-6f0be711cb02)

**Surrogate keys: **

In the star schema, the sequence (care_centre_id_sq and ward_id_sq) are used as surrogate keys instead of the natural keys (care_centre_id and ward_id). The reason for this is that in two datasets for care_centre (NYR and WYR), the care_centre_id (primary key in NYR_care_centre table) and care_id (primary key in WYR_care_centre table) are not unique. 

**Slowly changing dimension type 2:

**Moreover, applying the SCD type 2 may require more than one row for a subject such as one ward or one care centre. However, it is the requirement that there is an identifier to maintain the uniqueness among all the records which ward_id or care_centre_id cannot meet. 

Thus, it is necessary to have a surrogate key after combining these two datasets in one and implement the SCD.  The reason for Ward_dim table is similar to Care_Centre_dim. 


#### Data dictionary for each table: 

Time_dim table:


<img width="721" alt="image" src="https://github.com/user-attachments/assets/d20caf50-44b4-4135-baa0-1282e848b418">


Care_centre_Dim table:


<img width="720" alt="image" src="https://github.com/user-attachments/assets/0c761a07-ce7e-4032-8240-7e53a929f4a1">


Ward_Dim table:


<img width="721" alt="image" src="https://github.com/user-attachments/assets/fecf0a53-701d-4b14-a0b8-09b2bdc7ab7e">


Bed_occupancy_Fact table:


<img width="719" alt="image" src="https://github.com/user-attachments/assets/911f5e80-8245-4d1b-8a88-aae490c289c4">


### 5. Extract, Transform and Load process
After identifying 3 necessary dimension tables that links to one fact table as star scheme design above, the next issue is how to extract data from original dataset and load them into dim table and then populate fact table.

To deal perfectly with this issue, the process of Extract, transform and load (ETL) is applied to not only extract the required data from original dataset and load them into dimension tables but also includes some steps to clean and transform raw data to ensure the data integrity, quality and consistency in format between data in two original table (WYR and NYR). 

<img width="626" alt="image" src="https://github.com/user-attachments/assets/69f7d334-5321-411e-aebe-d24759a911ed">


## II. Star schema implementation
### 1. Star schema implementation

### 2. Staging area
#### a. Data cleaning
#### b. Data transforming
#### c. Data loading into star schema (integrating Slow changing dimension type 2)
