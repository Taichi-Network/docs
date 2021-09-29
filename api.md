## 1. 获取 ETH gas price
查询当前 ETH GasPrice 预测数据。接口数据每 8s 更新一次，请控制访问频率(间隔 >= 8s)，频率太高会被拉黑名单；已部署负载均衡。

### 请求

- GET https://www.gasnow.org/api/v3/gas/price?utm_source=:YourAPPName

### 参数
- utm_source String. Your app name (e.g. Xcompany)

### 响应
```json
{
  "code": 200,
  "data": {
    "rapid": 180132000000,
    "fast": 177000000000,
    "slow": 150000000000,
    "standard": 109000001459,
    "timestamp": 1598434638872
  }
}
```

## 2. RPC Node
选择延时最低的 rpc 节点，广播交易更高效

**亚太地区: https://api.taichi.network:10001**

**欧洲: https://api-eu.taichi.network:10001**

**北美: https://api-us.taichi.network:10001**

## 3. 发送隐私交易 eth_sendPrivateTransaction
向节点提交一个已签名的交易，交易被打包前不会通过p2p广播到以太坊网络中。

### 注意事项
1. 我们会尽最大努力保障隐私交易的私密性，鉴于以太坊网络的特点，您发送的交易仍有可能在正式确认前暴露到公开网络中。此类情况包括但不限于:
    * 打包这笔交易的块成为叔块。
    * 区块链发生重组。打包这笔交易的块成为孤块。
    * Ethereum规范或实现中的存在缺陷。
2. 隐私交易仍需要参与gas price竞价，过低的gas price会导致交易长时间无法打包甚至丢失。
3. 我们目前仅提供一部分算力用于打包隐私交易，因此不是每一个区块都能包含隐私交易。
4. 访问频率50次/秒。

### Parameters
DATA，已签名的交易数据
```json
params: ["0xf86c0785080ad9f00082627094302fc4c7231589239912d62ec7ea6266d771cfdf88024a8d93446ac0008025a01450674b2c65e7902d9f03cbf899bb1063b2b14ca5e6a7fa5616d420b67196c1a049063bc399b171b0c570aeba9d33bc78a550701c3e95238947b90f1ccf841032"]
```
### Return
DATA，32字节 - 交易哈希值

### Example
Request：
```shell script
curl -X POST \
  https://api.taichi.network:10001/rpc/private \
  -H 'content-type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "method":"eth_sendRawTransaction",
    "params":[
       "0xf86c0785080ad9f00082627094302fc4c7231589239912d62ec7ea6266d771cfdf88024a8d93446ac0008025a01450674b2c65e7902d9f03cbf899bb1063b2b14ca5e6a7fa5616d420b67196c1a049063bc399b171b0c570aeba9d33bc78a550701c3e95238947b90f1ccf841032"
    ],
    "id":1
}'
```
Response：
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x2531af4feb0a4ddf256a4b0ffa54563c9a857b7cf6e0987a26e446e1dc015578"
}
```

## 4. 隐私交易查询
查询隐私交易信息。

### 请求
GET https://api.taichi.network:10001/txscan/priTx?txHash=:txHash

### 参数
- txHash String.

### 交易状态说明
- received, 太极已经收到交易。
- pending, 交易等待确认中。
- success, 交易确认成功。
- fail, 交易失败(交易数据可能有错)。
- timeout, 交易超过3小时还未确认。

### 响应
```
{
    "success": true, // false表示交易不存在
    "obj": {
        "txHash": "0x7d03d5990b2250ceb3972f1ce7c663871b0e96136d7f3064456b5da48cf4457f",
        "nonce": 63,
        "from": "0x40F9c13364ddf2f70e01545BF2e19702FCf1D33D",
        "blockNumber": 0,
        "gasUsed": 0,
        "gasLimit": 21000,
        "gasPrice": 30000000000,
        "to": "0x40F9c13364ddf2f70e01545BF2e19702FCf1D33D",
        "value": 0,
        "status": "pending" // all status: received, pending, success, fail, timeout
    }
}
```

## 3. 广播交易 eth_sendRawTransaction
向节点提交一个已签名的交易以便广播到以太坊网络中

### Parameters
DATA，已签名的交易数据
```json
params: ["0xf86d82258a8507ea8ed40082520894efbb775769a6b29be8b504a7928deed1498e181087069ba8ff484000801ca039a3db3e613ec392f519bad0ca981d29b390ca246b231fae07ba0982ea05e805a01270fa3ccc2b92185f06f2c307255738f52e91ea26fac19e95bd254fb211cbdb"]
```
### Return
DATA，32字节 - 交易哈希值

### Example
Request：
```shell script
curl -X POST \
  https://api.taichi.network:10001/rpc/public \
  -H 'content-type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "method":"eth_sendRawTransaction",
    "params":[
       "0xf86d82258a8507ea8ed40082520894efbb775769a6b29be8b504a7928deed1498e181087069ba8ff484000801ca039a3db3e613ec392f519bad0ca981d29b390ca246b231fae07ba0982ea05e805a01270fa3ccc2b92185f06f2c307255738f52e91ea26fac19e95bd254fb211cbdb"
    ],
    "id":1
}'
```
Response：
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x6fb9f9012732a51aa3e4fb9e7fa4de62f942b249416d29505bc0b2fac48202b1"
}
```

## 6. 广播交易 eth_sendUncheckedTransaction
和`eth_sendRawTransaction`一样, 但是不检查nonce和gasprice有效性，用这个接口广播交易可以获得更快的响应。需要自己保证交易的有效性。

## 7. MEV 交易包 eth_sendBundle
可以将多比交易打成一个交易包发送。如果在交易包中给矿池支付足够的费用，矿池将整体打包这几笔交易，并排在最前面。

可参考[Flashbots的文档](https://docs.flashbots.net/flashbots-auction/searchers/advanced/rpc-endpoint).

### 请求
```
{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "eth_sendBundle",
  "params": [
    {
      txs,               // Array[String], 一组签名后的交易
      blockNumber,       // String, 16进制，预期需要上链的高度
      minTimestamp,      // (可选) 最早上链时间(unix 时间戳)
      maxTimestamp,      // (可选) 最晚上链时间(unix 时间戳)
      revertingTxHashes, // (可选) Array[String], 允许revert的交易hash
    }
  ]
}
```

### 响应
```json
{"jsonrpc": "2.0", "id": 1, "result": null}
```
### 范例
```shell
curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc":"2.0","method":"eth_sendBundle","params":[{see above}],"id":1}' https://api.taichi.network:10001/rpc/public
```
