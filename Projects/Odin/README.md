<h1 align="center"> 🔥ODIN🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Odin)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://odin.rpc.m.stavr.tech:443
SEEDS=9a5b281c2d627cdf362f86721ced61a6228b87d1@odin.seed.stavr.tech:1116
cp $HOME/.odin/data/priv_validator_state.json $HOME/.odin/priv_validator_state.json.backup
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.odin/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.odin/config/config.toml
odind tendermint unsafe-reset-all --home $HOME/.odin --keep-addr-book
mv $HOME/.odin/priv_validator_state.json.backup $HOME/.odin/data/priv_validator_state.json
sudo systemctl restart odind && journalctl -u odind -f -o cat
```
# SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop odind
cp $HOME/.odin/data/priv_validator_state.json $HOME/.odin/priv_validator_state.json.backup
rm -rf $HOME/.odin/data
curl -o - -L https://odin.snapshot.stavr.tech/odin-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.odin --strip-components 2
mv $HOME/.odin/priv_validator_state.json.backup $HOME/.odin/data/priv_validator_state.json
wget -O $HOME/.odin/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Odin/addrbook.json"
sudo systemctl restart odind && journalctl -u odind -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Odin-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://odin.api.m.stavr.tech \
🔥RPC🔥:          https://odin.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://odin.grpc.m.stavr.tech:122 \
🔥peer🔥:         `9a5b281c2d627cdf362f86721ced61a6228b87d1@odin.seed.stavr.tech:1116` \
🔥Addrbook🔥:  `wget -O $HOME/.odin/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Odin/addrbook.json"` \
🔥Auto_install script🔥:`wget -O odinm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Odin/odinm && chmod +x odinm && ./odinm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Odin/Decentralization)🔥
=

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

[raw Mainnet json](https://rpc-check.odinm.stavr.tech/odinm/rpc-odinm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>34.78.212.147:26657</td><td>odin-mainnet-freya</td><td>3209091e6167 🔴</td><td>13276403</td><td>12504048</td><td>False</td><td>on</td><td>973427</td><td>2024-03-09T16:13:21.681556918UTC</td></tr><tr><td>34.38.73.153:26657</td><td>odin-mainnet-freya</td><td>3209091e6167 🔴</td><td>13276403</td><td>12504048</td><td>False</td><td>on</td><td>9850028</td><td>2024-03-09T16:13:26.003914241UTC</td></tr><tr><td>65.108.121.190:2152</td><td>odin-mainnet-freya</td><td>c6cb180f-e8bded 🟢</td><td>13276403</td><td>12504048</td><td>False</td><td>on</td><td>0</td><td>2024-03-09T16:13:28.335967307UTC</td></tr><tr><td>34.78.8.181:26657</td><td>odin-mainnet-freya</td><td>3209091e6167 🔴</td><td>13276404</td><td>12504048</td><td>False</td><td>on</td><td>15668153</td><td>2024-03-09T16:13:30.635373666UTC</td></tr><tr><td>35.195.121.14:26657</td><td>odin-mainnet-freya</td><td>odin-auditor 🟢</td><td>13276405</td><td>12504048</td><td>False</td><td>on</td><td>0</td><td>2024-03-09T16:13:32.950070378UTC</td></tr><tr><td>135.181.210.171:1117</td><td>odin-mainnet-freya</td><td>STAVR-Service 🟢</td><td>13276402</td><td>13273001</td><td>False</td><td>on</td><td>0</td><td>2024-03-09T16:13:14.340237244UTC</td></tr></table>