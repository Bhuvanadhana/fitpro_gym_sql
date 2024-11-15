
# FitPro Gym SQL Project


Welcome to my first SQL project, where I analyze real-time gym data from **FitPro Gym**! This project uses a dataset of **10,000 visit records** to explore and analyze gym membership and visit data, answering key business questions that can help a fitness center understand its customer base better and optimize its services.

## Table of Contents
- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Business Problems](#business-problems)
- [SQL Queries & Analysis](#sql-queries--analysis)
- [Getting Started](#getting-started)
- [Questions & Feedback](#questions--feedback)
- [Contact Me](#contact-me)

---

## Introduction

This project aims to demonstrate essential SQL skills by analyzing a dataset from FitPro Gym. Using SQL, I explored membership details, member demographics, and visit patterns to derive actionable insights. This project showcases fundamental SQL techniques, including creating tables, writing queries, and analyzing data.

## Project Structure

1. **SQL Scripts**: Code to create the database schema and queries for analysis.
2. **Dataset**: Real-time data on gym visits, membership, and member demographics.
3. **Analysis**: SQL queries solving practical business problems, each one crafted to address specific questions.

---

## Database Schema

Here’s an overview of the database structure:

### 1. **Members Table**
- **member_id**: Unique identifier for each member
- **name**: Name of the member

### 2. **Memberships Table**
- **member_id**: Unique identifier linked to the `members` table
- **age**: Age of the member
- **gender**: Gender of the member ('M' or 'F')
- **membership_type**: Type of membership (e.g., Monthly, Quarterly)
- **join_date**: Date when the member joined
- **status**: Membership status (e.g., Active, Cancelled)

### 3. **Visits Table**
- **visit_id**: Unique identifier for each visit
- **member_id**: Linked to the `members` table
- **visit_date**: Date of the visit
- **check_in_time**: Check-in time of the visit
- **check_out_time**: Check-out time of the visit

## Business Problems

The following queries were created to solve specific business questions. Each query is designed to provide insights based on gym membership and visit data.

1.Retrieve all details of members who have a Cancelled membership.
```sql
select * from memberships
where status='Cancelled'
```
2.Find all members who are Male and have a Weekly membership type, and order the result by join_date.
```sql
select * from memberships 
where gender='M' and membership_type ='Weekly'
order by join_date
```

3.Get a list of distinct member ages.
```sql
select distinct age from memberships
```

4.Retrieve the name, membership_type, and join_date of all members who joined after 2023-10-01, ordered by join_date in ascending order.
```sql
select m.name,membership_type,join_date 
from members m join memberships ms on ms.member_id=m.member_id
where join_date>'2023-10-01'
order by join_date
```
5.Count the total number of visits made by each member, grouping by member_id.
```sql
select member_id,count(*) as total_no_visits from visits
group by member_id
order by total_no_visits desc
```

6.Retrieve the membership_type and the count of members for each membership type.
```sql
select membership_type,count(*) from memberships
group by membership_type
```

7.Get the names and ages of members who have a Monthly membership and are younger than 25, using WHERE.
```sql
select m.name,ms.age from members m join memberships ms 
on ms.member_id=m.member_id
where membership_type='Monthly' and age <25;
```

8.Retrieve the number of visits for each visit_date, ordered by visit_date.
```sql
select visit_date,count(*) as visit_count from visits
group by visit_date
order by visit_date
```

9.Find the average age of members who have a Quarterly membership type.
```sql
select avg(age) as avg_age from memberships
where membership_type='Quaterly'
```

10.Retrieve the name, membership_type, and status of members who are Active and Monthly, ordered by status.
```sql
select name,membership_type,status from members m join memberships ms on
ms.member_id=m.member_id
where status='Active'and membership_type='Monthly'
order by status
```

11.Count the number of members with each membership_type, using GROUP BY and HAVING to show only those with more than 1 member.
```sql
select membership_type,count(*) as count_no from memberships
group by membership_type
having count(*)>1
```
12.Find the name of the member who has made the most visits, ordered by total_visits.
```sql
select m.name,count(v.visit_id) as total_visit from members m join visits v on v.member_id=m.member_id 
group by m.name
order by total_visit desc
limit 1
```
13.Retrieve the list of name and status of members who have Cancelled status and joined before 2023-11-01, and limit the result to 3 rows.
```sql
select m.name,ms.status from memberships ms join members m on m.member_id=ms.member_id
where status='Cancelled' and join_date < '2023-11-01'
limit 3
```
14.Find the average age of members with Active status, grouped by membership_type.
```sql
select membership_type,avg(age) as avg_age from memberships
where status='Active'
group by membership_type

```
15.Retrieve all visit details (date, check-in, check-out) for the first 5 visits, ordered by visit_date in descending order.
```sql
select visit_date,check_in_time,check_out_time from visits
order by visit_date desc
limit 5
```

---

## SQL Queries & Analysis

The `analysis.sql` file contains all SQL queries developed for this project. Each query corresponds to a business problem and demonstrates skills in SQL syntax, data filtering, aggregation, grouping, and ordering.

## Getting Started

### Prerequisites
- PostgreSQL (or any SQL-compatible database)
- Basic understanding of SQL

### Steps
1. **Clone the Repository**:
   ```bash
   git clone https://github.com/yourusername/fitpro-gym-sql-project.git
   ```
2. **Set Up the Database**:
   - Run the `schema.sql` script to set up tables and insert sample data.

3. **Run Queries**:
   - Execute each query in `analysis.sql` to explore and analyze the data.

---

## Questions & Feedback

If you have any questions or feedback, feel free to create an issue or reach out!

---
Contact Info:
itbhuvi@gmail.com
