# Pewlett-Hackard-Analysis
## Overview of the analysis
This analysis provides insight onto what employees are reaching retirement age and will be ending their careers with Pewleet Hackard. In order to avoid staff shortages the positions, that the soon to be retirees hold, will need to be filled by a younger generation. To transition these roles it would be advantageous to institute a mentorship program so that the experience and knowlege of those Pewlett Hackard employees, who are soon to be retired, will pass on to a suitable protiege. In doing so, it will be nessessary to identify the current employees who would be able to participate in a mentorship program as well as defining the number of employees who will soon be retired and the title they hold.
## Deliverable 1: The number of Retiring Employees by Title
### Results
```
-- DELIVERABLE 1: The Number of Retiring Employees by Title
-- By Jeff Mosley
-- July, 2022

-- Follow the instructions below to complete Deliverable 1.
SELECT e.emp_no,
       e.first_name,
       e.last_name,
       t.title,
       t.from_date,
       t.to_date
INTO retirement_titles
FROM employees as e
INNER JOIN titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
order by e.emp_no;

-- Use Dictinct with Orderby to remove duplicate rows
SELECT DISTINCT ON (emp_no) emp_no,
first_name,
last_name,
title
INTO unique_titles
FROM retirement_titles
ORDER BY emp_no, title DESC;

-- Retrieve the number of employees by their most recent job title who are about to retire.
SELECT COUNT(ut.emp_no),
ut.title
-- INTO retiring_titles
FROM unique_titles as ut
GROUP BY title 
ORDER BY COUNT(title) DESC;
```

### First Query
```
SELECT e.emp_no,
       e.first_name,
       e.last_name,
       t.title,
       t.from_date,
       t.to_date
INTO retirement_titles
FROM employees as e
INNER JOIN titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1952-01-01' AND '1955-12-31')
order by e.emp_no;
```
![retirement_titles](https://user-images.githubusercontent.com/104540261/180622109-2bfcf5f6-2388-440d-b8e3-02afcc2ff877.png)

This query will return columns listing the first names, last names, titles, from dates, and to dates of employees from the employees table. It will only return the employees who were born between the years 1952 and 1955 and order them by employee number. This gives us an acquarite idea of those employees who are set to retire.

### Second Query

```
SELECT DISTINCT ON (emp_no) emp_no,
first_name,
last_name,
title
INTO unique_titles
FROM retirement_titles
ORDER BY emp_no, title DESC;
```
![unique_titles](https://user-images.githubusercontent.com/104540261/180622111-47bdb654-7b16-43d2-853f-829587051498.png)

This query uses the Dictinct command in combination with the groupby command to eliminate rows that contain the same information.It will return columns for first names, last names, and title from the retirement_title table and create a unique_titles table. The data for each new table created is exported to a csv file in the data folder of this project.
### Third Query
```
SELECT COUNT(ut.emp_no),
ut.title
INTO retiring_titles
FROM unique_titles as ut
GROUP BY title 
ORDER BY COUNT(title) DESC;
```

![retiring_titles](https://user-images.githubusercontent.com/104540261/180622116-7d5ccf78-39ed-48d7-b0c5-27c6b01b6fcb.png)

This query filters the employees who are about to retire by their job title. The filtered data form the unique_titles table is recreated in a new table entitled retiring_titles. The data from the new table is then exported into a csv file in the data folder.

## Deliverable 2: The Employees Eligible for the Mentorship Program

```
-- DELIVERABLE 2: The Employees Eligible for the Mentorship Program
-- By Jeff Mosley
-- July, 2022

-- Write a query to create a Mentorship Eligibility table that holds the employees who are eligible to participate in a mentorship program.
SELECT DISTINCT ON(e.emp_no) e.emp_no, 
    e.first_name, 
    e.last_name, 
    e.birth_date,
    de.from_date,
    de.to_date,
    t.title
INTO mentorship_eligibilty
FROM employees as e
Left outer Join dept_emp as de
ON (e.emp_no = de.emp_no)
Left outer Join titles as t
ON (e.emp_no = t.emp_no)
WHERE (e.birth_date BETWEEN '1965-01-01' AND '1965-12-31')
ORDER BY e.emp_no;
```
![mentorship_eligibility](https://user-images.githubusercontent.com/104540261/180623375-9938c77d-c959-4a99-825f-9db9d15f5f87.png)

This query displays employees who are eligible for the mentorship program. This query returns columns listing the first name, last name, birthdate, from date, to date, and title. The data is restructured from the employees table into a new table entitled mentorship_eligibilty. The data is then exported into a csv file in the data folder.
## Summary

Seeing the 63 % of the workforce is either retirment or mentorship eligible there will most likely be many positions to fill over the next 5-10 years. There may not exactly be enough people in the workforce to take care of the tasks or even come close to the amount of experience to fill these roles so quickly but what companies can do is try to best learn about what these employees did to be so successful/ having such long lasting careers to continue the tradition for future employees. Most likely the future generation is more computer savy/ efficent due to technologies and can catch on quickly helping companies continue to trend in the right direction by keeping revenues up.

1) How many roles will need to be filled as the "silver tsunami" begins to make an impact?.

90,398 roles are in urgent need to be filled out as soon as the workforce starts retiring at any given time.

2) Are there enough qualified, retirement-ready employees in the departments to mentor the next generation of Pewlett Hackard employees?

No, we have 1,940 employees who are eligible to participate in a mentorship program.


