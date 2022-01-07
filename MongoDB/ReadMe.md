# MongoDB

#### MongoDB 是非关系型数据库

[MongoDB 学习教程](https://www.runoob.com/mongodb/mongodb-tutorial.html)



#### 关系型数据库和非关系型数据库

#####  关系型数据库

表就是关系，或者说表与表之间存在关系

* 所有的关系型数据库都需要通过 `sql` 语言来操作
* 所有的关系型数据库在操作之前都需要设计表结构
* 而且数据表还支持约束
  * 唯一的
  * 主键
  * 非空
  * 默认值

##### 非关系型数据库

+ 非关系型数据库非常灵活

+ 有的关系型数据库就是 key-value 对

+ MongoDB 是长得最像关系型数据库的非关系型数据库

  + 数据库 》 数据库

  + 数据表 》 集合（数组）

  + 表记录 》 文档对象

    | SQL术语（概念） | MongoDB术语（概念） | 解释/说明                                    |
    | --------------- | ------------------- | -------------------------------------------- |
    | database        | database            | 数据库                                       |
    | table           | collection          | 数据库表/集合                                |
    | row             | document            | 数据记录行/文档                              |
    | column          | field               | 数据字段/域                                  |
    | index           | index               | 索引                                         |
    | table joins     |                     | 表链接，MongoDB不支持                        |
    | primary key     | primary key         | 主键，MongoDB自动将 _id <br />字段设置为主键 |

+ MongoDB 不需要设计表结构
+ 也就是说你可以任意的往里面存数据，没有结构性这么一说

####  安装MongoDB

* [MongoDB 下载地址](https://www.mongodb.com/try/download/community)，下载完成后按照提示安装即可
* 配置环境变量：安装完成后配置MongoDB环境变量
* 测试安装：打开 `cmd` 命令窗口，输入 `mongod --version` 按回车

#### 开启和关闭MongoDB

#####  启动：

`cmd` 命令窗口中输入 `mongod ` 敲回车键

```shell
# mongodb 默认使用执行 mongod 命令所处盘符根目录下的 /data/db 作为自己的数据存储目录
# 所以在第一次执行该命令之前先自己手动创建一个 /data/db (在执行命令的根目录下创建)
mongod
```

如果想要修改默认的数据存储目录，可以：

```shell
mongod --dbpath=数据存储目录路径
```



#####  关闭：

```shell
在开启服务的控制台，直接 ctrl+c 即可停止。
或者直接关闭开启服务的控制台也可以。
```



##### 连接：

在控制台（`cmd`）中输入 `mongo`  

```shell
# 改命令默认连接本机的 MongoDB 服务
mongo
```



##### 退出：

```shell
# 在连接状态输入 exit 退出连接
exit
```



##### 基本命令

+ `show dbs`
  + 查看显示所有数据库
+ `db`
  + 查看当前操作的数据库
+ `use 数据库名称`
  + 切换到指定的数据库（如果没有会新建，新建的数据库只有有数据时才会被 `show dbs` 显示）
+ 插入数据



