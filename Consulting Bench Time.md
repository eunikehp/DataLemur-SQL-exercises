# Consulting Bench Time

## Case

In consulting, being "on the bench" means you have a gap between two client engagements. 
Google wants to know how many days of bench time each consultant had in 2021. 
Assume that each consultant is only staffed to one consulting engagement at a time.

Write a query to pull each employee ID and their total bench time in days during 2021.

Assumptions:

- All listed employees are current employees who were hired before 2021.
- The engagements in the consulting_engagements table are complete for the year 2022.

**staffing Table:**

<img width="200" alt="image" src="https://user-images.githubusercontent.com/104567399/188855663-708c2bb0-bc21-4e05-a782-dbb7611f58a6.png">


<img width="400" alt="image" src="https://user-images.githubusercontent.com/104567399/188857746-b84de45a-ce17-405c-a37a-09a38e2c06ac.png">



**consulting_engagements Table:**

<img width="200" alt="image" src="https://user-images.githubusercontent.com/104567399/188855820-8da392f1-ff58-4f48-ab70-df095ca22c47.png">

<img width="400" alt="image" src="https://user-images.githubusercontent.com/104567399/188857758-cea33966-fd36-4cb6-91e5-de181c021b84.png">


## Solution

To solve this, I first count the total work days of the employees in each job id. I also include the add one day as the last day of each job id.
Then, I calculate the bench days by substract those work days and last day by 365. Therefore, bench days will be found.

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


<img width="391" alt="image" src="https://user-images.githubusercontent.com/104567399/188855202-e30c839f-f0af-41d9-b596-2c8ff89b1973.png">

