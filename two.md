一、三表联查，查找用户编号、昵称、真实姓名、组织编号、组织名称、身份类型

```sql
select user.uid, user.nick_name, user.real_name,
org_user.org_id,org.org_name,org_user.type
from user,org_user,org
where user.uid = org_user.uid and org.org_id = org_user.org_id;
```

![](D:\我的学习\数据库练习\第二天第一题.png)

二、通过左连接，查找用户的用户编号，昵称，真实姓名，组织编号，组织名称，还有身份类型，把没有国家的用户数据也显示出来

```sql
select user.uid, user.nick_name, user.real_name,
org_user.org_id,org.org_name,org_user.type
from user left JOIN org_user
on user.uid = org_user.uid left JOIN org on org.org_id = org_user.org_id;
```

![](D:\我的学习\数据库练习\第二天第二题.png)

三、通过右连接，查找用户的用户编号，昵称，真实姓名，组织编号，组织名称，还有身份类型，把没有国家的用户数据也显示出来

```sql
select user.uid, user.nick_name, user.real_name,
org_user.org_id,org.org_name,org_user.type
from user right JOIN org_user
on user.uid = org_user.uid right JOIN org on org.org_id = org_user.org_id;
```

![](D:\我的学习\数据库练习\第二天第三题.png)

四、三表联查，按国家进行分组，注意不要漏掉了没有关联任何用户的国家

```sql
SELECT
	count( USER.uid ) AS 总数,
	max( org.org_name ) as 国家
	
FROM
	USER left JOIN org_user ON USER.uid = org_user.uid
	right JOIN org on org.org_id = org_user.org_id
	 
GROUP BY
	org.org_name
```

![](D:\我的学习\数据库练习\第二天第四题.png)

五、三表联查，按国家进行分组，筛选出国家人数小于等于0的国家

```sql
SELECT
	count( USER.uid ) AS 总数,
	max( org.org_name ) as 国家
	
FROM
	USER  JOIN org_user ON USER.uid = org_user.uid
	RIGHT JOIN org on org.org_id = org_user.org_id
	 
GROUP BY
	org.org_name
HAVING 总数<=0
	
order by 总数 asc
```

![](D:\我的学习\数据库练习\第二天第五题.png)

六、三表联查，按国家进行分组，筛选出国家人数大于20的国家，并按人数倒序排列

```sql
SELECT
	count( USER.uid ) AS 总数,
	max( org.org_name ) as 国家
	
FROM
	USER  JOIN org_user ON USER.uid = org_user.uid
	RIGHT JOIN org on org.org_id = org_user.org_id
	 
GROUP BY
	org.org_name
HAVING 总数>20
	
order by 总数 desc
```

![](D:\我的学习\数据库练习\第二天第六题.png)

七、模拟登录场景，查询刘备用手机登录，需要从数据库查询到数据，包括头像，昵称，用户编号，密码字符串等

```sql
SELECT uid,avatar,`password`,nick_name from user where mobile = 17780008000;
```

![](D:\我的学习\数据库练习\第二天第七题.png)

八、因为刘备是君主，拥有查询到蜀国所有人的权限，模拟刘备查看蜀国所有人的语句(根据uid查询到org_id,再查询国家)

```sql
select org.org_id
from user right JOIN org_user
on user.uid = org_user.uid right JOIN org on org.org_id = org_user.org_id 
where user.uid=8000;

select *
from user right JOIN org_user
on user.uid = org_user.uid right JOIN org on org.org_id = org_user.org_id 
where org.org_id=8001;
```

![](D:\我的学习\数据库练习\第二天第八题.png)

九、因为刘备是君主，拥有查询到蜀国所有人的权限，模拟刘备查看关羽详细信息的语句

```sql
select org.org_id
from user right JOIN org_user
on user.uid = org_user.uid right JOIN org on org.org_id = org_user.org_id 
where user.uid=8000;

select *
from user right JOIN org_user
on user.uid = org_user.uid right JOIN org on org.org_id = org_user.org_id 
where org.org_id=8001 and user.nick_name = '关羽';
```

![](D:\我的学习\数据库练习\第二天第九题.png)
