# Project 2 - Analysis

## Introduction

This project was created to learn Excel advanced tools and to analyze how the different data roles and its salaries and skills associated fluctuate for different countries.

### Questions to answer:

1. What are the most in-demand data roles?
2. How many skills are demanded for different roles and what are the salaries associated to them?
3. What are the top 10 skills for Data roles?
4. What are median salaries in different countries?
5. What are the most in-demand skills and their associated salaries?

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

The first thing I did was to import the dataset to Power Query to understand how it was structured and to perform some cleaning and organizing of the data. 
I then created two main queries, one with all of the information (including salaries) and the second one with the skills exploded associated to each of the job_id. 

IMAGEN

#### 🔄 Transform

Then, I transformed each query by changing column types, removing unnecessary columns, cleaning text to eliminate specific words, and trimming excess whitespace.

IMAGEN

#### 🔗 Load

Finally, I loaded both transformed queries into the workbook, setting the foundation for my subsequent analysis.

IMAGEN

### Data Modeling

I build the model of the data I needed for the analysis through Power Pivot by creating the connections of both of the queries on the job_id column. During the analysis I also created the measures I would use the build the tables and charts for visualization.

IMAGEN

## The Analysis

### 1. What are the most in-demand data roles?

I used the first query to build a Pivot Table with the job_title_short column on the rows, and the count of each of the roles on the values. I then 







