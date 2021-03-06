**实验目的：**

\1.  掌握索引的基本概念。

\2.  掌握视图的基本概念。

\3.  掌握索引的可视化建立方法(菜单)。

\4.  掌握视图的可视化建立方法(菜单)。

 

**实验环境：**

\1.  硬件要求：微处理器Intel奔腾4，内存512M以上。

\2.  运行环境：Windows 7/8/10。

\3.  语言环境：SQL SERVER 2008及以上版本。

 

**实验内容与要求：**

 

请下载素材文件”成绩管理.rar”,解压后将其中的文件附加到数据库中,使用管理器(菜单)完成以下操作:

**一、索引：**

1.在tStud表中建立一个聚集、唯一索引"PK_index",索引字段为“学号”

2.在tStud表中增加一个记录，学号“1998101001”，姓名为“张三”，其余字段为null，将表关闭再打开，观察表中记录的排列情况。

3.在tStud表中，设置“学号”为主键，观察表中的索引情况（注意要刷新索引）。

4.在tScore表中，建立“学号”为索引字段的唯一索引“index_1”，观察能否建立，为什么？请选择正确的索引字段，建立该索引。

5.在教师表中，建立一个非聚集，非唯一索引“index_1”,索引字段为“性别、工作时间、职称”，要求首先按“职称”降序、然后按“工作时间”降序，最后按“性别”升序。

6.修改学生表中“PK_index”索引为非聚集索引，“PK_tStud”为聚集索引。

7.修改教师表中的索引“index_1”名称为“index_复合索引”

8.删除教师表中的索引“index_test”

**二、视图**

1.建立视图“课程”，含tCourse表中所有字段和所有记录，按学分降序排列。

2.建立视图“教授1”，含教师表的所有字段及2000年（含）之后参加工作的教授

3.建立视图“成绩1”，含tScore表中所有字段和成绩在区间[70，80]的记录，结果按成绩降序。

4.建立视图“退休教师名单”，含“编号，姓名，性别，年龄，职称，工作时间”六个字段和所有达到退休条件的教师（设退休条件为：年满60周岁的男职工和年满55周岁的女职工）

5.建立视图“学生成绩”，包括“学号、姓名、课程号、课程名、成绩”五个字段

6.建立视图“学生成绩统计”，包括“学号，姓名，最高分，最低分，平均分，总分，选课门数”等字段。

7.建立视图“学生学分”，包括“学号，姓名，总学分”等字段（注意只有课程及格才可以获得该课程的学分）

8.建立视图“未选课学生”，包括tStud表中所有字段。

**请将分离后的主数据文件”****成绩管理.mdf”****和日志文件”****成绩管理.ldf”****上传**