
# Taichi Ethereum node peering
## Basics
Set Taichi's enode as your Ethereum node's static node and enjoy fast transaction netwrok. The enode addresses can be found on https://taichi.network/

### Geth
* The list of static nodes resides in `<datadir>/geth/static-nodes.json` . <datadir> can be specified by --datadir commandline argument, default to `$HOME/.ethereum`
* static-nodes.json example：
```json
[
"enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305"
]
```
* For toml config file, the `StaticNodes` option in `[Node.P2P]` secion will set static nodes.
```toml
[Node.P2P]
StaticNodes = ["enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305"]
```
  
### Parity/OpenEthereum
Set commandline `--reserved-peers=/opt/parity/reserved.txt` , or add line `reserved_peers = "/opt/parity/reserved.txt"` in config file secion `[network]`.

Example `reserved.txt`
```
enode://3a682d77eb93b51582fac59182fa569819c6cc9e482e6b4e45307dcb5891fbf5c28fe71c91cd69f5a3317fe070e7a03f0887d3706901a36b2432da8232a4beff@10.5.30.150:30305
```
