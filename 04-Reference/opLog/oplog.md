## 总结
### 
**1** 在3.2,3.4版本的oplog格式为V1

**2** 3.6,4.0,4.4版本的oplog格式为V2

**3** 5.0版本的oplog格式为V3

###差异 

###删除某库

V1 产生一条删库的Oplog日志

V2,V3产生多条删除该库表的Oplog日志，最后生成一条删除该库的Oplog日志

###更新语句

V1,V2更新语句Oplog格式相同

V3更加细化Update的日志信息

###建立索引

V1建立多个索引时 会产生多个建立索引日志

V2,V3建立多个索引时 会产生一个建立索引日志，该日志下会出现建立索引集合


