
# MongodbT


## QuickStart

## 启动步骤

#### 1.下载MongoT

访问 https://github.com/whaleal/mongodbT/releases

下载最近版本的mongodbT.tar.gz

#### 2.解压缩

```
mkdir mongodbT
tar -zxvf mngodbT.tar.gz  -C mongodbT
```

#### 3.配置文件修改

```
cd mongodbT/config
vi mongodbT.properties
```

```
// 按照提示 输入配置信息
```

#### 4.准备启动

```
cd bin
./start.sh
```

#### 5.查看日志

```
cd logs/
tail -f logs.log
tail -f error.log
```

#### 6.查看目标端的数据量，对比数据一致性。

1 使用mongodb自带校验工具。（会锁库）

```
 use xxx
 db.runCommand({dbHash:1})
 ```

2 手动校验数据











