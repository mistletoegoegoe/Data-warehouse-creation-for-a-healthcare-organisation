# Data-warehouse-creation-for-a-healthcare-organisation
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
| Table name  | Attribute name    | Data type    |
|-------------|-------------------|--------------|
| Time        | Time_id           | Int (PK)     |
|             | Year              | Int          |
|             | Month             | Int          |
| Care_centre | Care_centre_id_sq | Int (PK)     |
|             | Care_centre_name  | Varchar (50) |
| Ward        | Ward_id_sq        | Int (PK)     |
|             | Ward_name         | Varchar (50) |
#### Fact table:
| Table Name         | Attribute Name       | Data Type | Keys        | Measure                                        |
|--------------------|----------------------|-----------|-------------|------------------------------------------------|
| Bed_occupancy_FACT | Serial_no            | Int       | Primary Key | Unique serial number                           |
|                    | Time_id              | Int       | Foreign Key | Refers to Time table                           |
|                    | Care_centre_id_sq    | Int       | Foreign Key | Refers to Care_centre table                    |
|                    | Ward_id_sq           | Int       | Foreign Key | Refers to Ward table                           |
|                    | AVG_available_bed    | Real      | Non key     | Records average available beds                 |
|                    | AVG_occupied_bed     | Real      | Non key     | Records average occupied beds                  |
|                    | AVG_occupancy_rate   | Real      | Non key     | Records bed occupancy rate                     |
|                    | AVG_waiting_time_WYR | Real      | Non key     | Records average waiting time in WYR home cares |
### 5. Extract, Transform and Load process
## II. Star schema implementation
### 1. Star schema implementation
### 2. Staging area
#### a. Data cleaning
#### b. Data transforming
#### c. Data loading into star schema (integrating Slow changing dimension type 2)
