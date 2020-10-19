
# 太极网络（Taichi）enode互联接入教程
## 互联方法
将太极的 enode 添加为ETH节点的静态/保留节点即可建立连接。节点enode地址可以在 https://taichi.network/ 上获取。

### Geth
* 静态节点列表的位置在 `<datadir>/geth/static-nodes.json` . <datadir>由命令行参数--datadir指定, 默认为`$HOME/.ethereum`
* static-nodes.json 内容范例：
```json
[
"enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305"
]
```
* 如果使用toml配置文件, 须在`[Node.P2P]`项的`StaticNodes`里添加, 如
```toml
[Node.P2P]
StaticNodes = ["enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305"]
```
  
### Parity/OpenEthereum
命令行`--reserved-peers=/opt/parity/reserved.txt` , 或配置文件`[network]`项下添加`reserved_peers = "/opt/parity/reserved.txt"`
`reserved.txt` 范例
```
enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305
```
