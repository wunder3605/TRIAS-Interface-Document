# Tendermint
### Tendermint我们简称TM，是Cosmos的共识框架，TM本身来负责共识的基部部分：消息的广播、共识、记账出块等。TM对外暴露消息接收的接口，接收到之后会进行消息广播，
在消息广播时，会检查消息有效性，共识过程中，会把检查完成的消息广播到其他节点，从而调用其他节点的deliver接口，这个回调接口，会把收到的消息推到每节点，节点收到后，本地记账。
## HTTP接口说明
### 1.消息广播
地址：http://address/broadcast_tx_commit?tx="the tx json string "

请求方式：POST；multipart/form-data

说明：

| 字段 | 说明 |
|-----|------|
| tx | 交易字符串 |


##  回调接口需求
### 1.checkTx
地址：http://address/check_tx

请求方式：POST；multipart/form-data

请求数据：  
```
curl -X POST \
  http://address/check_tx \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data' \
  -F tx="the tx json string"
```

说明：

| 字段 | 说明 |
|-----|------|
| tx | 交易json字符串 |


### 2.deliverTx
地址：http://address/deliver_tx

请求方式：POST；multipart/form-data

请求数据：
```
curl -X POST \
  http://address/deliver_tx \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data' \
  -F tx="the tx json string"
```

说明：

| 字段 | 说明 |
|-----|------|
| tx | 交易json字符串 |

### 3.commit
地址：http://address/queryState TODO 这个接口目前考虑到架构实现上，暂时可以先不用

请求方式：GET；

请求数据：
```
curl -X GET \
  http://address/query_state \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data'
```

