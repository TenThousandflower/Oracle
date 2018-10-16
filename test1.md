### 查询语句1
~~~
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
~~~

### 查询语句2
~~~
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
~~~

### 自定义查询语句
~~~
SELECT department_name, count(job_id) as "部门总人数", avg(salary) as "平均工资"
FROM hr.employees e
JOIN
(SELECT d.department_id, d.department_name
FROM hr.departments d
WHERE d.department_name in ('IT', 'Sales'))
USING (department_id)
GROUP BY department_name;
~~~
