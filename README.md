# Pewlett-Hackard-Analysis
## Overview of the analysis
This analysis provides insight onto what employees are reaching retirement age and will be ending their careers with Pewleet Hackard. In order to avoid staff shortages the positions, that the soon to be retirees hold, will need to be filled by a younger generation. To transition these roles it would be advantageous to institute a mentorship program so that the experience and knowlege of those Pewlett Hackard employees, who are soon to be retired, will pass on to a suitable protiege. In doing so, it will be nessessary to identify the current employees who would be able to participate in a mentorship program as well as defining the number of employees who will soon be retired and the title they hold.
## Deliverable 1: The number of Retiring Employees by Title
### Results
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
[Deliverable 1.txt](https://github.com/MosleyJD65109/Pewlett-Hackard-Analysis/files/9174608/Deliverable.1.txt)
### First Query

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

![retirement_titles](https://user-images.githubusercontent.com/104540261/180622109-2bfcf5f6-2388-440d-b8e3-02afcc2ff877.png)

This query will return columns listing the first names, last names, titles, from dates, and to dates of employees from the employees table. It will only return the employees who were born between the years 1952 and 1955 and order them by employee number. This gives us an acquarite idea of those employees who are set to retire.
![unique_titles](https://user-images.githubusercontent.com/104540261/180622111-47bdb654-7b16-43d2-853f-829587051498.png)

![retiring_titles](https://user-images.githubusercontent.com/104540261/180622116-7d5ccf78-39ed-48d7-b0c5-27c6b01b6fcb.png)



## Deliverable 2: The Employees Eligible for the Mentorship Program
## Summary
