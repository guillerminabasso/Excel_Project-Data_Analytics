# Project 2 - Analysis

## Introduction

This project was created to learn Excel advanced tools and to analyze the demand, salaries, and required skills for different data roles across countries.

### Questions to answer:

1. Which data roles are the most in demand?
2. How many skills are required for each role, and what are their associated salaries?
3. What are the top 10 skills across data roles?
4. What’s the salary for data jobs in different regions?
5. Which skills are the most in demand, and what salaries are associated with them?

### Excel Skills Used

- 📊 Pivot Tables  
- 📈 Pivot Charts  
- 🧮 DAX (Data Analysis Expressions)  
- 🔍 Power Query  
- 💪 Power Pivot

### Dataset

The dataset used in this project contains real-world data science job postings from 2023. It was provided by the creator of the YouTube course and is available in the Resources folder of this repository.

### ETL 

#### 📥 Extract

The first step was importing the dataset into Power Query to explore its structure and perform the initial cleaning and organization.
I created two main queries:
- one containing all job posting information, including salaries;
- another containing the exploded list of skills associated with each job_id.

<img width="762" height="382" alt="image" src="https://github.com/user-attachments/assets/d0beff14-45f6-4e28-8a9c-8b3f642a6158" />

<img width="595" height="381" alt="image" src="https://github.com/user-attachments/assets/6791c5b6-e31c-4314-bf68-07337256dc92" />



#### 🔄 Transform

Next, I transformed each query by:
- changing data types
- removing unnecessary columns
- cleaning text fields
- trimming extra whitespace

<img width="187" height="255" alt="image" src="https://github.com/user-attachments/assets/4308d113-bec0-4f70-a227-b3c797595409" />

<img width="188" height="291" alt="image" src="https://github.com/user-attachments/assets/5ab9fbd9-b8fd-43e4-89ee-d89e97cc275e" />



#### 🔗 Load

Finally, I loaded both transformed queries into the Data Model, preparing the dataset for analysis in Power Pivot and Pivot Tables.

### Data Modeling

I built the model of the data I needed for the analysis through Power Pivot by creating a relationship between the two queries using the job_id column. During the analysis I also created the DAX measures used to build the Pivot Tables and charts.

<img width="362" height="385" alt="image" src="https://github.com/user-attachments/assets/8dbc9c98-57eb-4a82-a223-24ad5e3b777d" />


## The Analysis

### 1. What are the most in-demand data roles?

Using the main query, I created a Pivot Table with job_title_short in the Rows area and created two measures to show the % of each of the job_title_short values in the dataset. 

<img width="803" height="245" alt="image" src="https://github.com/user-attachments/assets/11c6917f-c774-4b7a-9dd5-3de85248f648" />

I added a slicer to filter the data for the country of interest (France).

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

- **Data Engineer**, **Data Scientist**, and **Data Analyst** are the three most in-demand data roles in France, accounting for 72% of all job postings.
- **Data Engineers** and **Data Scientists** show slightly higher demand than **Data Analysts**, representing 25%, 24%, and 22% of job postings, respectively.
- Overall, the French data job market offers strong opportunities across all three roles. While **Data Analyst** positions remain highly sought after, the slightly higher demand for **Data Engineers** and **Data Scientists** suggests that professionals with the required technical skills may find a broader range of opportunities in those career paths.


### 2. How many skills are required for each role, and what are their associated salaries?

For this analysis, I created four DAX measures: **Median Salary**, **Skill Count**, **Job Count**, and **Skills per Job**, where **Skills per Job** is calculated by dividing **Skill Count** by **Job Count**. This metric represents the average number of skills required per job posting for each data role.

Using these measures, I built a Pivot Table with `job_title_short` in the **Rows** area and **Median Salary** and **Skills per Job** in the **Values** area.

To better visualize the relationship between salary and the average number of required skills, I created a scatter chart and added a trendline to highlight the overall correlation between the two variables.

<img width="842" height="274" alt="image" src="https://github.com/user-attachments/assets/08010512-cf1d-4ad2-ad33-89e45a675d73" />


#### Insights

- Overall, the chart suggests a positive relationship between the average number of skills required per job posting and median salary. **Data Engineers** are a notable exception, requiring an average of 8 skills while offering a median salary of $100K, compared with Senior Data Engineers, who require a similar number of skills but command a median salary of $150K.
- **Data Analyst** is the lowest-paying role in France, with a median salary of $65K and an average of 4 skills required per job posting. In comparison, **Data Scientists** also require around 4 skills but earn a considerably higher median salary of $85K.
- **Senior Data Scientist**, **Software Engineer**, and **Senior Data Analyst** roles appear to offer a strong balance between skill requirements and compensation, requiring an average of 4 to 6 skills while providing median salaries ranging from $110K to $160K.

### 3. What are the top 10 skills across data roles?

For this analysis, I created a pivot table based on the job_skills column from the data_jobs_skills table. For the values, I added a new measure called **Skill Likelihood**, which represents the percentage of job postings requiring each skill across the entire dataset.

The results were filtered to show the top 10 most frequently appearing skills and visualized using a bar chart. Slicers were also added to allow filtering by country and data role of interest.

<img width="776" height="257" alt="image" src="https://github.com/user-attachments/assets/4f293c41-e945-4640-8302-86d5242bae1a" />


#### Insights

- Filtering the data for **Data Analyst** roles, we can see that the most demanded skills are **SQL** (50%), **Excel** (40%), **Python** (29%), and **Tableau** (28%). This highlights the importance of mastering SQL, spreadsheet tools, a programming language (with Python being the most widely adopted for analytics), and a data visualization tool such as Tableau. Other relevant skills, including **SAS**, **Power BI**, **R**, **Word**, **PowerPoint**, and **Oracle**, appear in approximately 15% to 20% of job postings, showing the relevance of statistical analysis, reporting tools, and database technologies for Data Analyst positions.
- Looking at **Data Engineer** roles, the top skills include **SQL**, **Python**, **AWS**, **Spark**, **Azure**, **Java**, **Snowflake**, **Hadoop**, **Kafka**, and **NoSQL** technologies. Compared with Data Analyst roles, these skills demonstrate the stronger emphasis on software engineering, cloud infrastructure, big data processing, and database technologies required for building and maintaining data platforms.

### 4. What’s the salary for data jobs in different regions?

For this analysis I built two new DAX measures **US Median Salaries** and **Non-US Median Salary** in order to compare the median salaries between a selected country, the US (the majority of the data is from the US) and the rest of the countries. 

<img width="556" height="239" alt="image" src="https://github.com/user-attachments/assets/84013cd6-e9ec-495b-8841-e0a72895247a" />

#### Insights

- Senior Data Engineer and Data Scientist roles command the highest median salaries both in the United States and internationally, highlighting the strong global demand for experienced data professionals.
- Data Analyst, Machine Learning Engineer, Data Scientist, and Data Engineer roles have lower median salaries in France than in both the United States and the non-US median. Business Analyst is the exception, with a median salary comparable to or higher than the non-US median. These differences suggest that salaries for data roles vary considerably across countries, reflecting differences in local labor markets, demand, and compensation levels.

### 5. What are the Highest-Paying Skills and Their Likelihood in Job Postings?

For this analysis, I created two new DAX measures: **Median Salary – Skills** and **Skill Likelihood**. To calculate the median salary associated with each skill, I used the CROSSFILTER DAX function to temporarily enable bidirectional filtering between the data_jobs_salary and data_jobs_skills tables through the job_id field.

```DAX
Median Salary - Skills =
CALCULATE(
    [Median Salary],
    CROSSFILTER(
        data_jobs_salary[job_id],
        data_jobs_skills[job_id],
        Both
    )
)
```
I then created a combo chart displaying the 10 highest-paying skills alongside their likelihood of appearing in job postings. This visualization highlights the relationship between the earning potential of each skill and how frequently it is requested by employers.

<img width="914" height="286" alt="image" src="https://github.com/user-attachments/assets/5053936c-20bf-4ce5-b4ac-0177239be37e" />

#### Insights

- The most in-demand skills for Data Analysts are associated with median salaries ranging from **$80K to $100K**, with Airflow and Tableau being the only exceptions, offering slightly lower median salaries.
- **SQL** is by far the most requested skill, appearing in 55% of job postings, followed by **Python** and **Tableau**, each appearing in approximately 40% of postings. The remaining skills (Excel, Power BI, AWS, Snowflake, Azure, Spark, and Airflow) appear in 10%–20% of job postings.
- These results highlight the importance of mastering **SQL** and **Python**, as they combine high demand with strong salary potential. They also show that expanding beyond traditional Data Analyst tools (such as Excel, Power BI, and Tableau) by learning cloud platforms (AWS and Azure), cloud data warehousing (Snowflake), distributed data processing (Apache Spark), and workflow orchestration (Apache Airflow) can help develop a broader and more competitive data skill set.

## Conclusion















