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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>5.196.198.35:26657</td><td>side-testnet-2</td><td>vps15 🔴</td><td>218152</td><td>1</td><td>False</td><td>on</td><td>107</td><td>2024-03-09T13:28:35.979757310UTC</td></tr><tr><td>13.229.128.177:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>229587</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-09T13:28:37.169838741UTC</td></tr><tr><td>65.21.226.187:26657</td><td>side-testnet-2</td><td>Sr20de 🔴</td><td>229587</td><td>1</td><td>False</td><td>on</td><td>39421</td><td>2024-03-09T13:28:37.472248637UTC</td></tr><tr><td>178.32.28.180:26657</td><td>side-testnet-2</td><td>vps5 🔴</td><td>215937</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-09T13:28:38.550992954UTC</td></tr><tr><td>84.247.134.49:12557</td><td>side-testnet-2</td><td>BANYUMAS||NGAPAK 🔴</td><td>229587</td><td>1</td><td>False</td><td>off</td><td>353</td><td>2024-03-09T13:28:38.853518376UTC</td></tr><tr><td>5.196.247.120:26657</td><td>side-testnet-2</td><td>vps11 🔴</td><td>221170</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-09T13:28:41.976053514UTC</td></tr><tr><td>168.119.10.134:26642</td><td>side-testnet-2</td><td>TrustedPoint 🔴</td><td>229589</td><td>1</td><td>False</td><td>off</td><td>20038171</td><td>2024-03-09T13:28:48.636418731UTC</td></tr><tr><td>202.182.119.24:26657</td><td>side-testnet-2</td><td>testnet-rpc 🟢</td><td>229589</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-09T13:28:49.962319162UTC</td></tr><tr><td>91.134.196.103:26657</td><td>side-testnet-2</td><td>vps8 🔴</td><td>222211</td><td>1</td><td>False</td><td>on</td><td>165</td><td>2024-03-09T13:29:02.110853865UTC</td></tr><tr><td>51.255.228.100:26657</td><td>side-testnet-2</td><td>vps9 🔴</td><td>217463</td><td>1</td><td>False</td><td>on</td><td>90</td><td>2024-03-09T13:29:05.048255194UTC</td></tr><tr><td>95.217.148.179:26657</td><td>side-testnet-2</td><td>ksalab 🔴</td><td>229589</td><td>6001</td><td>False</td><td>off</td><td>45907</td><td>2024-03-09T13:28:46.361181233UTC</td></tr><tr><td>65.109.82.106:11157</td><td>side-testnet-2</td><td>2XS 🔴</td><td>229587</td><td>10001</td><td>False</td><td>off</td><td>324</td><td>2024-03-09T13:28:33.036208826UTC</td></tr><tr><td>144.217.68.182:26357</td><td>side-testnet-2</td><td>Nodeist-side-test 🔴</td><td>229590</td><td>123001</td><td>False</td><td>off</td><td>20039254</td><td>2024-03-09T13:28:54.605423347UTC</td></tr><tr><td>176.9.126.85:31002</td><td>side-testnet-2</td><td>CryptoSJnetRPC 🟢</td><td>229591</td><td>159785</td><td>False</td><td>on</td><td>0</td><td>2024-03-09T13:29:01.240637229UTC</td></tr></table>