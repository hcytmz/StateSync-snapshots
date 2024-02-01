<h1 align="center"> 🔥Carbon🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Carbon)
=
<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://carbon.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.carbon/config/config.toml
carbond tendermint unsafe-reset-all
wget -O $HOME/.carbon/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Carbon/addrbook.json"
sudo systemctl restart carbond && sudo journalctl -u carbond -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop carbond
cp $HOME/.carbon/data/priv_validator_state.json $HOME/.carbon/priv_validator_state.json.backup
rm -rf $HOME/.carbon/data
curl -o - -L https://carbon.snapshot.stavr.tech/carbon-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.carbon --strip-components 2
mv $HOME/.carbon/priv_validator_state.json.backup $HOME/.carbon/data/priv_validator_state.json
wget -O $HOME/.carbon/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Carbon/addrbook.json"
sudo systemctl restart carbond && journalctl -u carbond -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Carbon-Mainnet        `Indexer "ON"` \
🔥API🔥:          https://carbon.api.m.stavr.tech \
🔥RPC🔥:          https://carbon.rpc.m.stavr.tech:443              `Snapshot-interval = 1000` \
🔥EVM-RPC🔥:      https://carbon.evm-rpc.m.stavr \
🔥gRPC🔥:         http://carbon.grpc.m.stavr.tech:100 \
🔥seed🔥:      `f5f833ec5096dc9d1dd63e7d6a2727059696590e@carbon.seed.stavr.tech:2006` \
🔥Addrbook🔥:  `wget -O $HOME/.carbon/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Carbon/addrbook.json"` \
🔥Auto_install script🔥:`wget -O carbonm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Carbon/carbonm && chmod +x carbonm && ./carbonm`

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Carbon/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.carbonm.stavr.tech/carbonm/rpc-carbonm-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.21.88.84:26657</td><td>carbon-1</td><td>ics-node1 🟢</td><td>53134827</td><td>21164241</td><td>False</td><td>off</td><td>0</td><td>2024-02-01T20:01:15.407485845UTC</td></tr><tr><td>65.108.97.115:26657</td><td>carbon-1</td><td>galaz 🔴</td><td>53134832</td><td>47374001</td><td>False</td><td>on</td><td>11237787648</td><td>2024-02-01T20:01:26.314197618UTC</td></tr><tr><td>167.235.97.158:26657</td><td>carbon-1</td><td>Wetez 🔴</td><td>53134816</td><td>48067570</td><td>False</td><td>on</td><td>1330715131</td><td>2024-02-01T20:00:50.347181730UTC</td></tr><tr><td>65.21.232.158:26657</td><td>carbon-1</td><td>polarbear 🔴</td><td>53134836</td><td>48126001</td><td>False</td><td>on</td><td>10881614682</td><td>2024-02-01T20:01:34.866165314UTC</td></tr><tr><td>51.75.61.105:26657</td><td>carbon-1</td><td>sulu 🟢</td><td>53134824</td><td>48742001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T20:01:06.489886288UTC</td></tr><tr><td>65.109.69.234:26657</td><td>carbon-1</td><td>mynode 🔴</td><td>53134805</td><td>50560001</td><td>False</td><td>off</td><td>12849688991</td><td>2024-02-01T20:00:29.516653769UTC</td></tr><tr><td>65.109.69.233:26657</td><td>carbon-1</td><td>mynode 🔴</td><td>53134805</td><td>50610001</td><td>False</td><td>off</td><td>8704822948</td><td>2024-02-01T20:00:29.155137503UTC</td></tr><tr><td>95.216.22.75:26657</td><td>carbon-1</td><td>polarbear 🟢</td><td>53134826</td><td>52338001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T20:01:13.025742675UTC</td></tr><tr><td>218.212.209.219:26657</td><td>carbon-1</td><td>grapefield 🟢</td><td>53134823</td><td>52371001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T20:01:04.145423850UTC</td></tr><tr><td>147.135.138.180:26657</td><td>carbon-1</td><td>CryptoNet 🟢</td><td>53134828</td><td>52934001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T20:01:17.792059619UTC</td></tr><tr><td>66.45.246.166:2007</td><td>carbon-1</td><td>STAVR-Service 🟢</td><td>53134823</td><td>53126001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T20:01:03.174712850UTC</td></tr><tr><td>54.38.178.85:26657</td><td>carbon-1</td><td>rpc-bh-rocks 🟢</td><td>53134839</td><td>53130001</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T20:01:39.321247422UTC</td></tr></table>
