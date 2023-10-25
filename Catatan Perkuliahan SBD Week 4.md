## 📘 SISTEM BASIS DATA

### 🗓️ Week 4: Intro to SQL (2)

#### 📍 Definition clausa
- used to perform calculations on a group of rows, returning a single result
- operate on sets of rows as described by the query and are often used in conjunction with the GROUP BY clause to group rows that have the same values in specified columns.
- often used to summarize and analyze data

select *
from instructor;

select min(salary)
from instructor;

select max(salary)
from instructor;

select *
from department;

select sum(budget)
from department;
Image
select dept_name, avg(salary) as avg_salary
from instructor
group by dept_name
Image
select dept_name, count(dept_name) as inst_dept
from instructor
group by dept_name

#### 📍 Sum and Count
- sum for counting numbers
- count for counting the amount of something

sum:
select building, sum(budget) as budget_build
from department
group by building

count:
select building, count(budget) as budget_build
from department
group by building
Image
Image
HAVING filters out the groups based on certain criteria or conditions
note: predicates in the having clause are applied after the formation of groups whereas predicated in the where clause are applied before forming groups
example: finding the names and avg salaries of all departments whose avg salary is greater than 65000

select dept_name, avg(salary) as avg_salary
from instructor
group by dept_name
having avg(salary) > 65000
Image
example of how where and having are similar

select dept_name, avg(salary) as avg_salary
from instructor
group by dept_name
having dept_name = 'Biology'

#### 📍 Set membership
to check if a specific value exists within a set of values
using the IN clause, we can filter results to only those roles

--find courses offered in Fall 2017 and in Spring 2018
select distinct course_id
from section
where semester = 'Fall' and year=2017
and course_id in(select course_id
                from section
                where semester = 'Spring' and year=2018)

-- find courses offered in Fall 2017 but not in Spring 2018
select distinct course_id
from section
where semester = 'Fall' and year=2017
and course_id not in(select course_id
                from section
                where semester = 'Spring' and year=2018);

select course_id, semester, year
from section;

--no result--
select distinct course_id
from section
where semester = 'Summer' and year=2017
and course_id in(select course_id
                from section
                where semester = 'Summer' and year=2018);

--has result--
select distinct course_id, semester, year
from section
where semester = 'Summer' and year=2017
and course_id not in(select course_id
                from section
                where semester = 'Summer' and year=2018);

--no result--
select distinct course_id
from section
where semester = 'Summer' and year=2018
and course_id in(select course_id
                from section
                where semester = 'Fall' and year=2017);

#### 📍 Set comparison
- this involves comparing the values in one set to the values in another set
- ex: we can check if a value in one table is > than all the values in a column of another table
- find names of instructors with salary greater than that of some (at least one( instructor in the biology department

select name 
from instructor
where salary > (select max(salary)
                    from instructor
                    where dept_name = 'Biology')

select name 
from instructor
where salary > (select max(salary)
                    from instructor
                    where dept_name = 'Comp. Sci.')
--subquery atau subqueries

#### 📍 Exists clause
select course_id
from course as c
where exists (select *
              from teaches as t
              where t.course_id = c.course_id);

#### 📍 Not exists clause
--memeriksa apakah ada mata kuluah yang
--ada pada tabel courses dan juga
--sudah diajarkan (data ada di tabel teaches)
select course_id
from course as c
where not exists (select *
              from teaches as t
              where t.course_id = c.course_id); 
