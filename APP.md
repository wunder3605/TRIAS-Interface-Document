# APP Server
## HTTP接口说明
### 1.上传交易
地址：http://address/upload_transaction

请求方式：POST；application/json

请求数据：  
```
curl -X POST \
  http://address/upload_transaction \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -d '{"type": "trans", "from_address": "addr1", "to_address": "addr2", "amount": "1000"}'
```

说明：

| 字段 | 说明 |
|-----|------|
| type | 类型，默认为trans |
| from_address | 交易的来源地址 |
| to_address | 交易的目标地址 |
| amount | 交易数额 |

### 2.上传合约
地址：http://address/upload_contract

请求方式：POST；multipart/form-data

请求数据：  
```
curl -X POST \
  http://address/upload_contract \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data' \
  -F contract=@/home/ubuntu/contract/chaincode_example02.go \
  -F md5=7a3f59dd79140c6ce5de2d6a6ef5e352
```

说明：

| 字段 | 说明 |
|-----|------|
| contract | 合约的本地地址 |
| md5 | 合约的md5值 |

### 3.上传Action
地址：http://address/upload_action

请求方式：POST；multipart/form-data

请求数据：  
```
curl -X POST \
  http://127.0.0.1:5000/upload_action \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data' \
  -F md5=7a3f59dd79140c6ce5de2d6a6ef5e352 \
  -F contractName=contract_1546059807 \
  -F 'command={"Args":["init","a","7","b","8"]}' \
  -F operation=instantiate \
  -F address=QmStXVUdqAbKDTecFQkawuvSNqPs6su5KJB94Uvd9MiCny
```
说明：

| 字段 | 说明 |
|-----|------|
| md5 | 合约的md5值 |
| contractName | 合约的名称，从上传合约命令返回中拿到 |
| command | 执行的命令 |
| operation | 操作类型 |
| address | 合约所在IPFS的地址，从上传合约命令返回中拿到 |


### 4.调用查询
地址：http://address/query_action

请求方式：POST；multipart/form-data

请求数据：  
```
curl -X POST \
  http://127.0.0.1:5000/query_action \
  -H 'cache-control: no-cache' \
  -H 'content-type: multipart/form-data' \
  -F md5=7a3f59dd79140c6ce5de2d6a6ef5e352 \
  -F contractName=contract_1545984529 \
  -F 'command={"Args":["query","a"]}' \
  -F address=QmStXVUdqAbKDTecFQkawuvSNqPs6su5KJB94Uvd9MiCny
```
说明：

| 字段 | 说明 |
|-----|------|
| md5 | 合约的md5值 |
| contractName | 合约的名称，从上传合约命令返回中拿到 |
| command | 执行的命令 |
| address | 合约所在IPFS的地址，从上传合约命令返回中拿到 |
