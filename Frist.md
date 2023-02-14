一、查询用户表的所有数据，显示所有列

```sql
select * from user;
```

![](D:\我的学习\数据库练习\查询所有列.png)

二、查询用户的所有数据，只显示 uid、user_name、nick_name、real_name、sex

```sql
select uid,user_name,nick_name,real_name,sex from user;
```

![](D:\我的学习\数据库练习\只显示5列.png)

三、采用汉字别名，查询用户表中所有的数据，只显示用户编号、用户名、昵称、真实姓名、性别

```sql
select uid as 用户编号,user_name as 用户名,nick_name as 真实姓名,real_name as 昵称,sex as 性别 from user;
```

![](D:\我的学习\数据库练习\起别名.png)

四、把性别转换成汉字，使用 case when 用法

```sql
select uid,user_name,nick_name,real_name,
(case sex when 1 Then '男' else '女' END) as 性别
from user;
```

![](D:\我的学习\数据库练习\性别用casewhen.png)

五、通过把姓和名提取出来，组合在一起

```sql
select uid,user_name,concat(left(nick_name,1),right(real_name,2)),
(case sex when 1 Then '男' else '女' END) as 性别
from user;
```

![](D:\我的学习\数据库练习\截左一.png)

六、查询用户表中前面的 10 条记录

```sql
select * from user limit 10;
```

![](D:\我的学习\数据库练习\前十.png)

七、查询所有男性

```sql
select * from user where sex = 1;
```

![](D:\我的学习\数据库练习\察南.png)

八、用汉字别名，查询用户表中所有数据，只显示前五项、并只查询男性的前五条记录

```sql
select uid as 用户编号,user_name as 用户名,nick_name as 真实姓名,real_name as 昵称,
(case sex when 1 Then '男' else '女' end) as 性别 from user
where sex = 1 limit 5;
```

![](D:\我的学习\数据库练习\第八题.png)

九、按照性别进行分组统计，统计每个性别的用户在表中的人数，分别使用 case 函数格式和 case 搜索函数形式

```sql
select sum(case sex when 1 Then 1 else 0 end) as 男,sum(case sex when 0 Then 1 else 0 end) as 女
 from user GROUP BY sex;
 select sum(case when sex= 1 Then 1 else 0 end) as 男,sum(case when sex= 0 Then 1 else 0 end) as 女
 from user GROUP BY sex;
```

![](D:\我的学习\数据库练习\第九题.png)

十、查找某个姓氏男性人数大于二的数据，站不考虑双姓

```sql
select left(nick_name,1) as frist from user
where sex =1
GROUP BY frist
HAVING count(*)>2;
```

![](D:\我的学习\数据库练习\第十题.png)
