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
   
## 1. Does more skills get you a higher paying job?
### Skill: Power Query (ETL)

### Extract
- I used Power Query to extract the original dataset to create two queries
  - The first query had all the data job information from the original dataset with an index column (job_id).
  - The second query listed the skills for each job_id. The second query only has two columns, the job_id and the skills column, we need the job_id with the skills column is to ensure when unpivoting the skills they stay under the same unique ID.
<img width="547" height="384" alt="image" src="https://github.com/user-attachments/assets/8e9906fa-ec15-44f4-a2ca-f094fad77885" />

### Transform
- Then I transformed each query by chaning column types, removed unnecessary columns, replaced values to remove specific words such as "[" and trimmed excess whitespace
  - data_job_salary
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/6c200dc1b3dbeb3ae49d65bb34b39c7ca8cbb91f/Transform-salary.jpg">

  - data_job_skills

<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/6c200dc1b3dbeb3ae49d65bb34b39c7ca8cbb91f/Transform-skills.jpg">

### Load
- Finally, I loaded both transformed queries into the workbook
  - data_job_salary
   <img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/586dfa7bac85c398dca91709f912a2ed40c76592/Load-all.jpg">

  - data_job_skills
   <img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/586dfa7bac85c398dca91709f912a2ed40c76592/Load-skills.jpg">

## Insights
- There is a positive relationship between the number of skills and the median salary. Jobs that require more skills tend to offer higher paying salaries such as roles in Senior Data Engineer and Senior Data Scientists.
- An outlier would be Data Scientists, it shows they have a high salary whilse a lower skill average, this could hint that experience or role level could affect the pay more than skill count.

<img width="893" height="474" alt="image" src="https://github.com/user-attachments/assets/5f8a4a85-5dca-4582-817d-1e62128e2c24" />

## 2. What's the median salary for data jobs when compared to the US and countries outside the US?
### Skills: Pivot Tables & DAX
- Moving the job_title_short to the rows field and the salary_year_avg into the values field, however, I could not get value field to be MEDIAN, which I had to use DAX to add a new measure to calculate the median salary from salary_year_avg.
- I first needed to add a new measure to calculate the median salary for United States Job.
```
=CALCULATE(MEDIAN(data_jobs_salary[salary_year_avg], data_jobs_salary[job_country] = "United States")
```
- I then needed to add a new measure to calculate the median salary for data jobs that are not in the United States.
```
=CACULATE(MEDIAN(data_jobs_salary[salary_year_avg], data_jobs_salary[job_country] <> "United States")
```
- Finally, I needed to add a new measure to calculate the median salary for data jobs as a baseline.
```
Median Salary := MEDIAN(data_jobs_salary[salary_year_avg])
```
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/0a8113d0063e3c4f75e87a417cc83083b2de729b/images/median%20calculation.jpg">

### Insights
- In New Zealand, roles such as Data Engineer and Data Scientist tend to have higher average salaries than both the United States and internationally, showing that technical and analytical expertise are highly valued in New Zealand. 
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/5d55bc148c3e15feec7f6b79280ff8c399bb101c/images/second%20question.jpg">

## 3. What are the top skills for data jobs?
### Skill: Power Pivot
- I created a PivotTable using the Data Model I created with Power Pivot, where I joined the data_jobs_salary with data_jobs_skills, where the flow goes from data_jobs_salary to data_jobs_skills.
