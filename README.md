# Introduction

The data analytics job market continues to evolve rapidly, driven by increasing demand for data-driven decision-making across industries. This project contains over 150 countries with a focus to explores the UK data analytics job market, focusing on job titles, salary trends, locations, and required skills. The goal is to uncover actionable insights that can guide aspiring and practicing data analysts on which skills are most valuable, most demanded, and most financially rewarding.

# Background

With the growing importance of analytics in business strategy, understanding the intersection between skill demand and salary is crucial. Job seekers often face uncertainty about which skills to prioritize, while employers seek professionals who can deliver immediate value. This project analyzes real job posting data to answer key questions around demand trends, compensation, and optimal skill choices, with a primary focus on the UK job market.

## Key Questions Explored

This project addresses the following  questions:

1. What are the most in-demand skills for the top 3 most popular data roles?

2. How are in-demand skills trending over time for Data Analysts?

3. How well do jobs and skills pay for Data Analysts in the UK?

4. What are the optimal skills for Data Analysts to learn (high demand & high paying)?

## Tools & Technologies Used
Programming & Analysis

- Python

    - Pandas (data manipulation & analysis)

    - Matplotlib (data visualization)

    - Seaborn (statistical visualization)

Development Environment

    - Jupyter Notebook

    - Visual Studio Code

Version Control

    - Git & GitHub



## Data Preparation & Cleanup
This section outlines the steps taken to prepare data in ensuring accuracy and consistency.

## Import & Clean Up Data
I started by importing necessary libraries and loading the dataset, followed by inital data cleaning tasks to ensure data quality

```python
from datasets import load_dataset
import matplotlib.pyplot as plt
import seaborn as sns
import ast
dataset = load_dataset('lukebarousse/data_jobs')

df = dataset['train'].to_pandas()


import pandas as pd
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```
## Filter UK Jobs
My major focus mainly is to analyse the UK job market, out of over 160 countries i filtered out the UK from the dataset for my analysis.


## The Analysis
Each Jupyter notebook for this project aimed at investigating specific aspects of the data job market. Here's how i approached each question:

# 1. What are the Most demanded skills for the top 3 ,ost popular data roles?

To identify the most in-demand skills for the top 3 data roles, I first determined which positions were most popular, then identified the top 5 skills for each role. this analysis reveals the key to focus on based on my target position.

View my notebook with detailed steps here: [2_Skill_Demand.ipynb](3_Project\3_Skill_Demand.ipynb)



## Visualize Data

```python
fig, ax = plt.subplots(len(job_titlles), 1, figsize=(8, 2.5*len(job_titlles)))

for i, job_title in enumerate(job_titlles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```

## Results

![Visualization of Top Skills for Data Olawale](3_Project\images.png)
 *Bar graph visualizing the salary for the top 3 data roles and their top 5 skills associated with each.*


## Insights

- Python ranks as one of the most sought-after skills across the three leading data roles, particularly for Data Scientists (featured in 69% of postings) and Data Engineers (around 60%). 
- SQL remains the top-requested skill for both Data Analysts and Data Engineers, while Python clearly dominates Data Scientist job requirements.
- Data Analysts tend to rely more on tools such as Excel and Power BI for reporting and analysis, whereas Data Engineers and Data Scientists require deeper, more specialized technical expertise, including cloud platforms like AWS and Azure for data infrastructure and deployment.


# 2. How are in-demand skills trending  for Data Analysis?
To find how skills are trending in 2023 for Data Analysts, I filtered data analyst positions and grouped the skills by the month of the postings. This got me the top 5 skills of data analysts by month, showing how popular skills were throughout 2023.

View my notebook with detailed steps here: [3_Skill_Trend.ipynb](3_Project\3_Skill_Demand.ipynb)

## Visualize Data
```python
from matplotlib.ticker import PercentFormatter

df_plot = df_DA_UK_percent.iloc[:,:5]
sns.lineplot(data=df_plot, dashes=False, legend='full',palette='tab10')

plt.gca().yaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```
## Results
![Trending Top Skills for Data Analyst in the UK](3_Project\skill_Trend_DA.png)           
*Bar graph visualizing the trending top skills for data analysts in the US in 2023.*

 ### Insights:
 Here is a more concise version of your analysis:

*   **SQL and Excel Dominate:** SQL peaks at nearly 70% (May) while Excel holds steady at 45-55%, solidifying them as the essential, non-negotiable baseline skills.
*   **Power BI Leads Visualization:** Power BI (30-45%) consistently outperforms Tableau, establishing itself as the clear market leader for visualization tools in the UK.
*   **Q4 Surge for Niche Skills:** Despite lower overall demand, Python and Tableau showed a distinct upward trend starting in September, signaling growing interest in advanced technical skills toward the end of the year.

# 3. How well do jobs and skills pay the Data Analysts?
To identify the highest-paying roles and skills, I only got jobs in the United Kingdom  and looked at thier median salary, But first i looked at ther salary distribution of common data jobs like Data Scientist, Data Engineer, and Data Analyst, to get an idea of which jobs are paid the most. 

View my notebook with detailed steps here: [4_Salary_Analysis.ipynb](3_Project\4_Salary_Analysis.ipynb)


## VIsualize Data

```python
sns.boxplot(data=df_UK_top6, x='salary_year_avg', y='job_title_short', order=job_order)

ticks_x = plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()

``` 

## Results
![Salary Distribution of Data Jobs in the UK](3_Project\Salary_Analysis.png)
*Box plot visualizing the salary distribution for the top data job titles.*

 ### Insights:
 - **Pay rises with seniority and specialization:** Senior roles sit higher overall than non-senior ones, and the most lucrative track shown is **Senior Data Scientist**, with most salaries clustered roughly around **$100k–$160k** and reaching into the **$170k+** range.

- **Biggest spread in Data Scientist and Data Engineer:** **Data Scientist** and **Data Engineer** have the widest ranges (large boxes/long whiskers), meaning pay varies a lot by company, location, or experience. Data Scientist stretches from roughly the **$40k–$200k** area, and Data Engineer commonly runs from about **$40k up to $160k+**.

- **Analyst roles are lower and tighter, with a few high outliers:** **Data Analyst** tends to be lower (mostly around **$60k–$110k**) but has occasional higher points (around **$170k+**). **Senior Data Analyst** looks comparatively tight around **~$100k**, suggesting more consistent pay than the other roles.


# 4.(a) Highest Paid & Most Demanded Skills for Data Analysts
Next, I narrowed my analysis and focused only on data analyst roles. I looked at the highest-paid skills and the most in-demand skills. I used two bar charts to showcase these.

## Visualize Data
```python

fig, ax = plt.subplots(2, 1)

 # Top 10 Highest Paid Skills for Data Analysts   
sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analyst
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')

plt.show()

```

## Results

 ![The Highest Paid & Most In-Demand Skills for Data Analysts in the UK](3_Project\output.png)
*Two separate bar graph visualizing the highest paid skills and most in-demand skills fo data analysts in the UK.*

## Insights:

- Highest-paid skills skew toward **Advanced Programming & Data Engineering tools** Skills like C++, NumPy, TensorFlow, PyTorch, and Pandas command the highest median salaries around **$170k–$180k**, indicating strong market value for advanced analytics, ML, and performance-oriented programming.

- Most in-demand skills are more business-oriented but pay less. Tools such as Tableau, SQL, Power BI, Python, and Excel appear most frequently in job postings, but their median salaries are notably lower roughly **$70k–$110k**, reflecting broader adoption and lower specialization barriers.

- There’s a clear trade-off between demand and pay. Highly specialized technical skills offer higher salaries but lower demand, while widely used analytics and BI tools offer higher demand but moderate pay, suggesting different career paths depending on whether one prioritizes income or job availability.

# 4.(b) Whats is the most optimal skill to learn for Data Analysts?

### Visualize Data

```python
from adjustText import adjust_text
import matplotlib.pyplot as plt

plt.scatter (df_DA_skills_high_demand
['skill_percent'], df_DA_skills_high_demand
['median_salary'])
plt.show()

```

#### Results
![Most Optimal Skills for Data Analyst in the UK](3_Project\output1.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for the analyst in the UK*

### Insights:
- High-value niche skills stand out: Skills like SQL Server and Airflow command some of the highest median salaries despite appearing in a relatively small percentage of job postings, suggesting strong pay for specialized expertise.

- Core skills balance demand and pay: SQL and Python are the most widely requested skills, appearing in a large share of data analyst roles, while still offering solid median salaries, making them foundational and high-return skills.

- Common tools trade pay for accessibility: Frequently required tools such as Excel, Power BI, Tableau, and Looker appear in many job postings but generally offer moderate salaries, indicating they are essential but less differentiating skills.

# Challenges Faced

- Handling nested and multi-valued skill fields required careful data transformation.

- Ensuring consistency in skill naming across thousands of job postings.

- Balancing visual clarity when labeling dense plots.

- Dealing with missing salary data while maintaining analytical integrity.

# Conclusions

This project highlights that:

- Foundational skills like SQL and Python are essential for data analysts in the UK.

- Learning only common tools may limit earning potential; specialization matters.

- Data analysts can maximize career outcomes by balancing market demand with salary insights when choosing skills to learn.

- The UK job market offers strong opportunities for analysts who combine core skills with high-value niche expertise.

