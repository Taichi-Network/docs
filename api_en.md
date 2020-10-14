# Taichi Netork Transaction API
---

## API Endpoint
Actual enpoint will be provided by us.
Example:

`http://api.taichi.network:10000/rpc/public`

## JSON-RPC Methods

### eth_sendRawTransaction

### Request

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
### Response Example
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x29e3be282526f5a6329dc66c539b4d49f5d1d4dd740ed69edcb514150284bb53"
}
```

### eth_sendPrivateTransaction
Submit a signed transaction to the node, the transaction will not be broadcast to the Ethereum network through p2p.

### Request

```shell script
curl -X POST \
  http://api.taichi.network:10000/rpc/public \
  -H 'content-type: application/json' \
  -d '{
         "jsonrpc":"2.0",
         "method":"eth_sendPrivateTransaction",
         "params":[
             "0xf86c79851a8aedf40082520894f16b4261108f81606eaee9fbe1ae5c7ed812be3988b72fd2103b2800008025a0f7a0cee0fa8dbad6d3afa692b639beae1006c0fef539d699feebb9136215bb62a016f52055834db1abe7181f0a09c97e334fc08df1545b4d694e978bb2562b565f"
         ],
         "id":1
     }'
```
### Response Example
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x8fa5c40313c69b162de52ce5a8a16894cbd857cdcaebbfdc1249f46d9eaa87c5"
}
```

## Get gas price

### Request
- China Mainland: GET https://gasnow.sparkpool.com/api/v3/gas/price?utm_source=:YourAPPName
- International: GET https://www.gasnow.org/api/v3/gas/price?utm_source=:YourAPPName

### Parameters
- utm_source String. Your app name (e.g. imToken)

### Response Example
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
