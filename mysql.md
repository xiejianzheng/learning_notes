# mysql类型说明

1. 十进制类型 decimal
decimal又叫十进制精确存储数值。
decimal经常用于存储金钱相关的数据。

定义一个decimal类型, 需要使用以下语法：
	
	列名  decimal(p, d)

	p是精度的意思。精度就是数值的有效数字的个数的。
	d是比例的意思。表示小数点后的有效位数个数。

# sql语法

1. 更新表字段

UPDATE <表名> SET <列名>=<值> WHERE <条件>

# 常见日期处理函数

curdate(), current_date()：

curdate() 会根据上下文返回两种不同类型的数据：

字符串数据：缺省返回，在字符串上下文中，格式为"YYYY-MM-DD"

数值数据：在数值计算上下文中返回，格式为 YYYYMMDD
