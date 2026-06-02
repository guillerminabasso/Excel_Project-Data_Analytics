# Excel Salary Dashboard

<img width="1135" height="822" alt="Captura de pantalla 2026-06-02 130809" src="https://github.com/user-attachments/assets/8fc55b74-4d4c-4128-8759-d6320919f33f" />


## Introduction

This dashboard was created to help data science job seekers understand how job postings and key market variables fluctuate.

This project is based on an Excel tutorial created by a renowned data analytics content creator. It is part of my learning journey toward becoming a data analyst. While the original dataset and project structure were inspired by the tutorial, I implemented several personal modifications to tailor the analysis to my own interests and objectives.

### Dashboard File
My final dashboard is in [here](Project_1-Dashboard/1_Salary_Dashboard.xlsx).

### Excel Skills Used

The following Excel skills were utilized for analysis:

- **📉 Charts**
- **🧮 Formulas and Functions**
- **❎ Data Validation**

### Data Jobs Dataset 

The dataset was sourced from a public Excel tutorial focused on data analytics. It contains real-world data science job information from 2023 and is included in this repository.  The data contains detailed information on job titles, salaries, locations, and essential skills that are presented here.

- **👨‍💼 Job titles**
- **💰 Salaries**
- **📍 Locations**
- **🛠️ Skills**

- ## Dashboard build

- ### 📉 Charts

#### 📊 Data Science Job Salaries - Bar Chart

<img width="875" height="468" alt="Captura de pantalla 2026-06-02 140828" src="https://github.com/user-attachments/assets/915609de-2672-4f48-926a-2df74112e7e3" />



- 🛠️ **Excel Features:** Utilized bar chart feature (with formatted salary values) and optimized layout for clarity. To improve dashboard interactivity, additional helper columns were created to support dynamic updates in the bar chart visualizations.
- 🎨 **Design Choice:** Horizontal bar chart for visual comparison of median salaries.
- 📉 **Data Organization:** Sorted job titles by descending salary for improved readability.  
- 💡 **Insights Gained:** This enables quick identification of salary trends, noting that Senior roles and Engineers are higher-paying than Analyst roles.

#### 📈 Month distribution of job postings - Line Chart

<img width="833" height="497" alt="Captura de pantalla 2026-06-02 142613" src="https://github.com/user-attachments/assets/857e390e-ef27-457e-b0ad-6ffe68564c36" />


- 🛠️ **Excel Features:** Utilized Excel line chart features with formatted values and an optimized layout for improved clarity.
- 🎨 **Design Choice:** A line chart was selected to visually compare the number of job postings throughout the year.
- 📉 **Data Organization:** Additional helper columns were created to highlight the minimum and maximum values, allowing for a quick understanding of which months had the highest and lowest number of job postings.
- 💡 **Insights Gained:** This visualization enables quick identification of hiring trends over time, helping job seekers determine the most active months for applications. From a company perspective, it can also provide insights into the most effective periods for recruiting new employees.

#### 🥧 Distribution of On-Site and Remote Jobs - Pie Chart

<img width="362" height="215" alt="image" src="https://github.com/user-attachments/assets/b7fe9410-2b31-4bc8-b6f5-4fe34bb1c03b" />

- 🛠️ **Excel Features:** Utilized Excel pie chart features to provide a quick understanding of the distribution.
- 🎨 **Design Choice:** A pie chart was selected to visually represent the percentage of on-site versus remote jobs.
- 💡 **Insights Gained:** This visualization enables quick identification of the proportion of on-site and remote roles, allowing job seekers to compare distributions across different job roles and countries.

### 🧮 Formulas and Functions

#### 💰 Median Salary by Job Titles 

```
=MEDIAN(
FILTER(
jobs[salary_year_avg];
(jobs[job_title_short]=B2)*
(jobs[job_country]=my_country)*
(jobs[salary_year_avg]<>0)*
(ISNUMBER(SEARCH(my_type;jobs[job_schedule_type])))))

```
- 🔍 **Multi-Criteria Filtering:** Checks job title, country, schedule type, and excludes blank salaries.
- 📊 **Array Formula:** Utilizes `MEDIAN()` function with nested `FILTER()` statement to analyze an array.
- 🎯 **Tailored Insights:** Provides specific salary information for job titles, regions, and schedule types.
- **🔢 Formula Purpose:** This formula populates the table below, returning the median salary based on job title, country, and type specified.

<img width="347" height="283" alt="Captura de pantalla 2026-06-02 153422" src="https://github.com/user-attachments/assets/83a8e15e-6fb8-499e-a7cf-cce04c4c8366" />  

📉 Dashboard Implementation  

<img width="434" height="456" alt="Captura de pantalla 2026-06-02 151655" src="https://github.com/user-attachments/assets/b8fd2847-482c-482c-8616-7dba7c7eb850" />  

#### ⏰ Count of Job Schedule Type

```
=NOT(ISNUMBER(SEARCH("and";M2)))*(M2<>0)
```

- 🔍 **Unique List Generation:** This Excel formula uses the SEARCH() function to exclude entries containing “and” and to remove zero values.
- 🔢 **Formula Purpose:** This formula generates the table below, which provides a list of unique job schedule types. Combined with the MEDIAN(FILTER()) function shown earlier, it allows us to build the following bar chart.

🍽️ Background Table
    
<img width="320" height="144" alt="Captura de pantalla 2026-06-02 153631" src="https://github.com/user-attachments/assets/68d3adf8-8db0-4944-9382-7fb3a79c0e51" />  


📉 Dashboard Implementation:  


<img width="858" height="379" alt="Captura de pantalla 2026-06-02 153251" src="https://github.com/user-attachments/assets/cf07eae2-9a5c-440e-9eb8-747e5d970dc7" />  

#### 🏆 Top Job Postings Platform

```
=COUNTIFS(
jobs[job_title_short];my_title;
jobs[job_via];T2;
jobs[job_schedule_type];my_type;
jobs[job_country];my_country)

```

- 🔢 **Formula Purpose:** This formula identifies the platform with the highest number of job postings for the selected filters (job title, schedule type, and country).
- 📊 **Sorting Logic:** The results are sorted in descending order using the SORT() function to rank platforms from highest to lowest number of postings.
- 🏆 **KPI Insight:** The first value of the sorted result is then extracted and displayed in a KPI card, representing the most frequently used job platform.
- ⚡ **Performance Note:** COUNTIFS() was used instead of ROWS(FILTER()) due to better performance and efficiency on large datasets.
- ⚖️ **Trade-off:** This approach removes the previous SEARCH("and", M2) logic, but since the goal here is to determine the single most frequent platform, this simplification does not impact the final insight.  

🍽️ Background Table  

<img width="680" height="263" alt="Captura de pantalla 2026-06-02 155858" src="https://github.com/user-attachments/assets/0809fc75-7388-4244-bc07-f590320c904b" />  

📉 Dashboard Implementation:  

<img width="498" height="163" alt="Captura de pantalla 2026-06-02 155923" src="https://github.com/user-attachments/assets/aac07960-2cfe-4ecb-9bac-653bb4cae973" />


#### 🔢 Job Count
```
=ROWS(
FILTER(
jobs[job_title_short];
(jobs[job_title_short]=AC2)*
(jobs[job_country]=my_country)*
(ISNUMBER(SEARCH(my_type;jobs[job_schedule_type])))
```


- 🔢 **Formula Purpose:** This formula counts the number of rows returned by a filtered dataset based on job title, country, and job type.
- 🔍 **Filtering Logic:** The FILTER() function applies multiple conditions to isolate relevant job postings, including a partial match using SEARCH() for job schedule type.
- 🏆 **KPI Insight:** Combined with an XLOOKUP() based on selected job title, country, and job type, this result is used to populate a KPI card displaying the total number of job postings.

<img width="498" height="151" alt="Captura de pantalla 2026-06-02 161033" src="https://github.com/user-attachments/assets/2a0f5534-7753-4479-89c7-edc61903ea24" />

### ❎ Data Validation  

#### 🔍 Filtered List  

- 🔒 **Enhanced Data Validation:** Implementing the filtered list as a data validation rule under the `Job Title`, `Country`, and `Type` option in the Data tab ensures:
    - 🎯 User input is restricted to predefined, validated schedule types
    - 🚫 Incorrect or inconsistent entries are prevented
    - 👥 Overall usability of the dashboard is enhanced

<img width="648" height="357" alt="Captura de pantalla 2026-06-02 162627" src="https://github.com/user-attachments/assets/62aae1e9-605b-4264-8953-4047484f7e56" />

## Conclusion

I created this dashboard to apply all the tools I learned during an Excel course. Building this project also allowed me to explore how the data science job market behaved in 2023.

This analysis provides an initial overview of key insights, such as how salaries vary by location, the likelihood of finding remote jobs, and which platforms are most commonly used in each country.










