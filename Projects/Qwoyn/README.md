<h1 align="center"> 🔥Qwoyn🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Cosmic_Horizon)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://qwoyn.rpc.m.stavr.tech:443
SEEDS=becf65550dd8453e36393cb2b97ca4e2494b2460@qwoyn.peer.stavr.tech:11206
cp $HOME/.qwoynd/data/priv_validator_state.json $HOME/.qwoynd/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.qwoynd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.qwoynd/config/config.toml
qwoynd tendermint unsafe-reset-all --home $HOME/.qwoynd --keep-addr-book
mv $HOME/.qwoynd/priv_validator_state.json.backup $HOME/.qwoynd/data/priv_validator_state.json
sudo systemctl restart qwoynd && journalctl -u qwoynd -f -o cat
```
# SnapShot (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop qwoynd
cp $HOME/.qwoynd/data/priv_validator_state.json $HOME/.qwoynd/priv_validator_state.json.backup
rm -rf $HOME/.qwoynd/data
curl -o - -L http://qwoyn.snapshot.stavr.tech:2/qwoynd/qwoynd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.qwoynd --strip-components 2
mv $HOME/.qwoynd/priv_validator_state.json.backup $HOME/.qwoynd/data/priv_validator_state.json
wget -O $HOME/.qwoynd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cosmic_Horizon/addrbook.json"
sudo systemctl restart qwoynd && journalctl -u qwoynd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Qwoyn-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://qwoyn.api.m.stavr.tech \
🔥RPC🔥:          https://qwoyn.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         https://qwoyn.grpc.m.stavr.tech:1907 \
🔥peer🔥:         `becf65550dd8453e36393cb2b97ca4e2494b2460@qwoyn.peer.stavr.tech:11206` \
🔥Addrbook🔥:  `wget -O $HOME/.qwoynd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cosmic_Horizon/addrbook.json"` \
🔥Genesis🔥:  `wget -O $HOME/.qwoynd/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cosmic_Horizon/genesis.json"` \
🔥Auto_install script🔥:`wget -O qwoynm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Cosmic_Horizon/qwoynm && chmod +x qwoynm && ./qwoynm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Qwoyn/Decentralization)🔥
=

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

[raw Mainnet json](https://rpc-check.qwoynm.stavr.tech/qwoynm/rpc-qwoynm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>95.70.163.108:26657</td><td>qwoyn-1</td><td>MAHOF 🔴</td><td>4070393</td><td>1</td><td>False</td><td>on</td><td>65153</td><td>2024-03-10T03:57:21.775343231UTC</td></tr><tr><td>46.4.87.147:3000</td><td>qwoyn-1</td><td>Staketab-archive 🟢</td><td>4070393</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T03:57:21.998390351UTC</td></tr><tr><td>142.132.132.184:12257</td><td>qwoyn-1</td><td>Validatrium.com-rpc 🟢</td><td>4070395</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T03:57:33.452996490UTC</td></tr><tr><td>138.201.21.121:16457</td><td>qwoyn-1</td><td>Validatrium-rpc 🟢</td><td>4070395</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T03:57:35.703370588UTC</td></tr><tr><td>65.108.44.149:13657</td><td>qwoyn-1</td><td>ams 🟢</td><td>4070396</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T03:57:42.438374038UTC</td></tr><tr><td>209.182.239.169:14657</td><td>qwoyn-1</td><td>SECARD 🔴</td><td>4070393</td><td>371001</td><td>False</td><td>on</td><td>161593</td><td>2024-03-10T03:57:21.413410486UTC</td></tr><tr><td>45.77.126.244:26657</td><td>qwoyn-1</td><td>qwoyn-full-node 🟢</td><td>4070394</td><td>2170001</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T03:57:29.177800436UTC</td></tr><tr><td>65.108.135.212:61557</td><td>qwoyn-1</td><td>Ubuntu-2204-jammy-amd64-base 🔴</td><td>4070392</td><td>2352001</td><td>False</td><td>off</td><td>137781</td><td>2024-03-10T03:57:19.024492109UTC</td></tr><tr><td>148.251.235.130:13657</td><td>qwoyn-1</td><td>snap-st 🟢</td><td>4070393</td><td>3396001</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T03:57:26.330580921UTC</td></tr><tr><td>65.109.84.115:13657</td><td>qwoyn-1</td><td>azstake 🔴</td><td>4070396</td><td>3442426</td><td>False</td><td>off</td><td>76947</td><td>2024-03-10T03:57:42.746657674UTC</td></tr><tr><td>135.181.210.171:11207</td><td>qwoyn-1</td><td>STAVR-Service 🟢</td><td>4070396</td><td>4067001</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T03:57:38.032613559UTC</td></tr></table>
