# 实验4：图书管理系统顺序图绘制
学号 | 班级 | 姓名
------ | -----  | ------
201710414123 |  软工一班 | 许瑞峰 
## 图书管理系统的顺序图
### 1. 借书用例
---
#### 1.1. 借书用例PlantUML源码
---
```
@startuml
skinparam sequenceParticipant underline
actor "：Librarian"
activate "：Librarian"

"：Librarian" ->"：Reader":verifyReaders()
activate "：Reader"
deactivate "：Reader"
"：Librarian" ->"：Reader":getInformation()

activate "：Reader"
deactivate "：Reader"
"：Librarian" ->"：Resource":getResource()
activate "：Resource"
"：Resource" -> "：Collection":queryResKinds()
activate "：Collection"
deactivate "：Collection"
deactivate "：Resource"

"：Librarian" ->"：BorrowRecord":creaLendRecords()
activate "：BorrowRecord"
deactivate "：BorrowRecord"
"：Librarian" ->"：Resource":lendResource()
activate "：Resource"

"：Resource" ->"：Collection":reduceBorrNum()
activate "：Collection"
deactivate "：Collection"
deactivate "：Resource"
"：Librarian" ->"：Reader":reduceMaxLend()
activate "：Reader"
deactivate "：Reader"

"：Librarian"->"：BorrowRecord":printlendList()
activate "：BorrowRecord"
deactivate "：BorrowRecord"
deactivate "：Librarian"
@enduml
```
#### 1.2. 借书用例顺序图
---
![brrow.png](https://img-blog.csdnimg.cn/20200412204922286.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0dyZWVuQmlyZFo=,size_16,color_FFFFFF,t_70#pic_center)
#### 1.3. 借书用例顺序图说明
---
1. 由图书管理员验证读者身份
2. 读者身份验证成功后，图书管理员读取读者限制借书额度
3. 图书管理员获取读者借书所属资源项，并在资源项中查询所借数目的品种
4. 查询该数目存在后，创建借书记录
5. 图书管理员更新资源项，减少数目可借数量
6. 图书管理员减少读者可借书的额度
7. 图书管理员打印结束清单

***
### 2. 还书用例
---
#### 2.1. 还书用例PlantUML源码
---
```
@startuml
skinparam sequenceParticipant underline
actor "：Librarian"
activate "：Librarian"

"：Librarian"->"：Resource":readResInfo()
activate "：Resource"
"：Resource" ->"：BorrowRecord":getLendRecord()
activate "：BorrowRecord"
deactivate "：BorrowRecord"
"：Resource"->"：Collection":getResKinds()
activate "：Collection"
deactivate "：Collection"
deactivate "：Resource"

"：Librarian" ->"：Reader":getReaderInfo()
activate "：Reader"
deactivate "：Reader"
"：Librarian" ->"：Resource":returnRes()
activate "：Resource"

"：Resource" ->"：Collection":addLendNum()
activate "：Collection"
deactivate "：Collection"
deactivate "：Resource"


"：Librarian" ->"：BorrowRecord":recordDate()
activate "：BorrowRecord"
deactivate "：BorrowRecord"
"：Librarian" ->"：OverdueTreat":registrationOverdue()
activate "：OverdueTreat"
deactivate "：OverdueTreat"
deactivate "：Librarian"
@enduml
```
#### 2.2. 还书用例顺序图
---
![return.png](https://img-blog.csdnimg.cn/20200412210000691.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0dyZWVuQmlyZFo=,size_16,color_FFFFFF,t_70#pic_center)
#### 2.3. 还书用例顺序图说明
---
1. 图书管理员读取资源信息，从资源相中查询读者的结束记录，并查询书目所属类别
2. 图书管理员获取读者的借阅信息
3. 图书管理员在资源项中归还书目，并增加馆藏该书可借数量
4. 图书管理员登记还书日期
5. 图书管理员登记读者逾期记录

***



 
