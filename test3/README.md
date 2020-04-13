# 实验3：图书管理系统领域对象建模

| 学号         | 班级         | 姓名     |       
| ------------ | ------------ | -------- | 
| 201710414123 | 软工一班| 许瑞峰 | 

## 1. 图书管理系统的类图
-----
### 1.1 类图PlantUML源码如下：

```
@startuml



class OPAC
{
   -ArrayList<ResKind> resKind
 {method} +ResKind[] setResKind(ArrayList<ResKind>  res)
{method} +ResKind[] getResKind(ArrayList<ResKind> res)
}

class ResKind{
-resName
-ISBN
-price
-BrifeIntro
-num
-availbale
{method} +void setResName()
{method} +void getResName()
{method} +void setISBN()
{method} +void getISBN()
{method} +void setPrice()
{method} +void getPrice()
{method} +void setBrifeIntro()
{method} +void getBrifeIntro()
{method} +void setNum()
{method} +void getNum()
{method} +void setAvailbale()
{method} +void getAvailbale()

}
OPAC "1" -- "1..*" ResKind


class ReserveRecord{
-reserveDate
{method} +void setReserveDate()
{method} +void getReserveDate()
}
ResKind "1" -- "*" ReserveRecord:hasReserved


class Reader{
-userName
-idCard
-borrowNum
-bookMax
-bookBorrow
-discMax
-discBorrow
{method} +void setUserName()
{method} +void getUserName()
{method} +void setIdCard()
{method} +void getIdCard()
{method} +void setBorrowNum()
{method} +void getBorrowNum()
{method} +void setBookMax()
{method} +void getBookMax()
{method} +void setBookBorrow()
{method} +void getBookBorrow()
{method} +void setDiscMax()
{method} +void getDiscMax()
{method} +void setDiscBorrow()
{method} +void getDiscBorrow()

}

ReserveRecord "*" -- "1" Reader

class BorrowRecord{
-borrowDate
-backDate
{method} +void setBorrowDate()
{method} +void getBorrowDate()
{method} +void setBackDate()
{method} +void getBackDate()
}
Reader -- BorrowRecord


class ResOpt{
-saveNum
-status
{method} +void setSaveNum()
{method} +void getSaveNum()
{method} +void setStatus()
{method} +void getStatus()
}
BorrowRecord "0..1" --"1"ResOpt

ResOpt "*" --* "1" ResKind :possess


class DiscKind{
-disctype
-discnum
-madeCompany
{method} +void setDisctype()
{method} +void getDisctype()
{method} +void setDiscnum()
{method} +void getDiscnum()
{method} +void setMadeCompany()
{method} +void getMadeCompany()

}


class BookKind{
-author
-press
-pubDate
{method} +void setAuthor()
{method} +void getAuthor()
{method} +void setPress()
{method} +void getPress()
{method} +void setPubDate()
{method} +void getPubDate()
}
DiscKind --^ ResKind
BookKind  --^ ResKind


class BookManager{
-employeeId
-employeeName
{method} +void setEmployeeId()
{method} +void getEmployeeId()
{method} +void setEmployeeName()
{method} +void getEmployeeName()
}
BookManager  "1" -- "*" BorrowRecord:register


class OverdueRec{
-overdueDays
{method} +void setOverdueDays()
{method} +void getOverdueDays()
}
OverdueRec "0..1" -- "1" BorrowRecord


class FineDetails{
-fineNum
{method} +void setFineNum()
{method} +void getFineNum()

}
FineDetails "0..1" -- "*" OverdueRec
@enduml
```

###  1.2. 类图如下：
![UML1.png](https://img-blog.csdnimg.cn/20200413144634952.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0dyZWVuQmlyZFo=,size_16,color_FFFFFF,t_70)
### 1.3. 类图说明：

馆藏目录对馆藏资源品种是一对多的关系,含有多种馆藏资源品种 <br/>
馆藏资源品种对预定记录是一对多的关系，含有多条预定记录<br/>
预定记录对读者是多对一的关系，一位读者有多条预定记录<br/>
借书记录依赖于读者<br/>
资源项对借书记录是一对一的关系（0代表没有借过，1代表借过）<br/>
馆藏资源品种对资源项是一对多的组合关系，代表如果没有资源项，那么馆藏资源品种也不会存在，馆藏资源品种拥有很多资源项<br/>
碟片品种是对馆藏资源品种的继承和扩展<br/>
图书品种也是对馆藏资源品种的继承和扩展<br/>
图书管理员对借书记录是一对多的关系，代表图书管理员登记的借书记录可以有多条<br/>
逾期记录与借书记录是一对一的关系（借书记录只有逾期和不逾期两种情况）<br/>

## 2. 图书管理系统的对象图
***
### 2.1 类ResKind的对象图
#### 源码如下
```
@startuml
object ResKind
ResKind : resName = "classic movie"
ResKind : ISBN = 1613480020
ResKind : price=50.0
ResKind : BrifeIntro="about classic movie"
ResKind : num=20
ResKind : availbale=10
@enduml
```

### 对象图如下：
![UML2.png](https://img-blog.csdnimg.cn/20200413144703474.png)


### 2.2 类ReserveRecord的对象图
#### 源码如下
```
@startuml
object ReserveRecord
ReserveRecord : reserveDate = "2020-04-5"
@enduml
```

### 对象图如下：
![UML3.png](https://img-blog.csdnimg.cn/2020041314472384.png)


### 2.3 类Reader的对象图
#### 源码如下
```
@startuml
object Reader
Reader : userName="xrf"
Reader : idCard="0123"
Reader : borrowNum=2017
Reader : bookMax=40
Reader : bookBorrow=20
Reader : discMax=20
Reader : discBorrow=10
@enduml

```
### 对象图如下：
![UML4.png](https://img-blog.csdnimg.cn/20200413144738863.png)

### 2.4 类BorrowRecord的对象图
#### 源码如下
```
@startuml
object BorrowRecord
BorrowRecord : borrowDate="2020-04-5"
BorrowRecord : backDate="2020-05-5"
@enduml
```

### 对象图如下：
![UML5.png](https://img-blog.csdnimg.cn/20200413144755535.png)

### 2.5 类ResOpt的对象图
#### 源码如下
```
@startuml
object ResOpt
ResOpt : saveNum="201710414126"
ResOpt : status="available"
@enduml

```

### 对象图如下：
![UML6.png](https://img-blog.csdnimg.cn/20200413144810906.png)

### 2.6 类DiscKind的对象图
#### 源码如下
```
@startuml
object DiscKind
DiscKind : disctype="DVD"
DiscKind : discnum="66"
DiscKind : madeCompany="xiongmao"
@enduml
```

### 对象图如下：
![UML7.png](https://img-blog.csdnimg.cn/20200413144824669.png)


