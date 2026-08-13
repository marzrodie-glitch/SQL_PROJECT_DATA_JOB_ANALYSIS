# Introduction

Dive into the data job market! Focusing on the Data Analyst roles, this project explores top-paying jobs, in-demand skills, and where high demand meets high salary in data analytics.

SQL queries? Check them out here: [project_sql_folder](/project_sql/).

# Background

Driven by a request to navigate the data analyst job market more effectively, this project was born from a desire to pinpoint top-paid and in-demand skills, streamlining others work to find optimal jobs.

### The questions I wanted to answer through my SQL queries were:

1. What are the top-paying data analyst jobs?
2. What skills are required for these top-paying jobs?
3. What skills are the most in demand for data analysts?
4. Which skills are associated with higher salaries?
5. What are the most optimal skills to learn?

# Tools i used

For my deep dive into the data analyst job market, I harnessed the power of several key tools:

1. **SQL:** The backbone of this analysis, allowing me to query the database and unearth critical insights.
2. **PostgresSQL:** The chosen database management system, ideal for handling the job posting data
3. **Visual Studio Code:** My go-to for the database management and executing SQL queries.
4. **Git and GitHub:** Essential for version control and sharing my SQL scripts and analysis, ensuring collaboration and project tracking.

# The Analysis

Each query for this project aimed at investigating specific aspects of the data analyst job market.
Here is how I approached each question:

### 1. Top Paying Data Analyst jobs

To identify the highest-paying roles, I filtered Data Analyst positions by average yearly salary and location, focusing on remote jobs. This query highlights the high paying opportunities in the field.

```sql
SELECT
    job_id,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date,
    name AS company_name
FROM
    job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND
    job_location = 'Anywhere' AND
    salary_year_avg IS NOT NULL
ORDER BY
    salary_year_avg DESC
LIMIT 10
```

Here is the breakdown of the top data analyst jobs in 2023:

1. **Wide Salary Range:** Top 10 paying data analyst roles span from $184,000 to $650,000 indicating significant salary potential in the field.
2. **Diverse Employers:** Companies like Meta and AT&T are among those offering high salaries, showing a broad interest across different industries.
3. **Job Title Variety:** There is a high diversity in the job titles, from Data Analyst to Director of Analytics, reflecting varied roles and specializations within data analytics.

### 2. Skills for Top Paying Jobs

To understand what skills are required for the top-paying jobs, I joined the job postings with the skills data, providing insights into what employers value for high-compensation roles.

```sql

WITH top_paying_jobs AS (

        SELECT
            job_id,
            job_title,
            salary_year_avg,
            name AS company_name
        FROM
            job_postings_fact
        LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
        WHERE
            job_title_short = 'Data Analyst' AND
            job_location = 'Anywhere' AND
            salary_year_avg IS NOT NULL
        ORDER BY
            salary_year_avg DESC
        LIMIT 10
)

SELECT 
    top_paying_jobs.*,
    skills
FROM top_paying_jobs
INNER JOIN skills_job_dim ON top_paying_jobs.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
ORDER BY
    salary_year_avg DESC

```
Here is the breakdown of the most demanded skills for the top 10 highest paying data analyst jobs in 2023:

1. **SQL** is leading with a bold count of 8.
2. **Python** follows closely with a bold count of 7
3. **Tableau** is also highly sought after, with a bold count of 6. Other skills like R, Snowflake, Pandas, and Excel show varying degrees of demand


# What i learned
# Conclusions
