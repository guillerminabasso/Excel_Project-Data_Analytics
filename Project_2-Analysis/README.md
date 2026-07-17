# Project 2 - Analysis

## Introduction

This project was created to learn Excel advanced tools and to analyze the demand, salaries, and required skills for different data roles across countries.

### Questions to answer:

1. Which data roles are the most in demand?
2. How many skills are required for each role, and what are their associated salaries?
3. What are the top 10 skills across data roles?
4. What are the median salaries in different countries?
5. Which skills are the most in demand, and what salaries are associated with them?

### Excel Skills Used

- 📊 Pivot Tables  
- 📈 Pivot Charts  
- 🧮 DAX (Data Analysis Expressions)  
- 🔍 Power Query  
- 💪 Power Pivot

### Dataset

The dataset used in this project contains real-world data science job postings from 2023. It was provided by the creator of the YouTube course and is available via this link: https://huggingface.co/datasets/lukebarousse/data_jobs

### ETL 

#### 📥 Extract

The first step was importing the dataset into Power Query to explore its structure and perform the initial cleaning and organization.
I created two main queries:
- one containing all job posting information, including salaries;
- another containing the exploded list of skills associated with each job_id.

IMAGEN

#### 🔄 Transform

Next, I transformed each query by:
- changing data types
- removing unnecessary columns
- cleaning text fields
- trimming extra whitespace

IMAGEN

#### 🔗 Load

Finally, I loaded both transformed queries into the Data Model, preparing the dataset for analysis in Power Pivot and Pivot Tables.

IMAGEN

### Data Modeling

I built the model of the data I needed for the analysis through Power Pivot by creating a relationship between the two queries using the job_id column. During the analysis I also created the DAX measures used to build the Pivot Tables and charts.

IMAGEN

## The Analysis

### 1. What are the most in-demand data roles?

Using the main query, I created a Pivot Table with job_title_short in the Rows area and created two measures to show the % of each of the job_title_short values in the dataset. 

<img width="797" height="266" alt="image" src="https://github.com/user-attachments/assets/748af426-3091-40c1-9c0f-6831b1625ad6" />

I added a slicer to filter the data for the country of interest.

**Key DAX Measures**

```DAX
Job Count :=
DISTINCTCOUNT(data_jobs_salary[job_id])

All Job Postings :=
CALCULATE(
    [Job Count],
    ALL(data_jobs_salary[job_title_short])
)

Role Likelihood :=
DIVIDE([Job Count], [All Job Postings])
```
#### Insights

- Across the entire dataset, Data Analyst is the most in-demand role, accounting for 30% of all job postings. It is followed by Data Scientist (26%) and Data Engineer (21%), highlighting the strong demand for analytics and data-related professionals.
- When filtering the data for France and Spain, Data Engineer represents a larger share of job postings (25% in France and 23% in Spain), while Data Analyst and Data Scientist rank second and third. This suggests that these markets place relatively greater emphasis on data engineering roles compared with the overall dataset, possibly reflecting the growing adoption of cloud-based data platforms and modern data infrastructure.


### 2. How many skills are required for each role, and what are their associated salaries?

For this analysis, I created four DAX measures: **Median Salary**, **Skill Count**, **Job Count**, and **Skills per Job**, where **Skills per Job** is calculated by dividing **Skill Count** by **Job Count**. This metric represents the average number of skills required per job posting for each data role.

Using these measures, I built a Pivot Table with `job_title_short` in the **Rows** area and **Median Salary** and **Skills per Job** in the **Values** area.

To better visualize the relationship between salary and the average number of required skills, I created a scatter chart and added a trendline to highlight the overall correlation between the two variables.

<img width="838" height="261" alt="image" src="https://github.com/user-attachments/assets/24520f68-b9b8-4ec5-a184-b9a06a03361c" />

#### Insights

- Overall, the chart suggests a positive relationship between the average number of skills required per job posting and median salary. Business Analyst and Data Analyst roles require an average of 3–4 skills per job posting and have median salaries between $85,000 and $90,000 per year. For most of the remaining roles (with the exception of Cloud Engineer), roles requiring more skills also tend to offer higher median salaries.
- Data Engineer roles require an average of 7 skills per job posting and have a median salary of approximately $130,000. In comparison, Data Scientist and Senior Data Scientist roles require around 5 skills on average but offer higher median salaries, ranging from $145,000 to $155,000. Senior Data Engineer roles combine the highest skill requirements (around 8 skills) with a median salary of approximately $150,000.



