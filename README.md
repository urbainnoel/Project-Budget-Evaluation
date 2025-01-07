---
title: "Project Budget Evaluation"
author: "Data Analyst"
date: "`r Sys.Date()`"
output: html_document
---



## Overview

This analysis focuses on the project overview dashboard, which provides a comprehensive view of project budgets, departmental allocations, and employee details. The dashboard aims to help stakeholders understand the distribution of capital, project budgets, and the status of various projects across different departments.

## Introduction
This report presents an exploratory analysis of project budgets across departments. The goal is to assess budget distribution, project allocation, and departmental alignment with organizational goals.

## Key Performance Indicators (KPIs)
![Power BI Report](https://raw.githubusercontent.com/urbainnoel/Project-Budget-Evaluation/main/project_budget_evaluation.jpg)

### Capital and Project Budget

- **Total Capital:** $1.29M
- **Total Project Budget:** $570K

### Capital Allocation by Department

- **IT:** 15.79%
- **Sales:** 26.32%
- **Human Resources:** 18.42%
- **Marketing:** 20.18%
- **Engineering:** 19.3%

### Project Budget Status

- **Completed:** 35.96%
- **Upcoming:** 64.04%

### Departmental Goals and Budgets

| Department Name   | Department Goals                  | Sum of Project Cost | Sum of Salary Cost | Sum of 2-year Budget | Sum of Capital   |
|-------------------|-----------------------------------|---------------------|---------------------|----------------------|------------------|
| Engineering       | Develop new products              | 110,000 €           | 160,000 €           | 1,200,000 €          | 770,000.00 €     |
| Marketing         | Increase brand awareness          | 115,000 €           | 158,000 €           | 800,000 €            | 369,000.00 €     |
| Sales             | Boost sales                      | 150,000 €           | 167,000 €           | 600,000 €            | 116,000.00 €     |
| IT                | Improve IT infrastructure         | 90,000 €            | 151,000 €           | 450,000 €            | 58,000.00 €      |
| Human Resources   | Enhance employee engagement      | 105,000 €           | 160,000 €           | 400,000 €            | (525,000.00) €   |
| **Total**         |                                   | **570,000 €**        | **796,000 €**       | **3,450,000 €**      | **1,288,000.00 €**|

### Project Budgets

- **Sum of Project Budget:** 570K
- **Project Budgets by Department:**
  - **Sales:** 150K
  - **Marketing:** 115K
  - **Engineering:** 110K
  - **Human Resources:** 105K
  - **IT:** 90K

### Employee Details

- **Employee ID:** 1003
- **First Name:** Michael
- **Last Name:** Johnson
- **Job Title:** Data Scientist
- **Department Name:** Sales
- **Compensation:** $95K

## SQL Query for Data Extraction

The following SQL query is used to extract and calculate the necessary data for analysis:

```sql
-- project_status
WITH project_status AS (
    SELECT
        project_id,
        project_name,
        project_budget,
        'upcoming' AS status
    FROM [upcoming projects]
    UNION ALL
    SELECT
        project_id,
        project_name,
        project_budget,
        'completed' AS status
    FROM completed_projects
)

-- big table
SELECT
    e.employee_id,
    e.first_name,
    e.last_name,
    e.job_title,
    e.salary,
    d.Department_name,
    d.Department_Budget,
    d.Department_Goals,
    pa.project_id,
    ps.project_name,
    ps.project_budget,
    ps.status
FROM employees e
-- JOIN Head_Shots h
-- ON e.employee_id = h.Employee_ID
JOIN departments d
ON e.department_id = d.Department_ID
JOIN project_assignments pa
ON pa.employee_id = e.employee_id
JOIN project_status ps
ON pa.project_id = ps.project_id;
```

## Conclusion

The analysis reveals that the project overview dashboard provides a clear and concise view of the capital allocation, project budgets, and departmental goals. The majority of the project budget is allocated to the Sales department, followed by Marketing and Engineering. The Human Resources department has a negative capital allocation, which may require further investigation. The dashboard also highlights the status of various projects, with a significant portion being upcoming. These insights can be used to optimize resource allocation, prioritize projects, and ensure alignment with departmental goals.
