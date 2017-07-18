# 数据库操作
进入 MongoDB 命令操作窗口执行命令
- 在安装目录的 bin 目录下执行命令 `mongo` 可连接到数据库并可进行操作
- 已配置 windows 服务的直接在启动服务的前提下，在命令操作直接执行命令 `mongo`

## 命令
- help：可以看到 MongoDB 的基本操作命令
- db.getName()：查看当前使用的数据库 
- db：查看当前使用的数据库，效果等同于 db.getName()
- db.states：查看当前 db 的链接机器地址
- use dbname：新建或切换数据库，dbname 为数据名称，如果数据库不存在，则创建数据库，否则切换到指定数据库。
- db.dropDatabase()：删除当前使用数据库