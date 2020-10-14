
# 太极网络（Taichi）rpc接口说明
---

## 共同说明

### 协议
JSON-RPC

Content-Type: application/json

## eth_sendRawTransaction
向节点提交一个已签名的交易以便广播到以太坊网络中

### Parameters
1.DATA，已签名的交易数据
```json
params: ["0xf8aa2a85021ea4a10f830155e2940eee3e3828a45f7601d5f54bf49bb01d1a9df5ea80b8444706c375000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000053cfe425a0cf3735fe97ea23c4f7ee2dd62a1aa50ba595b99b347bf7ccd92f3123326a0bffa03bd4da469a1eba694c41d1c24ee56e275ace8c27cba0dc30760c1cdbe2d41ac2"]
```
### Return
DATA，32字节 - 交易哈希值

### Example
Request：
```shell script
curl -X POST \
  http://api.taichi.network:10000/rpc/public \
  -H 'content-type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "method":"eth_sendRawTransaction",
    "params":[
       "0xf8aa2a85021ea4a10f830155e2940eee3e3828a45f7601d5f54bf49bb01d1a9df5ea80b8444706c375000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000053cfe425a0cf3735fe97ea23c4f7ee2dd62a1aa50ba595b99b347bf7ccd92f3123326a0bffa03bd4da469a1eba694c41d1c24ee56e275ace8c27cba0dc30760c1cdbe2d41ac2"
    ],
    "id":1
}'
```
Response：
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x29e3be282526f5a6329dc66c539b4d49f5d1d4dd740ed69edcb514150284bb53"
}
```

## eth_sendPrivateTransaction
向节点提交一个已签名的交易，交易确认前不会通过p2p广播到以太坊网络中。

### Parameters
1.DATA，已签名的交易数据
```json
params: ["0xf8aa2a85021ea4a10f830155e2940eee3e3828a45f7601d5f54bf49bb01d1a9df5ea80b8444706c375000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000053cfe425a0cf3735fe97ea23c4f7ee2dd62a1aa50ba595b99b347bf7ccd92f3123326a0bffa03bd4da469a1eba694c41d1c24ee56e275ace8c27cba0dc30760c1cdbe2d41ac2"]
```
### Return
DATA，32字节 - 交易哈希值

### Example
Request：
```shell script
curl -X POST \
  http://api.taichi.network:10000/rpc/public \
  -H 'content-type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "method":"eth_sendPrivateTransaction",
    "params":[
       "0xf8aa2a85021ea4a10f830155e2940eee3e3828a45f7601d5f54bf49bb01d1a9df5ea80b8444706c375000000000000000000000000a0b86991c6218b36c1d19d4a2e9eb0ce3606eb48000000000000000000000000000000000000000000000000000000000053cfe425a0cf3735fe97ea23c4f7ee2dd62a1aa50ba595b99b347bf7ccd92f3123326a0bffa03bd4da469a1eba694c41d1c24ee56e275ace8c27cba0dc30760c1cdbe2d41ac2"
    ],
    "id":1
}'
```
Response：
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x29e3be282526f5a6329dc66c539b4d49f5d1d4dd740ed69edcb514150284bb53"
}
```

## 获取gas price

### 请求
- 中国大陆: GET https://gasnow.sparkpool.com/api/v3/gas/price?utm_source=:YourAPPName
- 国际: GET https://www.gasnow.org/api/v3/gas/price?utm_source=:YourAPPName

### 参数
- utm_source String. Your app name (e.g. imToken)

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


