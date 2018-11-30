
# Oracle

## 实验5：PL/SQL编程

####实验目的：
了解PL/SQL语言结构
了解PL/SQL变量和常量的声明和使用方法
学习条件语句的使用方法
学习分支语句的使用方法
学习循环语句的使用方法
学习常用的PL/SQL函数
学习包，过程，函数的用法。


####- 实验场景：
假设有一个生产某个产品的单位，单位接受网上订单进行产品的销售。通过实验模拟这个单位的部分信息：员工表，部门表，订单表，订单详单表。
本实验以实验四为基础


####实验内容：

创建一个包(Package)，包名是MyPack。
在MyPack中创建一个函数SaleAmount ，查询部门表，统计每个部门的销售总金额，每个部门的销售额是由该部门的员工(ORDERS.EMPLOYEE_ID)完成的销售额之和。函数SaleAmount要求输入的参数是部门号，输出部门的销售金额。
在MyPack中创建一个过程，在过程中使用游标，递归查询某个员工及其所有下属，子下属员工。过程的输入参数是员工号，输出员工的ID,姓名，销售总金额。信息用dbms_output包中的put或者put_line函数。输出的员工信息用左添加空格的多少表示员工的层次（LEVEL）。比如下面显示5个员工的信息：
由于订单只是按日期分区的，上述统计是全表搜索，因此统计速度会比较慢，如何提高统计的速度呢？

####实验过程步骤
1.创建程序包，包含函数Get_SaleAmount和过程GET_EMPLOYEES
![运行结果](https://github.com/1763301086/Oracle/blob/master/test5/H{YKFNMC8SEY9IZN`D7VZ0L.png)

2.验证程序包正确性
![运行结果](https://github.com/1763301086/Oracle/blob/master/tes5/]{GUHUF_$6MJL6}8C@JZIT8.png)
![运行结果](https://github.com/1763301086/Oracle/blob/master/test5/}UGKO{VUA[KJR1$IRZ`@FRO.png)
3.由于订单只是按日期分区的，上述统计是全表搜索，因此统计速度会比较慢，如何提高统计的速度呢？
解决办法：
1、分页实现，分段循环；
2、开多个线程查询；
3、建立适当的索引
