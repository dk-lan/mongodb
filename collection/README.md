# 文档操作
进入 MongoDB 命令操作窗口执行命令
- 在安装目录的 bin 目录下执行命令 `mongo` 可连接到数据库并可进行操作
- 已配置 windows 服务的直接在启动服务的前提下，在命令操作直接执行命令 `mongo`

MongoDB 集合可以相当于 MySQL 的表
MongoDB 文档可以相当于 MySQL 的表记录

## 命令
- db.getCollectionNames()：获取当前 db 的所有集合，以数组形式显示
- show collections：获取当前 db 的所有集合，以列表（换行）形式显示
- db.COLLECTION_NAME.insert(document)：插入文档
    - COLLECTION_NAME：集合名称（表名），若该集合不存在会自动创建
    - document：要插入的文档（记录），格式为 JSON 对象或者是数组对象
    - 示例对象：`db.account.insert({"name": "Lucy", "age": 20})`
    - 示例数组对象：`db.account.insert([{"name": "Tom", "age": 22}, {"name": "Sam", "age": 18}])`
- db.COLLECTION_NAME.find([condition])：查询文档
    - COLLECTION_NAME：集合名称（表名），若该集合不存在会自动创建
    - condition：条件，可选，如果没有条件为查找全部，条件格式为对象
    - 示例查找全部：`db.account.find()`
    - 示例条件查找：`db.account.find({"name": "Tom"})`
    - findOne() 方法，它只返回一个文档
    - 等于：{<key>:<value>} `db.account.find({"name":"Tom"})`
    - 小于：{<key>:{$lt:<value>}}	`db.account.find({"age":{$lt:20}})`
    - 小于或等于：{<key>:{$lte:<value>}}	`db.account.find({"age":{$lte:20}})`
    - 大于：{<key>:{$gt:<value>}}	`db.account.find({"age":{$gt:50}})`
    - 大于或等于：{<key>:{$gte:<value>}}	`db.account.find({"age":{$gte:50}})`
    - 不等于：{<key>:{$ne:<value>}}	`db.account.find({"age":{$ne:50}})`
    - and 条件：`db.account.find({"name": "Tom", "age": 22})`
    - or 条件：`db.account.find({$or:[{"name": "Tom"}, {"name": "Sam"}]})`
    - and 和 or 联合使用：`db.account.find({$or: [{name: "Tom"},{name: "Sam"}], age: 18})`
- db.COLLECTION_NAME.update(<query>, <update>, [options])：更新文档
    - query : update 的查询条件
    - update : update 的对象和一些更新的操作符（如$,$inc...）等
    - options
        - upsert : 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
        - multi : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
        - writeConcern :可选，抛出异常的级别。
    - 示例：
        - 将 age = 18 的文档更新为 age = 20：`db.account.update({age: 18}, {age: 20})`
        - 只更新第一条记录：`db.col.update( { "count" : { $gt : 1 } } , { $set : { "test2" : "OK"} } )`
        - 全部更新：`db.col.update( { "count" : { $gt : 3 } } , { $set : { "test2" : "OK"} },false,true )`
        - 只添加第一条：`db.col.update( { "count" : { $gt : 4 } } , { $set : { "test5" : "OK"} },true,false )`
        - 全部添加加进去: `db.col.update( { "count" : { $gt : 5 } } , { $set : { "test5" : "OK"} },true,true )`
        - 全部更新：`db.col.update( { "count" : { $gt : 15 } } , { $inc : { "count" : 1} },false,true )`
        - 只更新第一条记录：`db.col.update( { "count" : { $gt : 10 } } , { $inc : { "count" : 1} },false,false )`
-  db.COLLECTION_NAME.remove(<query>, [options])：删除文档
    - query :（可选）删除的文档的条件，如果没有条件则为删除所有文档
    - options
        - justOne : （可选）如果设为 true 或 1，则只删除一个文档。
        - writeConcern :（可选）抛出异常的级别。
    - 示例
        - 删除 name = 'Tom' 的文档：`db.users.remove({name:'Tom'})`
        - 删除所有文档：`db.col.remove({})`