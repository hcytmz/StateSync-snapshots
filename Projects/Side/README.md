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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>92.222.200.48:26657</td><td>side-testnet-2</td><td>vps3 🟢</td><td>306758</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:30.117407069UTC</td></tr><tr><td>13.229.128.177:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>342861</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:31.299425460UTC</td></tr><tr><td>164.132.80.115:26657</td><td>side-testnet-2</td><td>alice 🟢</td><td>321675</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:32.281631547UTC</td></tr><tr><td>178.32.28.180:26657</td><td>side-testnet-2</td><td>vps5 🟢</td><td>288435</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:33.047013121UTC</td></tr><tr><td>176.31.17.87:26657</td><td>side-testnet-2</td><td>vps14 🟢</td><td>287937</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:33.819471780UTC</td></tr><tr><td>84.247.134.49:12557</td><td>side-testnet-2</td><td>BANYUMAS||NGAPAK 🟢</td><td>342862</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-17T10:45:34.112850487UTC</td></tr><tr><td>5.196.247.120:26657</td><td>side-testnet-2</td><td>vps11 🟢</td><td>304612</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:37.072490037UTC</td></tr><tr><td>5.196.247.123:26657</td><td>side-testnet-2</td><td>vps12 🟢</td><td>294821</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:39.880449927UTC</td></tr><tr><td>178.32.28.183:26657</td><td>side-testnet-2</td><td>vps6 🟢</td><td>295919</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:42.888794491UTC</td></tr><tr><td>202.182.119.24:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>342864</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:46.802257890UTC</td></tr><tr><td>51.255.228.103:26657</td><td>side-testnet-2</td><td>vps10 🟢</td><td>305753</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:47.634794276UTC</td></tr><tr><td>92.222.200.51:26657</td><td>side-testnet-2</td><td>vps4 🟢</td><td>262258</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:48.486808727UTC</td></tr><tr><td>178.32.246.251:26657</td><td>side-testnet-2</td><td>vps13 🟢</td><td>271546</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:49.919421714UTC</td></tr><tr><td>91.134.196.100:26657</td><td>side-testnet-2</td><td>vps7 🟢</td><td>305245</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:50.724239132UTC</td></tr><tr><td>91.134.196.103:26657</td><td>side-testnet-2</td><td>vps8 🟢</td><td>305737</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:55.861357489UTC</td></tr><tr><td>51.255.228.100:26657</td><td>side-testnet-2</td><td>vps9 🟢</td><td>269765</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:59.417297835UTC</td></tr><tr><td>95.217.148.179:26657</td><td>side-testnet-2</td><td>ksalab 🔴</td><td>342863</td><td>6001</td><td>False</td><td>off</td><td>72795</td><td>2024-03-17T10:45:43.219696954UTC</td></tr><tr><td>65.109.82.106:11157</td><td>side-testnet-2</td><td>2XS 🟢</td><td>342860</td><td>10001</td><td>False</td><td>off</td><td>0</td><td>2024-03-17T10:45:27.192410954UTC</td></tr><tr><td>144.217.68.182:26357</td><td>side-testnet-2</td><td>Nodeist-side-test 🔴</td><td>342864</td><td>123001</td><td>False</td><td>off</td><td>20063310</td><td>2024-03-17T10:45:49.107084391UTC</td></tr><tr><td>149.202.124.43:26657</td><td>side-testnet-2</td><td>vps1 🟢</td><td>296626</td><td>161001</td><td>False</td><td>on</td><td>0</td><td>2024-03-17T10:45:56.634676739UTC</td></tr><tr><td>116.203.95.66:26657</td><td>side-testnet-2</td><td>Andromeda 🔴</td><td>342863</td><td>181001</td><td>False</td><td>off</td><td>20067262</td><td>2024-03-17T10:45:42.130379364UTC</td></tr><tr><td>168.119.10.134:26642</td><td>side-testnet-2</td><td>TrustedPoint 🟢</td><td>342817</td><td>266001</td><td>False</td><td>off</td><td>0</td><td>2024-03-17T10:45:45.498785424UTC</td></tr></table>