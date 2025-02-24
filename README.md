# Customer Behavior Analysis
## Guided Data Analysis Project with 365 Data Science
#### To utilize my newly advanced SQL skills and refresh my Tableau and data analysis skills, I am following this guided project via Udemy. Think of it as a "warm up" for the rest of my portfolio. Let's begin!

### Project Overview

### Data Sources

### Tools
- MySQL - Data Analysis
- Tableau - Data Visualization

### Defining the Problem

### Collecting the Data
- Downloaded provided SQL file
- Opened SQL file in MySQL Workbench, then executed query to generate database
### Cleaning the Data
- Because the data is provided, it is assumed to be clean
### Data Analysis
- Explored database, familiarized self with table names and contents, and identified primary keys
- Created .csv file for Tableau by extracting data from database
#### Creating student engagement .csv
1. Extracted the following information from student_purchases to create table purchases_info
  - ID of purchase (purchase_id)
  - ID of student (student_id)
  - Purchase type (purchase_type)
  - Start Date (date_purchased)
  - End Date (derived using CASE, DATE_ADD, and MAKEDATE)
  - Refund Date (refund_date)
    - Used with IF statement to modify end_date when applicable
 ```sql
SELECT
	purchase_id,
    student_id,
    purchase_type,
    date_start,
    IF(date_refunded IS NULL, date_end, date_refunded) AS date_end
 FROM
(SELECT
	purchase_id,
    student_id,
    purchase_type,
    date_purchased AS date_start,
	CASE
		-- when purchase type is monthly
		WHEN purchase_type = 0 THEN
			DATE_ADD(MAKEDATE(YEAR(date_purchased), DAY(date_purchased)),
				INTERVAL MONTH(date_purchased) MONTH)
        -- when purchase type is quarterly       
		WHEN purchase_type = 1 THEN
			DATE_ADD(MAKEDATE(YEAR(date_purchased), DAY(date_purchased)),
				INTERVAL MONTH (date_purchased)+2 MONTH)
		-- when purchase type is annual
		WHEN purchase_type = 2 THEN
			DATE_ADD(MAKEDATE(YEAR(date_purchased), DAY(date_purchased)),
				INTERVAL MONTH(date_purchased)+11 MONTH)
    END AS date_end,
	date_refunded
FROM student_purchases) purchases_info;
```
2. Saved table with CREATE VIEW
3. 
### Data Visualization
