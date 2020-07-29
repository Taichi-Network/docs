
# 太极网络（Taichi）rpc接口说明
---

## 共同说明

### 接口地址
POST http://api.taichi.network:10000/rpc/af9cfc6d90f2489d91c357d449da5b79

### 协议
JSON-RPC

Content-Type: application/json

## eth_sendRawTransaction
向节点提交一个已签名的交易以便广播到以太坊网络中。

### 请求参数
请求示例：
```shell script
curl -X POST \
  http://api.taichi.network:10000/rpc/af9cfc6d90f2489d91c357d449da5b79 \
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
### 请求响应
返回交易哈希。
响应结果示例：
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x29e3be282526f5a6329dc66c539b4d49f5d1d4dd740ed69edcb514150284bb53"
}
```