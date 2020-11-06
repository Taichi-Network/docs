## Get gas price
Interface data updates per 8s, please don't access frequently, or you will be blocked. A high-availability cluster has been deployed.

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

## RPC Node
Choose the rpc node with the lowest delay, broadcast transactions more efficiently.

**Asia-Pacific: https://api.taichi.network:10001**

**Europe: https://api-eu.taichi.network:10001**

**North: America https://api-us.taichi.network:10001**

## Broadcast TX | eth_sendRawTransaction
Submit a signed transaction to the node for broadcasting to the Ethereum network.

### Parameters
DATA, signed transaction data.
```json
params: ["0xf86d82258a8507ea8ed40082520894efbb775769a6b29be8b504a7928deed1498e181087069ba8ff484000801ca039a3db3e613ec392f519bad0ca981d29b390ca246b231fae07ba0982ea05e805a01270fa3ccc2b92185f06f2c307255738f52e91ea26fac19e95bd254fb211cbdb"]
```
### Return
DATA, 32 Bytes - Transaction hash.

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

## Private TX | eth_sendPrivateTransaction
Submit a signed transaction to the node, and it will not be broadcasted to the Ethereum network before the transaction is sealed in a block.

### Caveats
1. We provide private transaction with our best effort. However, there are still ocassions that your private transaction can be exposed to public before 
confirmation. Such cases include but are not limited to
    * The block containing private tx becomes uncle block
    * The block chain reorgnizes and block containing private tx becomes orphaned block
2. Private transactions still conform to gas price requirement. If the gas price is too low, it will wait for a long time or even lost.
3. We currently only provide a portion of SparkPool's hash power for private transaction, so not all blocks mined by SparkPool will contain private transaction.
4. Frequency limit 50/sec.

### Parameters
DATA, signed transaction data.
```json
params: ["0xf86c0785080ad9f00082627094302fc4c7231589239912d62ec7ea6266d771cfdf88024a8d93446ac0008025a01450674b2c65e7902d9f03cbf899bb1063b2b14ca5e6a7fa5616d420b67196c1a049063bc399b171b0c570aeba9d33bc78a550701c3e95238947b90f1ccf841032"]
```
### Return
DATA, 32 Bytes - Transaction hash.

### Example
Request：
```shell script
curl -X POST \
  https://api.taichi.network:10001/rpc/public \
  -H 'content-type: application/json' \
  -d '{
    "jsonrpc":"2.0",
    "method":"eth_sendPrivateTransaction",
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

## Get private transaction
Get private transaction by hash.

### Request
Get https://api.taichi.network:10001/txscan/priTx?txHash=:txHash

### Parameters
- txHash String.

### Response
```json
{
    "success": true, // false means that the transaction does not exist
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
        "status": "pending" // all status: received, pending, success
    }
}
```
