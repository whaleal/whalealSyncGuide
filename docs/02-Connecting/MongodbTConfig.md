
# MongodbTConfig

~~~
    MongodbTConfig包含以下配置,其配置内容为config目录下mongodbT.properties 配置文件
    - 任务与进程名
    - URL配置
    - 全量任务
    - 实时任务
    - 全量加增量
    - 全量加实时
~~~

<br>

## 任务与进程名

- 任务名。

      不写则默认生成
      taskName = mongoTask

- 程序名名。

      不写则默认生成
      proName = mongoPro

<br>

## URL配置

- source端mongodb的url。(必配)

      带认证：
          sourceDsUrl = mongodb://root:123456@192.168.3.190:27001/admin
      无认证：
         sourceDsUrl = mongodb://192.168.3.190:27001

- target端mongodb的url。(必配)

      带认证：
          sourceDsUrl = mongodb://root:123456@192.168.3.190:27001/admin
      无认证：
         sourceDsUrl = mongodb://192.168.3.190:27001

<br>

## 全量任务
### 同步模式


- 全量:all  全量同步表,不同步同步期间对源表进行的操作
    
      syncMode = all

- 全量同步时,是否按照依次同步表或多表并行同步。默认为false即多表并行同步

      parallelSynchronizationMultipleTables = false

- 需要同步的表,使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+
   
      dbTableWhite = .+

- 全量同步情况下:是否删除目标库已经存在的源表。默认false即不删除
   
      autoDropExistDbTable = false

- 全量同步情况下:是否同步源表的索引信息。默认true即同步。在true时,当源表数据同步60%时开始同步源表的索引

      autoCreateIndex = true

- 全量同步情况下读取源表的线程数。最小为2，最大为50。默认值为2
    
      sourceThreadNum = 4

- 全量同步情况下执行写入目标库的线程数。最小为4，最大为50 。默认值为6
- 建议targetThreadNum是sourceThreadNum的3倍

      targetThreadNum = 12


- 下面三个参数cacheBucketSize,cacheBucketNum,dataBatchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
- 均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
- 每个缓存桶缓存批次数量。默认为20

      cacheBucketSize = 10


- 缓存区个数。默认为20

      cacheBucketNum = 60


- 每批次数据的大小。默认为128

      dataBatchSize = 128

<br>

## 实时任务
### 同步模式


- 实时:realTime 实时同步

      syncMode = realTime

- 全量同步时,是否按照依次同步表或多表并行同步。默认为false即多表并行同步

      parallelSynchronizationMultipleTables=false

- 需要同步的表,使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+

      dbTableWhite=.+

- 需要同步的DDL
- 实时同步情况下可以同步drop,create,createIndexes,dropIndexes,renameCollection,convertToCapped,dropDatabase。默认值为*,即同步所有DDL操作
- 多个DDL中间使用英文逗号隔离。若多个DDL中包含*,则同步所有DDL操作

      ddlFilterSet = *

- 在实时同步时,设置读取oplog的开始时间。默认值为程序启动时刻的10位时间戳，否则则书写10位时间戳

      startOplogTime =


- 在实时同步时,设置读取oplog的结束时间。默认值为0即没有结束时间，否则则书写10位时间戳

      endOplogTime =


- 在实时同步时,设置读取oplog的延迟时间。默认值为0即没有延迟时间

      delayTime =


- 在实时同步中每个数据源解析数据的线程。最小为4，最大为50。默认值为8

      realTimeThreadNum = 12


<br>

## 全量加增量
### 同步模式

- 全量和增量:allAndIncrement 全量同步后,仅同步同步期间对源表进行的操作。增量同步的开始时间为全量同步的开始时间,增量同步的结束时间为全量同步的结束时间

      syncMode = allAndIncrement

- 全量同步时,是否按照依次同步表或多表并行同步。默认为false即多表并行同步

      parallelSynchronizationMultipleTables = false

- 需要同步的表,使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+

      dbTableWhite = .+

- 需要同步的DDL
- 实时同步情况下可以同步drop,create,createIndexes,dropIndexes,renameCollection,convertToCapped,dropDatabase。默认值为*,即同步所有DDL操作
- 多个DDL中间使用英文逗号隔离。若多个DDL中包含*,则同步所有DDL操作

      ddlFilterSet = *

- 全量同步情况下:是否删除目标库已经存在的源表。默认false即不删除

      autoDropExistDbTable = false

- 全量同步情况下:是否同步源表的索引信息。默认true即同步。在true时,当源表数据同步60%时开始同步源表的索引

      autoCreateIndex = true

- 全量同步情况下读取源表的线程数。最小为2，最大为50。默认值为2

      sourceThreadNum = 4

- 全量同步情况下执行写入目标库的线程数。最小为4，最大为50 。默认值为6
- 建议targetThreadNum是sourceThreadNum的3倍

      targetThreadNum = 12

- 下面三个参数cacheBucketSize,cacheBucketNum,dataBatchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
- 均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
- 每个缓存桶缓存批次数量。默认为20

      cacheBucketSize = 10

- 缓存区个数。默认为20

      cacheBucketNum = 60

- 每批次数据的大小。默认为128

      dataBatchSize = 128

- 在实时同步时,设置读取oplog的开始时间。在全量加增量情况下,该参数由程序确定

      startOplogTime =

- 在实时同步时,设置读取oplog的结束时间。在全量加增量情况下,该参数由程序确定

      endOplogTime =

- 在实时同步时,设置读取oplog的延迟时间。在全量加增量情况下,该参数由程序确定

      delayTime =

- 在实时同步中每个数据源解析数据的线程。最小为4，最大为50。默认值为8

      realTimeThreadNum = 12


<br>

## 全量加增量
### 同步模式


- 全量和实时:allAndRealTime  全量同步后,开始进行实时同步,实时同步的开始时间为全量同步的开始时间

      syncMode=allAndRealTime

- 全量同步时,是否按照依次同步表或多表并行同步。默认为false即多表并行同步

      parallelSynchronizationMultipleTables=false

- 需要同步的表,使用正则表达式书写。例如同步mongodb库下的所有表：mongodb\\..+   默认同步全部表：.+

      dbTableWhite=.+

- 需要同步的DDL
- 实时同步情况下可以同步drop,create,createIndexes,dropIndexes,renameCollection,convertToCapped,dropDatabase。默认值为*,即同步所有DDL操作
- 多个DDL中间使用英文逗号隔离。若多个DDL中包含*,则同步所有DDL操作

      ddlFilterSet=*

- 全量同步情况下:是否删除目标库已经存在的源表。默认false即不删除

      autoDropExistDbTable=false

- 全量同步情况下:是否同步源表的索引信息。默认true即同步。在true时,当源表数据同步60%时开始同步源表的索引

      autoCreateIndex=true

- 全量同步情况下读取源表的线程数。最小为2，最大为50。默认值为2

      sourceThreadNum=4

- 全量同步情况下执行写入目标库的线程数。最小为4，最大为50 。默认值为6
- 建议targetThreadNum是sourceThreadNum的3倍

      targetThreadNum=12

- 下面三个参数cacheBucketSize,cacheBucketNum,dataBatchSize共同决定全量情况下,内存中缓存的数据条数,注意内存溢出的情况。
- 均采用默认值则内存缓存20*20*128条数据,若每条数据100kb,则最大占用内存4.88G
- 每个缓存桶缓存批次数量。默认为20

      cacheBucketSize=10

- 缓存区个数。默认为20

      cacheBucketNum=60

- 每批次数据的大小。默认为128

      dataBatchSize=128

- 在实时同步时,设置读取oplog的开始时间。全量加实时模式下:该参数由程序确定

      startOplogTime=

- 在实时同步时,设置读取oplog的结束时间。默认值为0即没有结束时间，否则则书写10位时间戳

      endOplogTime=

- 在实时同步时,设置读取oplog的延迟时间。默认值为0即没有延迟时间

      delayTime=

- 在实时同步中每个数据源解析数据的线程。最小为4，最大为50。默认值为8

      realTimeThreadNum=12




