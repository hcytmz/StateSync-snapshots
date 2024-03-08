<h1 align="center"> 🔥Side🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Side_Protocol)
=

<h1 align="center"> TESTNET</h1>

# StateSync Side Testnet
```python
SNAP_RPC=https://side.rpc.t.stavr.tech:443
peers="fe54f3964664592b3be89eb685cc72e9aecb14e9@side-t.seed.stavr.tech:21306"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.side/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.side/config/config.toml
sided tendermint unsafe-reset-all --home /root/.side
wget -O $HOME/.side/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/addrbook.json"
systemctl restart sided && journalctl -u sided -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop sided
cp $HOME/.side/data/priv_validator_state.json $HOME/.side/priv_validator_state.json.backup
rm -rf $HOME/.side/data
curl -o - -L https://side-t.snapshot.stavr.tech/side-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.side --strip-components 2
mv $HOME/.side/priv_validator_state.json.backup $HOME/.side/data/priv_validator_state.json
wget -O $HOME/.side/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/addrbook.json"
sudo systemctl restart sided && journalctl -u sided -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Side-Testnet/        `Indexer "ON"` \
🔥API🔥:      https://side.api.t.stavr.tech \
🔥RPC🔥:      https://side.rpc.t.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:     http://side.grpc.t.stavr.tech:9917 \
🔥peer🔥:     `fe54f3964664592b3be89eb685cc72e9aecb14e9@side-t.seed.stavr.tech:21306` \
🔥Addrbook🔥: ```wget -O $HOME/.side/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O sidem https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Side_Protocol/sidem && chmod +x sidem && ./sidem`

<h1 align="center"> RPC Scanning</h1>

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

[raw Testnet json](https://rpc-check.sidet.stavr.tech/sidet/rpc-sidet-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>18.183.249.187:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>218589</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T17:20:35.686897374UTC</td></tr><tr><td>13.229.128.177:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>218589</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T17:20:36.887733448UTC</td></tr><tr><td>65.21.226.187:26657</td><td>side-testnet-2</td><td>Sr20de 🔴</td><td>218589</td><td>1</td><td>False</td><td>on</td><td>27925</td><td>2024-03-08T17:20:37.200319422UTC</td></tr><tr><td>178.32.28.180:26657</td><td>side-testnet-2</td><td>vps5 🔴</td><td>211155</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-08T17:20:38.143735290UTC</td></tr><tr><td>176.31.17.87:26657</td><td>side-testnet-2</td><td>vps14 🔴</td><td>212991</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-08T17:20:39.339726969UTC</td></tr><tr><td>84.247.134.49:12557</td><td>side-testnet-2</td><td>BANYUMAS||NGAPAK 🔴</td><td>218589</td><td>1</td><td>False</td><td>off</td><td>353</td><td>2024-03-08T17:20:39.689271391UTC</td></tr><tr><td>5.196.247.120:26657</td><td>side-testnet-2</td><td>vps11 🔴</td><td>215027</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-08T17:20:42.898892138UTC</td></tr><tr><td>168.119.10.134:26642</td><td>side-testnet-2</td><td>TrustedPoint 🔴</td><td>218591</td><td>1</td><td>False</td><td>off</td><td>20028010</td><td>2024-03-08T17:20:49.522356940UTC</td></tr><tr><td>86.48.3.66:12557</td><td>side-testnet-2</td><td>vtbside 🔴</td><td>218591</td><td>1</td><td>False</td><td>off</td><td>30030</td><td>2024-03-08T17:20:51.043256995UTC</td></tr><tr><td>13.229.243.195:26657</td><td>side-testnet-2</td><td>side 🟢</td><td>218379</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T17:20:52.856970357UTC</td></tr><tr><td>178.32.246.251:26657</td><td>side-testnet-2</td><td>vps13 🔴</td><td>212858</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-08T17:20:55.747291362UTC</td></tr><tr><td>91.134.196.103:26657</td><td>side-testnet-2</td><td>vps8 🔴</td><td>215395</td><td>1</td><td>False</td><td>on</td><td>165</td><td>2024-03-08T17:21:01.267891005UTC</td></tr><tr><td>51.255.228.100:26657</td><td>side-testnet-2</td><td>vps9 🔴</td><td>212808</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-08T17:21:05.154634669UTC</td></tr><tr><td>95.217.148.179:26657</td><td>side-testnet-2</td><td>ksalab 🔴</td><td>218591</td><td>6001</td><td>False</td><td>off</td><td>34281</td><td>2024-03-08T17:20:49.308927556UTC</td></tr><tr><td>65.109.82.106:11157</td><td>side-testnet-2</td><td>2XS 🔴</td><td>218588</td><td>10001</td><td>False</td><td>off</td><td>324</td><td>2024-03-08T17:20:32.402325488UTC</td></tr><tr><td>144.217.68.182:26357</td><td>side-testnet-2</td><td>Nodeist-side-test 🔴</td><td>218591</td><td>123001</td><td>False</td><td>off</td><td>20029020</td><td>2024-03-08T17:20:51.662876946UTC</td></tr><tr><td>176.9.126.85:31002</td><td>side-testnet-2</td><td>CryptoSJnetRPC 🟢</td><td>218592</td><td>159785</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T17:21:00.393187534UTC</td></tr><tr><td>149.202.124.43:26657</td><td>side-testnet-2</td><td>vps1 🔴</td><td>213082</td><td>161001</td><td>False</td><td>on</td><td>90</td><td>2024-03-08T17:21:02.120436749UTC</td></tr></table>