# Oracle

## 实验一：分析SQL执行计划，执行SQL语句的优化指导

实验内容：

对Oracle12c中的HR人力资源管理系统中的表进行查询与分析。
首先运行和分析教材中的样例：本训练任务目的是查询两个部门('IT'和'Sales')的部门总人数和平均工资，以下两个查询的结果是一样的。但效率不相同。
设计自己的查询语句，并作相应的分析，查询语句不能太简单。
教材中的查询语句

- 查询1：

SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
from hr.departments d，hr.employees e
where d.department_id = e.department_id
and d.department_name in ('IT'，'Sales')
GROUP BY department_name；

执行自动跟踪执行计划

![运行结果](https://github.com/1763301086/Oracle/blob/master/test1/1.png)

执行SQL语句的优化指导

![运行结果](https://github.com/1763301086/Oracle/blob/master/test1/5.png)

- 查询2：
SELECT d.department_name，count(e.job_id)as "部门总人数"，
avg(e.salary)as "平均工资"
FROM hr.departments d，hr.employees e
WHERE d.department_id = e.department_id
GROUP BY department_name
HAVING d.department_name in ('IT'，'Sales');

执行自动跟踪执行计划

![运行结果](https://github.com/1763301086/Oracle/blob/master/test1/3.png)

执行SQL语句的优化指导

![运行结果](https://github.com/1763301086/Oracle/blob/master/test1/6.png)

- 分析：我认为第二条查询语句比较优。因为第一条查询的查询条件需要对两张表进行两次查询，查出满足条件的数据后进行求和，求平均等操作，而第二条查询语句秩序查询一次，相当于生成了一张新的表，之后通过having语句进行过滤，所以总的查询数据变少了，速度也较快。但是根据第一条查询建议进行修改，设置适当的索引，让第一条的查询语句比第二条的查询语句更快。

自定义查询：查询所有工资大于5000的员工，，显示其信息，通过设置查询条件
SELECT  d.department_name as "部门",e.FIRST_NAME as 姓名 ,e.SALARY as 工资
FROM hr.departments d,hr.employees e
WHERE d.department_id = e.department_id
and e.SALARY>5000

![运行结果](https://github.com/1763301086/Oracle/blob/master/test1/2.png)


