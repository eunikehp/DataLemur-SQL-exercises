# Consulting Bench Time

## Case

In consulting, being "on the bench" means you have a gap between two client engagements. 
Google wants to know how many days of bench time each consultant had in 2021. 
Assume that each consultant is only staffed to one consulting engagement at a time.

Write a query to pull each employee ID and their total bench time in days during 2021.

Assumptions:

-All listed employees are current employees who were hired before 2021.
-The engagements in the consulting_engagements table are complete for the year 2022.

staffing Table:



## Solution

```sql
WITH workdays AS (
  SELECT 
    st.employee_id , 
    SUM(ce.end_date-ce.start_date) AS workdays,
    COUNT(st.job_id) AS last_day
  FROM staffing AS st
  JOIN consulting_engagements AS ce
  ON st.job_id = ce.job_id
  WHERE is_consultant = 'true'
  GROUP BY employee_id)
SELECT employee_id, 365-SUM(workdays)- SUM(last_day) AS bench_days
FROM workdays
GROUP BY employee_id;
```
