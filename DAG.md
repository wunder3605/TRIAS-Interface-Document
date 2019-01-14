# DAG 接口文档

## 1. HTTP 接口

### 1.1 将数据Cache在DAG中

```
endpoint: save_data
method: POST
payload: json形式的数据，数据是IPFS地址或者是数据本身由上层应用决定。
例子：
curl http://host:port/save_data -X POST -H "Content-Type: application/json" \
    -d "{"data" : <data_info>, "tag" : <tag_info>}"
```

|字段|说明|
|-----|------|
|data|数据是IPFS地址或者是数据本身由上层应用决定|
|tag|标签，用于表明时间，服务类型等等|

### 1.2 获取数据的信息

```
endpoint: get_data
method: GET 
payload: json形式的数据，如果提供数据内容则精确匹配，如果仅提供tag/extended_tag则模糊匹配。
例子：
curl http://host:port/get_data -X GET -H "Content-Type: application/json" \
    -d "{"data" : <data_info>, "tag" : 20150109TXN, "extended_tag" : "confirmed_unsynced"}"
找到2019年01/09号所有被确认但是没被同步的交易信息。
```
|字段|说明|
|-----|------|
|data|数据是IPFS地址或者是数据本身由上层应用决定|
|tag|标签，用于表明时间，服务类型等等|
|extended\_tag|主要是对已有的信息做标注，比如说某个信息已经“删除”等等|


### 1.3 将数据状态进行更新

```
endpoint: update_data
method: PUT
payload: json形式的数据，仅支持修改扩展标签
例子：
curl http://host:port/update_data -X PUT -H "Content-Type: application/json" \
    -d "{"data":"<data_info>", "extended_tag" : <extended_tag_info>}"
```
|字段|说明|
|-----|------|
|data|数据是IPFS地址或者是数据本身由上层应用决定|
|extended\_tag|主要是对已有的信息做标注，比如说某个信息已经“删除”等等|


## 2. python SDK
目前对外暴露的SDK仅支持python版本的，接口如下：
```
TriasDAG(uri=None, seed=None)
save_data(data=None, tag=None)
get_data(data=None, tag=None, extended_tag=None)
update_data(data=None, extended_tag=None)
```

## 3. 依赖的服务
目前不依赖任何服务。

## 4. 提供服务
|服务|说明|
|-----|------|
|APP|APP 会向DAG中缓存数据|
|同步(SYNC)|SYNC服务会从DAG中PULL数据并推送给TM|
|TM|TM 从DAG中拉取数据|
|UTXO|TM 从DAG中拉取交易数据|
