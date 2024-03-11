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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.196.198.35:26657</td><td>side-testnet-2</td><td>vps15 🔴</td><td>226026</td><td>1</td><td>False</td><td>on</td><td>107</td><td>2024-03-10T21:41:56.391856717UTC</td></tr><tr><td>92.222.200.48:26657</td><td>side-testnet-2</td><td>vps3 🔴</td><td>232893</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:41:57.352243767UTC</td></tr><tr><td>13.229.128.177:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>248473</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T21:41:58.540069167UTC</td></tr><tr><td>164.132.80.115:26657</td><td>side-testnet-2</td><td>alice 🔴</td><td>234123</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:41:59.555559725UTC</td></tr><tr><td>178.32.28.180:26657</td><td>side-testnet-2</td><td>vps5 🔴</td><td>225742</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:00.608677022UTC</td></tr><tr><td>176.31.17.87:26657</td><td>side-testnet-2</td><td>vps14 🔴</td><td>224641</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:01.408415091UTC</td></tr><tr><td>84.247.134.49:12557</td><td>side-testnet-2</td><td>BANYUMAS||NGAPAK 🟢</td><td>248474</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T21:42:01.746166787UTC</td></tr><tr><td>5.196.247.120:26657</td><td>side-testnet-2</td><td>vps11 🔴</td><td>230729</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:04.582896675UTC</td></tr><tr><td>5.196.247.123:26657</td><td>side-testnet-2</td><td>vps12 🔴</td><td>227390</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:07.496638641UTC</td></tr><tr><td>178.32.28.183:26657</td><td>side-testnet-2</td><td>vps6 🔴</td><td>228737</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:12.694311048UTC</td></tr><tr><td>168.119.10.134:26642</td><td>side-testnet-2</td><td>TrustedPoint 🔴</td><td>248475</td><td>1</td><td>False</td><td>off</td><td>20042334</td><td>2024-03-10T21:42:13.207004981UTC</td></tr><tr><td>202.182.119.24:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>248476</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T21:42:14.471511242UTC</td></tr><tr><td>51.255.228.103:26657</td><td>side-testnet-2</td><td>vps10 🔴</td><td>230859</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:15.433639024UTC</td></tr><tr><td>92.222.200.51:26657</td><td>side-testnet-2</td><td>vps4 🔴</td><td>223139</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:16.248553500UTC</td></tr><tr><td>86.48.3.66:12557</td><td>side-testnet-2</td><td>vtbside 🔴</td><td>248476</td><td>1</td><td>False</td><td>off</td><td>45304</td><td>2024-03-10T21:42:16.542251412UTC</td></tr><tr><td>178.32.246.251:26657</td><td>side-testnet-2</td><td>vps13 🔴</td><td>224867</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:18.305939980UTC</td></tr><tr><td>91.134.196.100:26657</td><td>side-testnet-2</td><td>vps7 🔴</td><td>231020</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:19.406937184UTC</td></tr><tr><td>91.134.196.103:26657</td><td>side-testnet-2</td><td>vps8 🔴</td><td>232266</td><td>1</td><td>False</td><td>on</td><td>165</td><td>2024-03-10T21:42:24.676097513UTC</td></tr><tr><td>51.255.228.100:26657</td><td>side-testnet-2</td><td>vps9 🔴</td><td>224602</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:28.568881068UTC</td></tr><tr><td>95.217.148.179:26657</td><td>side-testnet-2</td><td>ksalab 🔴</td><td>248475</td><td>6001</td><td>False</td><td>off</td><td>51878</td><td>2024-03-10T21:42:12.992398886UTC</td></tr><tr><td>65.109.82.106:11157</td><td>side-testnet-2</td><td>2XS 🟢</td><td>248472</td><td>10001</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T21:41:53.293193853UTC</td></tr><tr><td>144.217.68.182:26357</td><td>side-testnet-2</td><td>Nodeist-side-test 🔴</td><td>248476</td><td>123001</td><td>False</td><td>off</td><td>20043386</td><td>2024-03-10T21:42:17.101278781UTC</td></tr><tr><td>149.202.124.43:26657</td><td>side-testnet-2</td><td>vps1 🔴</td><td>227673</td><td>161001</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T21:42:25.478361844UTC</td></tr></table>