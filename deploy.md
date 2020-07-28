
# 太极网络（Taichi）推送交易的接入教程
## 接入推送
矿池节点想接入太极网络，得到交易的推送非常简单，只需要告知我们矿池节点的 enode，并且矿池节点把太极的 enode 添加为静态/保留节点即可。

### Geth
* 静态节点列表的位置在 `<datadir>/geth/static-nodes.json` . <datadir>由命令行参数--datadir指定, 默认为`$HOME/.ethereum`
* static-nodes.json 内容范例：
```json
[
"enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305"
]
```
  
### Parity/OpenEthereum
命令行`--reserved-peers=/opt/parity/reserved.txt` , 或配置文件`[network]`项下添加`reserved_peers = "/opt/parity/reserved.txt"`
`reserved.txt` 范例
```
enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305
```


## 推送效果获取
目前主要有2种不同的方式能获取到推送效果。它们的差异取决于矿池端需要做的修改有多少。
1. 矿池端不需要做其它任何额外的变动。
这种方式可以知道的是太极网络成功推送的交易数量。
2. 矿池端运行的 Geth 节点在代码上应用我们开源的补丁，并且在节点旁部署一个数据获取和上报的开源程序。
这种方式获取的数据最精确，能得到太极推送交易的精确数量。首先这个补丁会在原有的 Json-RPC 里面新增一个接口，用来获取太极节点推送过来的交易数量。在节点旁边运行的程序会从这个接口中获取交易推送数量，并传回给太极的后端服务。
