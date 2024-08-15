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

![image](https://github.com/user-attachments/assets/49974130-7252-4748-878a-51f563e69925)

#### Dimension tables:

<img width="307" alt="image" src="https://github.com/user-attachments/assets/4e6fdac1-dd31-44fd-a45b-5dfea48aa508">


#### Fact table:

<img width="527" alt="image" src="https://github.com/user-attachments/assets/64f8d5bf-2f19-4588-a5bb-ecf7b22ded29">

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
## II. Star schema implementation
### 1. Star schema implementation
### 2. Staging area
#### a. Data cleaning
#### b. Data transforming
#### c. Data loading into star schema (integrating Slow changing dimension type 2)
