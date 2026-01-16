The analysis

## 1. What are the most demanded skills for the top 3 most popular data roles ?

To find the most demanded skills for the most popular data roles. I filtered out those positions by which ones were the most popular, and got the top 5 skills for these top 3 roles. this query highligths the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my nootbook with detailed steps here : 
[2_Skills_demand.ipynb](2_projectLucasPython\2_Skills_demand.ipynb)

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

---

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

---