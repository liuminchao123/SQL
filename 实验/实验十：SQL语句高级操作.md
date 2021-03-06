

**实验目的：**

1. 掌握SQL嵌套查询语句。
2. 掌握合并查询的语句。
3. 掌握带条件的分组查询语句。
4. 掌握各种综合查询的语句。

**实验环境：**

1. 硬件要求：微处理器Intel奔腾4，内存512M以上。
2. 运行环境：Windows 7/8/10。
3. 语言环境：SQL SERVER 2008及以上版本。

**实验内容与要求： **

```sql
-- 1.将素材中的数据库附加到SQL SERVER中，在C盘建立STSQL的文件夹，下列所有的查询文件均存入该文件夹中。


-- 2.新建查询，查询那些同学选修了3个以上的课程，显示学号和选修门数，将查询文件保存为st1.sql。
-- st1.sql
SELECT 学生信息.学号, COUNT(课程号) AS 选修门数
FROM 学生成绩, 学生信息
WHERE 学生信息.学号 = 学生成绩.学号
GROUP BY 学生信息.学号
HAVING COUNT(课程号) > 3


-- 3.新建查询，查询每个学生的成绩在80分以上的各有多少门，显示姓名和门数，将查询文件保存为st2.sql。
-- st2.sql
SELECT 姓名, COUNT(课程号) AS 门数
FROM 学生成绩, 学生信息
WHERE 学生信息.学号 = 学生成绩.学号 AND 课程号 IN 
	(SELECT 课程号
	 FROM 学生成绩
	 WHERE 成绩 > 80)
GROUP BY 姓名 
	 

-- 4.新建查询，查询所有课程的平均成绩比王永林平均分高的学生的学生名和平均成绩，将查询文件保存为st3.sql。
-- st3.sql
select 姓名 as 学生姓名,AVG(成绩) as 平均成绩 
from 学生信息,学生成绩
where 学生信息.学号=学生成绩.学号 
group by 姓名 
having AVG(成绩) > (select AVG(成绩) from 学生成绩,学生信息 where 学生信息.学号=学生成绩.学号 and 姓名='王永林') 


-- 5.新建查询，查询教师或学生的学号（或教师编号）、姓名、性别、政治面貌，第一个字段以编号显示，将查询文件保存为st4.sql。
-- st4.sql
(select 学号 as 编号,姓名,性别,政治面貌 from 学生信息)
union
(select 教师编号 as 编号,姓名,性别,政治面貌 from 教师信息)


-- 6.新建查询，查询入学分数在前25%同学选修哪些课程，显示姓名、课程名和成绩，将查询文件保存为st5.sql。
-- st5.sql
select 姓名,课程名,成绩 from 学生信息,学生成绩,课程信息
where 学生信息.学号 =学生成绩.学号 
and 学生成绩.课程号=课程信息.课程号
and 姓名 in
	(select top 25 percent 姓名 
	 from 学生信息 
	 order by 入学分数 desc)


-- 7.新建查询，查询大于入学分数平均值的男生的人数，将查询文件保存为st6.sql。
-- st6.sql
SELECT COUNT(姓名) AS 人数
FROM 学生信息
WHERE 入学分数 > (SELECT AVG(入学分数) FROM 学生信息 )
and 性别 = '男'


-- 8.新建查询，查询既有先修课，同时自己又是其他课的先修课的课程名，将查询文件保存为st7.sql。
-- st7.sql
select 课程名 from 课程信息
where 先修课 != 'NULL' 
intersect
select 先修课 as 课程名 from 课程信息
where 先修课 != 'NULL'


-- 9.新建查询，查询入学分数前3同学选修的所有课程中学生的学号、姓名和性别（双重嵌套），将查询文件保存为st8.sql。
-- st8.sql
select 学生信息.学号,姓名,性别 
from 学生信息,学生成绩
where 学生信息.学号=学生成绩.学号
and 课程号 in
	(select 课程号 
	 from 学生成绩
	 where 学号 in 
		 (select top 3 学号 
		  from 学生信息 
		  order by 入学分数 desc))
 

-- 10.新建查询，查询教师中工龄超过18年（包括）的未婚教师的姓名、工龄、结婚状态（婚否的别名）和院系名称，将查询文件保存为st9.sql。
-- st9.sql
select 姓名,YEAR(GETDATE())-YEAR(参加工作时间) as 工龄,婚否,学院名称 as 院系名称 
from 教师信息,学院信息 
where 学院信息.学院编码=教师信息.学院编码
and YEAR(GETDATE())-YEAR(参加工作时间)>18


-- 11.新建查询，查询哪些课程没有同学选，显示课程号和课程名，将查询文件保存为st10.sql。
-- st10.sql
select 课程号,课程名 
from 课程信息 
where not exists 
	(select * 
	 from 学生成绩 
	 where 学生成绩.课程号=课程信息.课程号)

-- 12.新建查询，查询最受学生欢迎（选课人数最多）的课程号、课程名，将查询文件保存为st11.sql。
-- st11.sql
select 课程号,课程名 
from 课程信息
where 课程号=
	(select top 1 课程号 
	 from 学生成绩 
	 group by 课程号 
	 order by COUNT(学号) desc)


-- 13.新建查询，查询在出生人数最多年份出生的学生学号、姓名和出生年年份，将查询文件保存为st12.sql。
-- st12.sql
select 学号,姓名,YEAR(出生日期) as 出生年份 
from  学生信息
where YEAR(出生日期)=
	(select top 1 YEAR(出生日期) 
	 from 学生信息 
	 group by YEAR(出生日期)
	 order by COUNT(YEAR(出生日期)) desc)
```

最后将STSQL压缩上传。

