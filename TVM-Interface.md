#### TVM：
##### 接口说明：
地址：http://address/executeContract

请求方式：POST；application/json

请求数据：

    {
        "address": "QmStXVUdqAbKDTecFQkawuvSNqPs6su5KJB94Uvd9MiCny",
        "checkMD5": "7a3f59dd79140c6ce5de2d6a6ef5e352",
        "command": "{\"Args\":[\"query\",\"b\"]}",
        "contractName": "firstContract",
        "contractType": "fabric",
        "contractVersion": "v1.0",
        "vmVersion": "1.0",
        "sequence": "10",
        "timestamp": 1545117978737,
        "user": "user1",
        "signature": "",
        "operation": "query"
    }
说明

|字段|说明|
|-----|------|
|address|合约的ipfs地址|
|checkMD5|合约的md5校验码|
|command|合约执行的命令|
|contractName|合约名|
|contractType|合约类型,目前只有fabric|
|contractVersion|合约版本|
|vmVersion|虚拟机版本|
|sequence|执行序号（预留字段，是否可用作以后共识状态使用）|
|timestamp|时间戳|
|user|用户|
|signature|用户签名|
|operation|操作类型,install:安装;instantiate:初始化;query:查询;……|
