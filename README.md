# 认识 MongoDB
历史 2007年10月，MongoDB由10gen团队所发展。2009年2月首度推出。它是一个非关系型数据库，高性能数据存和BSON（一种类json的一种二进制形式的存储格式,简称Binary JSON）数据结构是它的特点。
本人于2009年底开始接触 MongoDB，当时用它来实现一个跨平台的数据传输工具，后续接触更多是在 redis memcached mongodb 三者之间徘徊，有兴趣的可自行查阅相关资料，这里不多介绍。

# 与关系型数据库对比（MySQL）
这里用 MySQL 来做为关系型数据库的代表
## MySQL
- 步骤
    - 安装 MySQL
    - 启动数据库服务器
    - 连接数据库服务器
    - 新建数据库，一台数据库服务器可新建多个数据库
    - 切换到要操作的数据库，可进行表的新建、修改、删除操作。一个数据库可以有多张表
    - 对当前数据库的表进行记录的增、删、查、改操作
- 关系
    - 一台数据库服务器可对应多个数据库（一对多的关系）
    - 一个数据库可以有多张表（一对多的表关系）
    - 一张表可以对应多条表记录（一对的关系）

## MongoDB
- 步骤
    - 安装 MongoDB
        - [下载](http://www.mongodb.org/downloads)对应版本的安装文件
        - 双击安装下载好的安装文件完成安装，注意：安装路径尽量简单，不要有中文
    - 启动数据库服务器
        - 在安装目录的 bin 目录下打开命令窗口并执行命令 `mongod.exe --dbpath` 路径，注意：路径为手动创建的一个全新目录，如：E:\DB\MONGO\db，不要有中文
        - 可以在浏览器访问 http://127.0.0.1:27017/，访问成功则表示安装成功且已启动数据库服务
    - 连接数据库服务器
        - 在安装目录的 bin 目录下打开命令窗口并执行命令 `mongo.exe`
        - 命令运行成功会显示 MongoDB 的一些信息，并进入到 MongoDB 的操作命令窗口（数据库操作都会在这个命令窗口进行）
    - 新建数据库，一台数据库服务器可新建多个数据库
    - 切换到要操作的数据库，可进行集合的新建、删除操作。一个数据库可以有多个集合
    - 对当前数据库的集合进行文档的增、删、查、改操作
- 关系
    - 一台数据库服务器可对应多个数据库（一对多的关系）
    - 一个数据库可以有多个集合（一对多的表关系）
    - 一个集合可以对应多条个文档（一对的关系）

除了在步骤上的对比，MongoDB 没有表和记录的概念，取而代之的是集合和文档。

# MongoDB 配置成服务
在上面步骤中，对启动和连接数据库服务器都要先打开安装目录下的 bin 目录再执行命令，显得非常麻烦。我们可以把上这两步配置成 windows 服务。
在这里以目录 E:\DB\MONGO\ 为例，注意：该目录是手动创建的全新目录。
1. 在 E:\DB\MONGO 新建目录文件夹 dblog
2. 在 E:\DB\MONGO 新建 mongod.cfg 的配置文件，文件内容如下：注意：配置中的两个目录是根据你配置文件所在目录相关
```
systemLog:
    destination: file
    path: E:\DB\MONGO\dblog\mongod.log
    logAppend: true
storage:
    journal:
        enabled: true
    dbPath: E:\DB\MONGO\db
net:
    port: 27017
```
3. 在 MongoDB 的安装目录下的 bin 目录打开命令窗口（以管理员权限）执行命令 `mongod.exe --config "E:\DB\MONGO\mongod.cfg" --install`
4. 配置成功的情况可以在命令窗口（以管理员权限）手动操作该服务
    - net start MongoDB 开户服务
    - net stop MongoDB 停止服务
    - sc delete MongoDB 删除服务
5. 配置成功的同时也可以在服务窗口找到对应的服务，服务名为 MongoDB，可设置为自动启动
6. 在启动服务的前提下，可以直接在命令窗口输入命令 `mongo` 便可直接进入 MongoDB 的命令操作窗口，无需要先跳转到 bin 目录

# MongoDB 操作
- [数据库操作](https://github.com/dk-lan/mongodb/tree/master/db)
- [文档操作](https://github.com/dk-lan/mongodb/tree/master/collection)
- 用户操作
- 复杂查询