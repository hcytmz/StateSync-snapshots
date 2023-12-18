<h1 align="center"> 🔥Althea🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Althea)
=

<h1 align="center"> TESTNET</h1>

# StateSync Althea Testnet
```python
SNAP_RPC=http://althea.rpc.t.stavr.tech:17887
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
🔥RPC🔥:      http://althea.rpc.t.stavr.tech:17887              `Snapshot-interval = 100` \
🔥gRPC🔥:     http://althea.grpc.t.stavr.tech:7219 \
🔥peer🔥:     `a1ef55814e2b9aa6c75fbdda52a0ce3d10aebfec@althea.peers.stavr.tech:17886` \
🔥Addrbook🔥: ```wget -O $HOME/.althea/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O althe https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Althea/althe && chmod +x althe && ./althe`


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

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.9.106.214:26679</td><td>althea_417834-3</td><td>node 🔴</td><td>2437607</td><td>1</td><td>False</td><td>on</td><td>975</td><td>2023-12-18T13:41:45.752825288UTC</td></tr><tr><td>66.172.36.142:14657</td><td>althea_417834-3</td><td>node 🟢</td><td>2437609</td><td>165</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T13:41:53.903287820UTC</td></tr><tr><td>176.9.110.12:60557</td><td>althea_417834-3</td><td>Sirius.nodes 🔴</td><td>2437607</td><td>496001</td><td>False</td><td>on</td><td>1625</td><td>2023-12-18T13:41:42.780064921UTC</td></tr><tr><td>49.12.84.248:19657</td><td>althea_417834-3</td><td>[NODERS]TEAM 🔴</td><td>2437608</td><td>542401</td><td>False</td><td>off</td><td>1</td><td>2023-12-18T13:41:48.742854747UTC</td></tr><tr><td>65.109.88.254:31657</td><td>althea_417834-3</td><td>ksalab 🔴</td><td>2437607</td><td>1335001</td><td>False</td><td>off</td><td>1396</td><td>2023-12-18T13:41:46.453177191UTC</td></tr><tr><td>136.243.148.154:15257</td><td>althea_417834-3</td><td>terlia 🔴</td><td>2437606</td><td>1943001</td><td>False</td><td>on</td><td>1011</td><td>2023-12-18T13:41:40.260122211UTC</td></tr><tr><td>168.119.139.86:63657</td><td>althea_417834-3</td><td>node 🔴</td><td>2437607</td><td>1957001</td><td>False</td><td>on</td><td>1009</td><td>2023-12-18T13:41:43.064438956UTC</td></tr><tr><td>65.108.135.212:14657</td><td>althea_417834-3</td><td>2xStake.com 🔴</td><td>2437607</td><td>1973401</td><td>False</td><td>on</td><td>1866</td><td>2023-12-18T13:41:45.471261914UTC</td></tr><tr><td>35.201.194.177:26657</td><td>althea_417834-3</td><td>althea-testnet-0 🟢</td><td>2437609</td><td>2252701</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T13:41:57.289772519UTC</td></tr><tr><td>5.75.153.46:17887</td><td>althea_417834-3</td><td>STAVR 🔴</td><td>2437609</td><td>2326501</td><td>False</td><td>on</td><td>1816</td><td>2023-12-18T13:41:56.194969754UTC</td></tr><tr><td>94.130.26.9:26957</td><td>althea_417834-3</td><td>Pro-Nodes75 🔴</td><td>2437607</td><td>2337607</td><td>False</td><td>on</td><td>980</td><td>2023-12-18T13:41:42.548630555UTC</td></tr><tr><td>142.132.202.50:47657</td><td>althea_417834-3</td><td>cryptobtcbuyer 🟢</td><td>2437608</td><td>2337608</td><td>False</td><td>off</td><td>0</td><td>2023-12-18T13:41:48.985872614UTC</td></tr><tr><td>135.181.210.171:17887</td><td>althea_417834-3</td><td>STAVR-Service 🟢</td><td>2437607</td><td>2437501</td><td>False</td><td>on</td><td>0</td><td>2023-12-18T13:41:46.089746494UTC</td></tr></table>
