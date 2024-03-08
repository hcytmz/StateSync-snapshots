<h1 align="center"> 🔥Regen Network🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Regen)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://regen.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.regen/config/config.toml
regen tendermint unsafe-reset-all
wget -O $HOME/.regen/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/addrbook.json"
sudo systemctl restart regen && sudo journalctl -u regen -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop regen
cp $HOME/.regen/data/priv_validator_state.json $HOME/.regen/priv_validator_state.json.backup
rm -rf $HOME/.regen/data
curl -o - -L https://regen.snapshot.stavr.tech/regen/regen-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.regen --strip-components 2
mv $HOME/.regen/priv_validator_state.json.backup $HOME/.regen/data/priv_validator_state.json
wget -O $HOME/.regen/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/addrbook.json"
sudo systemctl restart regen && journalctl -u regen -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Regen-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://regen.api.m.stavr.tech \
🔥RPC🔥:          https://regen.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC🔥:         http://regen.grpc.m.stavr.tech:124 \
🔥seed🔥:      `dc7121500d58d40c98f06f14d5a9065935a7adf6@regen.seed.stavr.tech:2126` \
🔥Genesis🔥:   `wget -O $HOME/.regen/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/genesis.json"` \
🔥Addrbook🔥:  `wget -O $HOME/.regen/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/addrbook.json"` \
🔥Auto_install script🔥:`wget -O regenm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Regen/regenm && chmod +x regenm && ./regenm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Regen/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.regenm.stavr.tech/regenm/rpc-regenm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>3.23.48.152:26657</td><td>regen-1</td><td>rndArchive 🟢</td><td>15035572</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:31:22.691132537UTC</td></tr><tr><td>3.22.22.248:26657</td><td>regen-1</td><td>rnd-fullnode 🟢</td><td>15035570</td><td>4134001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:31:09.780937195UTC</td></tr><tr><td>104.236.201.138:26657</td><td>regen-1</td><td>vitwit-seed1 🟢</td><td>15035556</td><td>8943001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:29:50.628305069UTC</td></tr><tr><td>95.217.109.223:6767</td><td>regen-1</td><td>Spanish-rpc 🟢</td><td>15035582</td><td>10068001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:32:23.666016148UTC</td></tr><tr><td>142.132.132.184:14857</td><td>regen-1</td><td>Validatrium.com-rpc 🟢</td><td>15035583</td><td>11175001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:32:25.957955087UTC</td></tr><tr><td>141.95.104.188:26657</td><td>regen-1</td><td>Stakely.io 🟢</td><td>15035566</td><td>13442501</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:30:48.518293671UTC</td></tr><tr><td>134.209.237.188:26657</td><td>regen-1</td><td>test 🟢</td><td>15035589</td><td>13992001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:33:05.694633539UTC</td></tr><tr><td>135.181.216.151:30657</td><td>regen-1</td><td>fastsync 🟢</td><td>15035574</td><td>14457001</td><td>False</td><td>off</td><td>0</td><td>2024-03-08T21:31:36.038034505UTC</td></tr><tr><td>135.181.229.110:51657</td><td>regen-1</td><td>rpc 🟢</td><td>15035565</td><td>14844001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:30:39.473374169UTC</td></tr><tr><td>5.78.86.30:26657</td><td>regen-1</td><td>catBoss 🔴</td><td>15035594</td><td>14962001</td><td>False</td><td>on</td><td>9022530806</td><td>2024-03-08T21:33:31.835939196UTC</td></tr><tr><td>135.181.210.171:2127</td><td>regen-1</td><td>STAVR-Service 🟢</td><td>15035597</td><td>15034001</td><td>False</td><td>on</td><td>0</td><td>2024-03-08T21:33:48.509903984UTC</td></tr></table>