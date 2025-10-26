# Excel_Data_Analysis_Project

## Introduction
In today's competitive job market, understanding how job requirements translate into salary outcomes is important for both job seekers and employers. This project explores a dataset of global data job postings in 2023. This project sets out to find the most important and highest paying skills in the data job market.

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
- These salary insights help jobseekers focus choose the role to focus on while considering geographical locations. While also helping companies align their offers with the market standards while considering geographical locations.
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/5d55bc148c3e15feec7f6b79280ff8c399bb101c/images/second%20question.jpg">

## 3. What are the top skills for data jobs?
### Skill: Power Pivot
- I created a PivotTable using the Data Model I created with Power Pivot, where I joined the data_jobs_salary with data_jobs_skills, where the flow goes from data_jobs_salary to data_jobs_skills.
- I created a relationship between my two tables using the job_id column.
<img src="https://github.com/ewensyee/Excel_Data_Analysis_Project_with_Dashboard/blob/4d1dafdf48794be33d3a93806382eda0c6eec750/images/data%20model.jpg">

- Moving the skills to the rows field and skill likelihood into the values field.
  - Creating the measure of skill likelihood, I used DAX to calculate the likelihood of skills appearing in job postings.
```
= DIVIDE([skill_count], [job_count])
```
### Insights
- In data related jobs, SQL and Python are the most in-demand skills, where SQL appears nearly 60% of data job postings, with Python following closely.
- Big data and cloud tools such as Spark, Azure and AWS appear in several postings, underlining the industry's shift towards more scalable data solutions.
- Understanding a wide range or skills is necessary in the current industry.
<img width="846" height="454" alt="image" src="https://github.com/user-attachments/assets/0f08dc32-72eb-4674-ae2c-2ee54210bbb8" />

## 4. What's the pay for the top 10 skills?
### Skills: Pivot Chart
- I created a combo PivotTable to plot the median salary and skill count
  - **Primary Axis:** Medain Salary (as a Clustered Column)
  - **Secondary Axis:** Skill Count (as a Line with Markers)
 
### Insights
- In the data industry, Spark is the highest-paying skill, despite having the highest-paying skill, it has the lowest skill count which suggests it's a more specialized skill in higher demand than its current supply.
- Excel is a high in-demand skill but with low-paying skill, which could indicate the skill is widely known and may be a foundational skill rather than a specialized skill in the job market.

<img width="1005" height="478" alt="image" src="https://github.com/user-attachments/assets/91b701f4-7023-420d-b234-ce752512c3b6" />

# Dashboard
If you want to play around with the dashboard you can download it and open it through this [link](https://1drv.ms/x/c/eeea490656099efa/EfjZh-Hw6SRLmH31vhHI0HkBsKLoMzhQnKpuw48AXaI3Yg?e=VCmZUa).
<img width="972" height="678" alt="image" src="https://github.com/user-attachments/assets/c1bd647b-fd10-4225-a815-49c5f2330e65" />




