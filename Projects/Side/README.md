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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.196.198.35:26657</td><td>side-testnet-2</td><td>vps15 🔴</td><td>223023</td><td>1</td><td>False</td><td>on</td><td>107</td><td>2024-03-10T09:36:51.716541592UTC</td></tr><tr><td>92.222.200.48:26657</td><td>side-testnet-2</td><td>vps3 🔴</td><td>228997</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:36:52.531706115UTC</td></tr><tr><td>13.229.128.177:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>241161</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T09:36:53.740196293UTC</td></tr><tr><td>164.132.80.115:26657</td><td>side-testnet-2</td><td>alice 🔴</td><td>230327</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:36:54.605340897UTC</td></tr><tr><td>178.32.28.180:26657</td><td>side-testnet-2</td><td>vps5 🔴</td><td>222171</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:36:55.751010469UTC</td></tr><tr><td>84.247.134.49:12557</td><td>side-testnet-2</td><td>BANYUMAS||NGAPAK 🟢</td><td>241162</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T09:36:56.063210153UTC</td></tr><tr><td>5.196.247.120:26657</td><td>side-testnet-2</td><td>vps11 🔴</td><td>227272</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:36:59.019164218UTC</td></tr><tr><td>5.196.247.123:26657</td><td>side-testnet-2</td><td>vps12 🔴</td><td>223992</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:02.003171164UTC</td></tr><tr><td>178.32.28.183:26657</td><td>side-testnet-2</td><td>vps6 🔴</td><td>225413</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:07.037911867UTC</td></tr><tr><td>168.119.10.134:26642</td><td>side-testnet-2</td><td>TrustedPoint 🔴</td><td>241163</td><td>1</td><td>False</td><td>off</td><td>20040739</td><td>2024-03-10T09:37:07.575594694UTC</td></tr><tr><td>202.182.119.24:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>241164</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T09:37:08.944489528UTC</td></tr><tr><td>51.255.228.103:26657</td><td>side-testnet-2</td><td>vps10 🔴</td><td>227639</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:09.756424289UTC</td></tr><tr><td>92.222.200.51:26657</td><td>side-testnet-2</td><td>vps4 🔴</td><td>220245</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:10.632159379UTC</td></tr><tr><td>86.48.3.66:12557</td><td>side-testnet-2</td><td>vtbside 🔴</td><td>241164</td><td>1</td><td>False</td><td>off</td><td>43699</td><td>2024-03-10T09:37:10.946447408UTC</td></tr><tr><td>178.32.246.251:26657</td><td>side-testnet-2</td><td>vps13 🔴</td><td>222176</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:12.421299630UTC</td></tr><tr><td>91.134.196.100:26657</td><td>side-testnet-2</td><td>vps7 🔴</td><td>227806</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:13.434060209UTC</td></tr><tr><td>91.134.196.103:26657</td><td>side-testnet-2</td><td>vps8 🔴</td><td>228887</td><td>1</td><td>False</td><td>on</td><td>165</td><td>2024-03-10T09:37:18.768945782UTC</td></tr><tr><td>51.255.228.100:26657</td><td>side-testnet-2</td><td>vps9 🔴</td><td>221882</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:22.437337063UTC</td></tr><tr><td>95.217.148.179:26657</td><td>side-testnet-2</td><td>ksalab 🔴</td><td>241163</td><td>6001</td><td>False</td><td>off</td><td>48359</td><td>2024-03-10T09:37:07.357096749UTC</td></tr><tr><td>65.109.82.106:11157</td><td>side-testnet-2</td><td>2XS 🟢</td><td>241160</td><td>10001</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T09:36:48.889068651UTC</td></tr><tr><td>144.217.68.182:26357</td><td>side-testnet-2</td><td>Nodeist-side-test 🔴</td><td>241164</td><td>123001</td><td>False</td><td>off</td><td>20041712</td><td>2024-03-10T09:37:11.539009429UTC</td></tr><tr><td>149.202.124.43:26657</td><td>side-testnet-2</td><td>vps1 🔴</td><td>224480</td><td>161001</td><td>False</td><td>on</td><td>90</td><td>2024-03-10T09:37:19.623412394UTC</td></tr></table>