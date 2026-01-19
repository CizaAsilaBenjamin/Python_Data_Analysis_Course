# Overview
Welcome to my analysis of the data job market, focusing on data analyst roles. This project was created out of a desire to navigate and understand the job market more effectively. It delves into the top-paying and in-demand skills to help find optimal job opportunities for data analysts.

The data sourced from Luke Barousse's Python Course which provides a foundation for my analysis, containing detailed information on job titles, salaries, locations, and essential skills. Through a series of Python scripts, I explore key questions such as the most demanded skills, salary trends, and the intersection of demand and salary in data analytics.

# The Questions
Below are the questions I want to answer in my project:

- What are the skills most in demand for the top 3 most popular data roles?

- How are in-demand skills trending for Data Analysts?
- How well do jobs and skills pay for Data Analysts?
What are the optimal skills for data analysts to learn? (High Demand AND High Paying)

# Tools I Used
For my deep dive into the data analyst job market, I harnessed the power of several key tools:

- Python: The backbone of my analysis, allowing me to analyze the data and find critical insights.I also used the following Python libraries:
- Pandas Library: This was used to analyze the data.
Matplotlib Library: I visualized the data.
- Seaborn Library: Helped me create more advanced visuals.
- Jupyter Notebooks: The tool I used to run my Python scripts which let me easily include my notes and analysis.
- Visual Studio Code: My go-to for executing my Python scripts.
- Git & GitHub: Essential for version control and sharing my Python code and analysis, ensuring collaboration and project tracking.

# Data Preparation and Cleanup
This section outlines the steps taken to prepare the data for analysis, ensuring accuracy and usability.

# Import & Clean Up Data
I start by importing necessary libraries and loading the dataset, followed by initial data cleaning tasks to ensure data quality.

# Importing Libraries
```python import ast
import pandas as pd
import seaborn as sns
from datasets import load_dataset
import matplotlib.pyplot as plt  
```
# Loading Data
```python 
dataset = load_dataset('lukebarousse/data_jobs')
df = dataset['train'].to_pandas()
```
# Data Cleanup
```python 
df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
```
Filter US Jobs
To focus my analysis on the U.S. job market, I apply filters to the dataset, narrowing down to roles based in the United States.
```python
df_US = df[df['job_country'] == 'United States']
The Analysis
```


# The analysis

## 1. What are the most demanded skills for the top 3 most popular data roles ?

To find the most demanded skills for the most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. this query highligths the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my nootbook with detailed steps here : 
[2 Skills demand](2_projectLucasPython\2_Skills_demand.ipynb)

### Visualize Data

```Python

fig, ax = plt.subplots(len(job_titles), 1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.set_theme(style="ticks")
    sns.barplot(data=df_plot, y='job_skills', x='skill_perc', ax=ax[i], palette='dark:b_r', hue='job_skill', dodge=False, legend=False)
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].set_xlim(0, 78)


    for n, v in enumerate(df_plot['skill_perc']):
        ax[i].text(v + 1, n, f"{v:.0f}%", color='black', va='center')

        if i != len(job_titles) - 1:
            ax[i].set_xticks([])

    fig.suptitle('Likelihood of skills in job postings in the US', fontsize=15)
    fig.tight_layout(h_pad=0.5)

plt.show()
```

### Resultat 
![Visualization of top skills for data Nerd](2_projectLucasPython\Images\image_skills_demand.png)

### What are the insights ?

### 📌 1. Core Skills Across All Roles
- **SQL** and **Python** are the most consistently demanded skills across all three roles:
  - SQL: 51% (Analyst), 68% (Engineer), 51% (Scientist)
  - Python: 27% (Analyst), 65% (Engineer), 72% (Scientist)
- These two skills form the **technical backbone** of data work, indicating that proficiency in both is essential regardless of specialization.


### 🔍 2.Strategic Insights

- **Overlap vs. Differentiation**:
  - SQL and Python are universal.
  - Visualization tools (Excel, Tableau) are analyst-centric.
  - Cloud and distributed tools (AWS, Spark) are engineer-centric.
  - Statistical tools (R, SAS) are scientist-centric.

- **Skill Evolution**:
  - Python’s rise across all roles suggests a shift toward **programmatic data work**.
  - Tableau’s presence in both analyst and scientist roles shows the growing importance of **data storytelling**.

- **Hiring Signals**:
  - Employers expect **multi-tool fluency**: not just one language or platform.
  - Candidates who combine core skills (SQL, Python) with role-specific tools (e.g., AWS for engineers, R for scientists) are more competitive.


## 2. How are in-demand skills trending for Data Analysis ? 

## Visualize Data 


```Python 

df_DA_plot= df_US_top_skills_percentage.iloc[:, :5]
sns.lineplot(data=df_DA_plot , markers=True, dashes=False, palette="tab10")
sns.set_theme(style="ticks")
plt.ylabel('likelihood in Job Postings')
plt.xlabel('2023 Months')
plt.title('Trending of top Skills for Data Analyst Jobs in the US ')

from matplotlib.ticker import PercentFormatter
ax= plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))


plt.show()
```
## Result 
**Bar graph visualizing the trending top skills for data analysis in US in 2023

![Trending skills for Data Analysis](2_projectLucasPython\Images\image_skills_trending.png)

## 📊 Top Skill Trends by Month

### 1. **SQL dominates consistently**
- SQL is the most in-demand skill throughout all months.
- Its likelihood in job postings remains high, ranging from **50% to 55%**.
- This suggests SQL is a **core requirement** for data analyst roles in the US.

### 2. **Excel holds strong as a secondary skill**
- Excel consistently ranks second, with a likelihood between **40% and 45%**.
- Indicates that **spreadsheet proficiency** is still highly valued, especially for reporting and data manipulation.

### 3. **Python and Tableau show similar mid-tier demand**
- Both fluctuate around **25% to 30%**.
- Python is essential for **data analysis and automation**, while Tableau is key for **visualization and dashboarding**.
- Their parallel trends suggest that employers often seek **either or both**, depending on the role’s focus.

### 4. **SAS is the least demanded among the five**
- SAS stays around **20% to 22%**, with minimal fluctuation.
- This reflects a **declining preference** for SAS in favor of open-source tools like Python and SQL.


## 📈 Strategic Takeaways

- **SQL and Excel** are foundational — mastering these gives you broad access to data analyst roles.
- **Python and Tableau** are differentiators — they boost your profile for more technical or visualization-heavy roles.
- **SAS** may be relevant in niche industries (like healthcare or finance), but it's no longer mainstream.

## 3. How well do jobs and skills pay for data ?
### 3.1 Salary analysis for Data Nerds 
### Visualize data 
```python
sns.boxplot(data=df_us_top_jobs, x='salary_year_avg', y='job_title_short', order=df_us_top_jobs_ordered )
sns.despine()
sns.set_theme(style="ticks")

plt.xlabel('Average Yearly Salary (USD)')
plt.ylabel('')
plt.title('Salary Distribution for Top 6 Job Titles in the US')
plt.xlim(0, 600000)
ticks_x= plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}k')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```
### Result 

![top paying jobs for Data Nerds](2_projectLucasPython\Images\image_salary_analysis.png)

*Box plot visualizing the salary distribution for the top 6 job titles.*

### Insights 

### 📊 **1. Salary Hierarchy Across Roles**
- **Top Earners**: *Senior Data Engineers* have the highest median and overall salary range, with some outliers reaching close to $600k.
- **Mid-Tier Roles**: *Data Scientists* and *Software Engineers* follow closely, showing competitive compensation but with slightly lower medians and fewer extreme outliers.
- **Lower Tier**: *Business Analysts* and *Data Analysts* have the lowest salary ranges and medians, indicating these roles are typically entry-level or less technical.


### 📈 **2. Salary Spread and Variability**
- **Wide Distribution**: *Senior Data Engineers* and *Software Engineers* show a broad interquartile range (IQR), suggesting significant variability in pay based on experience, location, or company.
- **Tight Distribution**: *Data Analysts* and *Business Analysts* have narrower boxes, indicating more consistent salaries across the industry.


### 🧭 **3. Strategic Career Planning**
- For professionals aiming for higher compensation, transitioning from *Data Analyst* or *Business Analyst* roles into *Data Engineering* or *Data Science* could be a lucrative path.
- The chart also highlights the value of specialization and seniority in boosting earning potential.

### 3.2 Highest paid & in-demand skills for Data
### Visualize Data
```python 
fig, ax = plt.subplots(2, 1)  

sns.set_theme(style='ticks')

# Top 10 Highest Paid Skills for Data Analysts
sns.barplot(data=df_DA_us_top_pay, x='median', y=df_DA_us_top_pay.index, hue='median', ax=ax[0], palette='dark:b_r')
ax[0].legend().remove()
# original code:
# df_DA_top_pay[::-1].plot(kind='barh', y='median', ax=ax[0], legend=False) 
ax[0].set_title('Top 10 Highest Paid Skills for Data Analysts')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

# Top 10 Most In-Demand Skills for Data Analystsr')
sns.barplot(data=df_DA_skills, x='median', y=df_DA_skills.index, hue='median', ax=ax[1], palette='light:b')
ax[1].legend().remove()
# original code:
# df_DA_skills[::-1].plot(kind='barh', y='median', ax=ax[1], legend=False)
ax[1].set_title('Top 10 Most In-Demand Skills for Data Analysts')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary (USD)')
ax[1].set_xlim(ax[0].get_xlim())  # Set the same x-axis limits as the first plot
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

plt.tight_layout()
plt.show()

```

### Result 
![highest and in-demand skills for Data Analysis in US](2_projectLucasPython\Images\image_highestPaid_and_InDemand_skills.png)

*Two separate bar graphs visualizing the highest and in-demand skills for Data Analysis in US.*

### Insights 

## 🧠 Strategic Takeaways

- **High Pay ≠ High Demand**: Skills like *solidity* or *hugging face* are rare and specialized, leading to higher pay but lower demand.
- **High Demand = Core Skills**: Skills like *python*, *SQL*, and *tableau* are must-haves but don’t necessarily lead to top-tier salaries.
- **Career Strategy**: Master core skills to get hired, then layer in niche or emerging tech (e.g., NLP, blockchain, NoSQL) to boost salary potential.

## 4 What are the most optimal skills to learn for Data Analysts?
To identify the most optimal skills to learn ( the ones that are the highest paid and highest in demand) I calculated the percent of skill demand and the median salary of these skills. To easily identify which are the most optimal skills to learn.

### View my notebook with detailed steps here: 5_Optimal_Skills.

## Visualize Data

```python 
from adjustText import adjust_text

df_DA_skills.plot(kind='scatter', x='skills_percent', y='salary_year_median')

# Prepare texts for adjustText
texts = []
for i, txt in enumerate(df_DA_skills.index):
    texts.append(plt.text(df_DA_skills['skills_percent'].iloc[i], df_DA_skills['salary_year_median'].iloc[i], txt))

# Adjust text to avoid overlap
adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray'))

# Set axis labels, title, and legend
plt.xlabel('Percent of data analyst jobs')
plt.ylabel('Median Yearly Salary')
plt.title('Most optimal skills for data analysts in the US')

ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, loc: f'${int(y/1000)}k'))
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, loc: f'{int(x)}%'))
# Adjust layout and display plot 
plt.tight_layout()
plt.show()
```
### Results

![Most Optimal Skills for Data Analysts in the US](2_projectLucasPython\Images\image_optimal_skills.png)

A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US with color labels for technology.

Insights:

- Skills such as Python, Tableau, and SQL Server are towards the higher end of the salary spectrum while also being fairly common in job listings, indicating that proficiency in these tools can lead to good opportunities in data analytics. 
- More commonly required skills like Excel and SQL have a large presence in job listings but lower median salaries compared to specialized skills like Python and Tableau, which not only have higher salaries but are also moderately prevalent in job listings.

- The scatter plot shows that most of the programming skills tend to cluster at higher salary levels compared to other categories, indicating that programming expertise might offer greater salary benefits within the data analytics field. 
- Analyst tools, including Tableau and Power BI, are prevalent in job postings and offer competitive salaries, showing that visualization and data analysis software are crucial for current data roles. This category not only has good salaries but is also versatile across different types of data tasks.

## What I Learned

Throughout this project, I deepened my understanding of the data analyst job market and enhanced my technical skills in Python, especially in data manipulation and visualization. Here are a few specific things I learned:

Advanced Python Usage: Utilizing libraries such as Pandas for data manipulation, Seaborn and Matplotlib for data visualization, and other libraries helped me perform complex data analysis tasks more efficiently.
Data Cleaning Importance: I learned that thorough data cleaning and preparation are crucial before any analysis can be conducted, ensuring the accuracy of insights derived from the data.
Strategic Skill Analysis: The project emphasized the importance of aligning one's skills with market demand. Understanding the relationship between skill demand, salary, and job availability allows for more strategic career planning in the tech industry.

## Insights

This project provided several general insights into the data job market for analysts:

Skill Demand and Salary Correlation: There is a clear correlation between the demand for specific skills and the salaries these skills command. Advanced and specialized skills like Python and Oracle often lead to higher salaries.
Market Trends: There are changing trends in skill demand, highlighting the dynamic nature of the data job market. Keeping up with these trends is essential for career growth in data analytics.
Economic Value of Skills: Understanding which skills are both in-demand and well-compensated can guide data analysts in prioritizing learning to maximize their economic returns.

## Challenges I Faced
This project was not without its challenges, but it provided good learning opportunities:

 - Data Inconsistencies: Handling missing or inconsistent data entries requires careful consideration and thorough data-cleaning techniques to ensure the integrity of the analysis.
 - Complex Data Visualization: Designing effective visual representations of complex datasets was challenging but critical for conveying insights clearly and compellingly.
 - Balancing Breadth and Depth: Deciding how deeply to dive into each analysis while maintaining a broad overview of the data landscape required constant balancing to ensure comprehensive coverage without getting lost in details.

## Conclusion

This exploration into the data analyst job market has been incredibly informative, highlighting the critical skills and trends that shape this evolving field. The insights I got enhance my understanding and provide actionable guidance for anyone looking to advance their career in data analytics. As the market continues to change, ongoing analysis will be essential to stay ahead in data analytics. This project is a good foundation for future explorations and underscores the importance of continuous learning and adaptation in the data field. 