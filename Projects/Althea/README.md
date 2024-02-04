<h1 align="center"> 🔥Althea🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Althea)
=

<h1 align="center"> TESTNET</h1>

# StateSync Althea Testnet
```python
SNAP_RPC=https://althea.rpc.t.stavr.tech:443
peers="a1ef55814e2b9aa6c75fbdda52a0ce3d10aebfec@althea.peers.stavr.tech:17886"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.althea/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.althea/config/config.toml
althea tendermint unsafe-reset-all --home /root/.althea
systemctl restart althea && journalctl -u althea -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop althea
cp $HOME/.althea/data/priv_validator_state.json $HOME/.althea/priv_validator_state.json.backup
rm -rf $HOME/.althea/data
curl -o - -L http://althea.snapshot.stavr.tech:1020/althea/althea-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.althea --strip-components 2
mv $HOME/.althea/priv_validator_state.json.backup $HOME/.althea/data/priv_validator_state.json
wget -O $HOME/.althea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/addrbook.json"
sudo systemctl restart althea && journalctl -u althea -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Althea-testnetL1/staking        `Indexer "ON"` \
🔥API🔥:      https://althea.api.t4.stavr.tech \
🔥RPC🔥:      https://althea.rpc.t.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC🔥:     http://althea.grpc.t.stavr.tech:7219 \
🔥peer🔥:     `a1ef55814e2b9aa6c75fbdda52a0ce3d10aebfec@althea.peers.stavr.tech:17886` \
🔥Addrbook🔥: ```wget -O $HOME/.althea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O althe https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/althe && chmod +x althe && ./althe` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Althea/Decentralization)🔥

<details>
<summary>RPC Scanning</summary>

<h2 align="center"> We scan nodes in real time every 4 hours. And we provide the final result of RPC endpoints.
We cannot influence the operation of these nodes in any way. </h2>


```python
If Voting Power is higher than 0 --> then the Node is a validator of the network and may be subject to attack and be a potential threat to the chain.
```
```python
We marked such validators with a red symbol
```

</details>

[raw json](https://rpc-check.althea.stavr.tech/althea/rpcalthea_result.json)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.9.106.214:26679</td><td>althea_417834-3</td><td>node 🔴</td><td>3163740</td><td>1</td><td>False</td><td>on</td><td>1475</td><td>2024-02-04T16:39:15.412900224UTC</td></tr><tr><td>176.9.110.12:60557</td><td>althea_417834-3</td><td>Sirius.nodes 🔴</td><td>3163739</td><td>496001</td><td>False</td><td>on</td><td>1631</td><td>2024-02-04T16:39:12.247578427UTC</td></tr><tr><td>49.12.84.248:19657</td><td>althea_417834-3</td><td>[NODERS]TEAM 🟢</td><td>3163741</td><td>542401</td><td>False</td><td>off</td><td>0</td><td>2024-02-04T16:39:18.643557083UTC</td></tr><tr><td>65.109.88.254:31657</td><td>althea_417834-3</td><td>ksalab 🔴</td><td>3163740</td><td>1335001</td><td>False</td><td>off</td><td>1486</td><td>2024-02-04T16:39:16.097128985UTC</td></tr><tr><td>136.243.148.154:15257</td><td>althea_417834-3</td><td>terlia 🔴</td><td>3163739</td><td>1943001</td><td>False</td><td>on</td><td>1011</td><td>2024-02-04T16:39:11.887989374UTC</td></tr><tr><td>168.119.139.86:63657</td><td>althea_417834-3</td><td>node 🔴</td><td>3163740</td><td>1957001</td><td>False</td><td>on</td><td>1009</td><td>2024-02-04T16:39:12.495098494UTC</td></tr><tr><td>5.75.153.46:17887</td><td>althea_417834-3</td><td>STAVR 🔴</td><td>3163742</td><td>2580801</td><td>False</td><td>on</td><td>2069</td><td>2024-02-04T16:39:25.546456338UTC</td></tr><tr><td>35.201.194.177:26657</td><td>althea_417834-3</td><td>althea-testnet-0 🔴</td><td>3163742</td><td>2876301</td><td>False</td><td>on</td><td>1057</td><td>2024-02-04T16:39:26.675998645UTC</td></tr><tr><td>65.108.135.212:14657</td><td>althea_417834-3</td><td>2xStake.com 🔴</td><td>3163740</td><td>2890401</td><td>False</td><td>on</td><td>2081</td><td>2024-02-04T16:39:15.115728292UTC</td></tr><tr><td>142.132.202.50:47657</td><td>althea_417834-3</td><td>cryptobtcbuyer 🟢</td><td>3163741</td><td>3063741</td><td>False</td><td>off</td><td>0</td><td>2024-02-04T16:39:18.932470514UTC</td></tr></table>
