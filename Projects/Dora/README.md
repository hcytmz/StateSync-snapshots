<h1 align="center"> 🔥Dora Testnet🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/DORA)
=

<h1 align="center"> TESTNET</h1>

# StateSync Dora Testnet
```python
SNAP_RPC=https://dora.rpc.t.stavr.tech:443
peers="3c21389d10b9499df09a7eb36afa8e748433c286@dora-t.peer.stavr.tech:32046"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dora/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dora/config/config.toml
dorad tendermint unsafe-reset-all --home /root/.dora
systemctl restart dorad && journalctl -u dorad -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dorad
cp $HOME/.dora/data/priv_validator_state.json $HOME/.dora/priv_validator_state.json.backup
rm -rf $HOME/.dora/data
curl -o - -L https://dorat.snapshot.stavr.tech/dora-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dora --strip-components 2
curl -o - -L http://dorat.wasm.stavr.tech:1103/wasm-dora.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dora --strip-components 2
mv $HOME/.dora/priv_validator_state.json.backup $HOME/.dora/data/priv_validator_state.json
wget -O $HOME/.dora/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/DORA/addrbook.json"
sudo systemctl restart dorad && journalctl -u dorad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER-T🔥: https://explorer.stavr.tech/Dora-Testnet        `Indexer "ON"` \
🔥API-T🔥:      https://dora.api.t.stavr.tech \
🔥RPC-T🔥:      https://dora.rpc.t.stavr.tech:443              `Snapshot-interval = 1000` \
🔥gRPC-T🔥:     http://dora.grpc.t.stavr.tech:1912 \
🔥peer-T🔥:     `3c21389d10b9499df09a7eb36afa8e748433c286@dora-t.peer.stavr.tech:32046` \
🔥WASM-T🔥:     ```curl -o - -L http://dorat.wasm.stavr.tech:1103/wasm-dora.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dora --strip-components 2``` \
🔥Genesis-T🔥:  ```wget -O $HOME/.dora/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/DORA/genesis.json"``` \
🔥Addrbook-T🔥: ```wget -O $HOME/.dora/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/DORA/addrbook.json"``` \
🔥Auto_install script-T🔥:  `wget -O dorat https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/DORA/dorat && chmod +x dorat && ./dorat` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dora/Decentralization)🔥

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

[Testnet raw json](https://rpc-check.dorat.stavr.tech/dorat/rpc-dorat-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>216.158.237.22:26657</td><td>vota-vk</td><td>BlockBeacon 🔴</td><td>79337</td><td>1</td><td>False</td><td>off</td><td>9009800000000000</td><td>2023-12-25T19:09:49.819679628UTC</td></tr><tr><td>135.181.210.171:32047</td><td>vota-vk</td><td>STAVR-Service 🟢</td><td>79338</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-25T19:09:54.661861968UTC</td></tr><tr><td>18.143.75.85:26657</td><td>vota-vk</td><td>dorafactory 🟢</td><td>79338</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-25T19:09:55.599104874UTC</td></tr><tr><td>65.109.92.148:60857</td><td>vota-vk</td><td>Shoni 🔴</td><td>79338</td><td>1</td><td>False</td><td>on</td><td>9323404379593930</td><td>2023-12-25T19:09:57.303452598UTC</td></tr><tr><td>65.108.206.118:60657</td><td>vota-vk</td><td>UTSA_guide 🟢</td><td>79338</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2023-12-25T19:09:57.645459716UTC</td></tr><tr><td>213.239.207.175:13357</td><td>vota-vk</td><td>StakeUp 🔴</td><td>79337</td><td>13001</td><td>False</td><td>off</td><td>9009500000000000</td><td>2023-12-25T19:09:49.175173528UTC</td></tr><tr><td>65.109.117.219:29257</td><td>vota-vk</td><td>moodman 🔴</td><td>79337</td><td>13001</td><td>False</td><td>off</td><td>9009100000000000</td><td>2023-12-25T19:09:52.279113691UTC</td></tr><tr><td>167.235.14.83:16957</td><td>vota-vk</td><td>NodeName 🟢</td><td>79338</td><td>14001</td><td>False</td><td>on</td><td>0</td><td>2023-12-25T19:09:57.897540534UTC</td></tr><tr><td>158.69.27.233:23657</td><td>vota-vk</td><td>KYN-PUBLIC 🟢</td><td>79338</td><td>52001</td><td>False</td><td>on</td><td>0</td><td>2023-12-25T19:09:56.888072247UTC</td></tr><tr><td>135.181.176.109:36657</td><td>vota-vk</td><td>UTSA_guide 🟢</td><td>79337</td><td>55501</td><td>False</td><td>on</td><td>0</td><td>2023-12-25T19:09:48.937642511UTC</td></tr><tr><td>5.161.240.23:26657</td><td>vota-vk</td><td>RPC 🟢</td><td>79338</td><td>60001</td><td>False</td><td>off</td><td>0</td><td>2023-12-25T19:09:56.220544534UTC</td></tr></table>
