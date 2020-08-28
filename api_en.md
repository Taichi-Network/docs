# Taichi Netork Transaction API
---

## API Endpoint
Actual enpoint will be provided by us.
Example:

`http://api.taichi.network:10000/rpc/af9cfc6d90f2489d91c357d449da5b79`

## JSON-RPC Methods

### eth_sendRawTransaction

* Request

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
* Response
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": "0x29e3be282526f5a6329dc66c539b4d49f5d1d4dd740ed69edcb514150284bb53"
}
```

### eth_sendRawTransactions
commit a maximum of 20 transactions

* Request

```shell script
curl -X POST \
  http://api.taichi.network:10000/rpc/af9cfc6d90f2489d91c357d449da5b79 \
  -H 'content-type: application/json' \
  -d '{
         "jsonrpc":"2.0",
         "method":"eth_sendRawTransactions",
         "params":[
             "0xf86c79851a8aedf40082520894f16b4261108f81606eaee9fbe1ae5c7ed812be3988b72fd2103b2800008025a0f7a0cee0fa8dbad6d3afa692b639beae1006c0fef539d699feebb9136215bb62a016f52055834db1abe7181f0a09c97e334fc08df1545b4d694e978bb2562b565f",
             "0xf8ac8201b0851a8aedf4008301117094a6595bcfd91af46900fea8e7c9752db536d798f180b844a9059cbb000000000000000000000000651d23d05481326fb93b3f53ba427e0b235009e000000000000000000000000000000000000000000000000006f05b59d3b2000025a0307ff2fec8cadcbf2b820669675cd09158e1e8187e0e373b226b2d008f4c5939a074b8e425a86c1cd6772d9e7fff45e3aa2111de120f8f8a2248d24cbde590a0fd"
         ],
         "id":1
     }'
```
* Response
```shell script
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": [
        "0x8fa5c40313c69b162de52ce5a8a16894cbd857cdcaebbfdc1249f46d9eaa87c5",
        "0xd0f623571c7ce1ee2acbce6eee7c99da3fb038892aa9f016b6d38f12c9a591f0"
    ]
}
```
