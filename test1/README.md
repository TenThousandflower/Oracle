
### 查询语句1
~~~sql
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name;
~~~

### 查询语句2
~~~sql
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');
~~~

### 自定义查询语句
~~~sql
SELECT department_name, count(job_id) as "部门总人数", avg(salary) as "平均工资"
FROM hr.employees e
JOIN
(SELECT d.department_id, d.department_name
FROM hr.departments d
WHERE d.department_name in ('IT', 'Sales'))
USING (department_id)
GROUP BY department_name;
~~~
### 执行结果
- 查询语句1用时0.036秒，查询语句2用时0.06秒，自定义查询语句用时0.031秒。 所以我认为在前两个查询语句中最优的语句是查询语句1。
### 查询语句1分析
- 该语句首先执行了id查询d.department_id = e.department_id，然后查找department_name='IT'和department_name='Sales'的信息并找出job_id的个数然后显示出来，通过avg函数算出salary平均工资。使用group by提高了查询的效率。
### 自定义查询语句分析
- 该语句首先执行了id查询d.department_id = e.department_id，然后通过两个表相同名字的属性department_id的值的对比和department_name='IT'和department_name='Sales'条件找到需要的信息。再次说明使用group by可以提高查询的效率。
