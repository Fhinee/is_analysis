# 实验4:图书管理顺序图
姓名：余盈瑾<br>
班级：15软工2班<br>
学号：201510414225<br>

## 1.借书用例
借书用例PlantUML代码：
```
@startuml
@startuml
actor admin

admin->图书管理系统:扥路
activate 图书管理系统

图书管理系统->借书界面:menu()
deactivate 图书管理系统

借书界面->借书:借书
activate 借书界面
deactivate 借书界面
actor 读者
借书->读者:获取读者信息
activate 借书
activate 读者

读者->借书:返回是否符合借书条件
deactivate 读者
借书->书目:获取书目信息
deactivate 借书

借书 ->预订:查看图书是否被预定
activate 预订
预订->借书 :可借
activate 借书
deactivate 预订

借书->书:创建借书记录
activate 书
deactivate 书
deactivate 借书
借书->借书界面:借书完成
@enduml
```
借书顺序图如下：<br>
![](borrow.png '描述')<br>

说明：<br>
1.读者借书通过管理员借书<br>
2.管理员首先确认读者状态是否能借书，就获取到书籍信息，查看书籍是否能借<br>
3.能借出去就创建借书记录并更新书籍信息

## 2.还书用例
还书用例PlantUML代码如下：
```aidl
@startuml
actor 读者
actor admin
读者->admin:提交
activate 读者
admin->图书管理系统:login()
activate admin

deactivate 读者
图书管理系统->还书界面:菜单
activate 还书界面
deactivate admin
deactivate 还书界面

还书界面->借书信息:输入编码或扫码
activate 还书界面
activate 借书信息
deactivate 还书界面
 deactivate 借书信息

借书信息->书目:获取书目
activate 借书信息
activate 书目
deactivate 借书信息
deactivate 书目

书目->还书界面:确认还书
activate 还书界面
activate 书目
deactivate 还书界面
deactivate 书目

还书界面->书目:更新书目
activate 还书界面
activate 书目
deactivate 还书界面
deactivate 书目

还书界面->借书:更新书目
activate 还书界面
activate 借书
deactivate 还书界面
deactivate 借书

借书->还书界面:还书完成
activate 借书
activate 还书界面
@enduml
```
还书顺序图如下：<br>
![](return.png '描述')<br>

还书说明：<br>
1.管理员进行书籍的扫描，获取书籍信息<br>
2.确认还书后跟新书目信息<br>

## 3.罚款用例
还书用例plantUML代码如下：<br>
```aidl
@startuml
actor admin
admin->借书信息:查询显示
activate admin
activate 借书信息
deactivate admin
deactivate 借书信息

借书信息->借书:显示超时未还书籍
activate 借书
activate 借书信息
deactivate 借书
deactivate 借书信息
actor 读者
借书信息->读者:提示罚款金额
activate 读者
activate 借书信息
deactivate 读者
deactivate 借书信息
读者->admin:提交罚款
activate 读者
activate admin
deactivate 读者
deactivate admin
admin->借书信息:更新信息
activate admin
activate 借书信息
deactivate 读者
deactivate admin
admin->借书:更新信息
activate admin
activate 借书
deactivate admin
deactivate 借书
@enduml
```
罚款顺序图如下：<br>
![](fine.png '描述')<br>

罚款说明：<br>
1.管理员查询借书记录中超时未还的记录<br>
2.读者提交罚款金额<br>
3.借书记录与书籍记录中更新信息