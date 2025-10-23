# Excel_Data_Analysis_Project

## Introduction

## Excel Skills Used
- Pivot Tables
- Pivot Charts
- Power Query
- Power Pivot
- DAX

## Dataset
The dataset used for this project contains real-world data science job information from 2023.

It has detailed information on:
- Job Titles
- Job Countries
- Job Schedule Types
- Job Posted Dates
- Job Salaries
- Skills
  
## Questions to Analyse
1. Do more skills get you a higher paying job?
2. What's the median salary for data jobs when compared to the US and countries outside the US?
3. What are the top skills for data jobs?
4. What's the pay for the top 10 skills?
   
## 1. Do more skills get you a higher paying job?
## Power Query: ETL

**Extract**
- I used Power Query to extract the original dataset to create two queries
- The first query had all the data job information from the original dataset with an index column (job_id).
- The second query listed the skills for each job_id. The second query only has two columns, the job_id and the skills column, we need the job_id with the skills column is to ensure when unpivoting the skills they stay under the same unique ID.
<img width="547" height="384" alt="image" src="https://github.com/user-attachments/assets/8e9906fa-ec15-44f4-a2ca-f094fad77885" />

**Transform**
- Then I transformed each query by chaning column types, removed unnecessary columns, replaced values to remove specific words such as "[" and trimmed excess whitespace
- 
- data_jobs_all
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/6c200dc1b3dbeb3ae49d65bb34b39c7ca8cbb91f/Transform-salary.jpg">
- data_job_salary
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/6c200dc1b3dbeb3ae49d65bb34b39c7ca8cbb91f/Transform-skills.jpg">
**Load**
- Finally, I loaded both transformed queries into the workbook
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/586dfa7bac85c398dca91709f912a2ed40c76592/Load-all.jpg">
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/586dfa7bac85c398dca91709f912a2ed40c76592/Load-skills.jpg">

## Analysis

