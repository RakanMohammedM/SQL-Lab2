# SQL-Lab2

# We will use the Employees and Awards table below:

 <img src="Lab2.png" width="500" height="500">

### Q1: Choose all employees who have received an award (Nested Query)?
Query: 
```sql
SELECT id, name
FROM employee
where id IN (
  SELECT employee_id as employee_id_awards
  FROM awards
  WHERE employee_id_awards = employee.id
  );
```
Output:
<img src="https://github.com/RakanMohammedM/SQL-Lab2/blob/main/Q1.png" width="300" height="300">
 

### Q2: Choose all employees who have never received an award (Nested Query)?
Query: 
```sql
SELECT id, name, salary, role
FROM employee
where id not in (
  SELECT employee_id as employee_id_awards
  FROM awards
  WHERE employee_id_awards = employee.id
  );
```
`Another solution`
```sql
SELECT id, name
FROM employee
where Not EXISTS (
  SELECT employee_id
  FROM awards
  WHERE employee.id = awards.employee_id
  );
```
Output:
![img](C:\Users\mc872\Desktop\sql\SQL-Lab2-Pictures\Latest\Q2)
 
### Q3: Choose all Developers who make more than all Managers combined (Nested Query)?
Query: 
```sql
SELECT id, name, salary, role
FROM employee
where role = "Developer" and salary > (
  SELECT sum(salary)
  FROM employee
  WHERE role = "Manager"
  );
```
![img](C:\Users\mc872\Desktop\sql\SQL-Lab2-Pictures\Latest\Q3_1)
`Another solution`

```sql
SELECT id, name, salary, role
FROM employee
where role = "Developer" and salary > (
  SELECT salary
  FROM employee
  WHERE role = "Manager"
  );
```
Output:
![img](C:\Users\mc872\Desktop\sql\SQL-Lab2-Pictures\Latest\Q3_2)

 
### Q4: Choose all Developers who make more money than any Manager (Nested Query)?
Query:
```sql
SELECT id, name, salary, role
FROM employee
where role = "Developer" and salary > (
  SELECT max(salary)
  FROM employee
  WHERE role = "Manager"
  );
```
Output:
![img](C:\Users\mc872\Desktop\sql\SQL-Lab2-Pictures\Latest\Q4)
 
### Q5: Choose all employees whose salaries are higher than the average for their position. (Nested Query)?
Query: 
```sql
SELECT id, name, salary, role
FROM employee
where salary > (
  SELECT avg(salary)
  FROM employee
  );
```
Output:
![img](C:\Users\mc872\Desktop\sql\SQL-Lab2-Pictures\Latest\Q5)
