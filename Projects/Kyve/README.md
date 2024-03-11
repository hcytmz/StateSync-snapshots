<h1 align="center"> 🔥Kyve🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Kyve)
=
# StateSync KYVE Mainnet
```python
SNAP_RPC=https://kyve.rpc.m.stavr.tech:443
peers="23f2668adb6d7387c8bc7fdc8a9d10430a092df7@kyve.peer.stavr.tech:12356"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.kyve/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.kyve/config/config.toml
kyved tendermint unsafe-reset-all --home $HOME/.kyve --keep-addr-book
sudo systemctl restart kyved && journalctl -u kyved -f -o cat
```

## SnapShot (~1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop kyved
cp $HOME/.kyve/data/priv_validator_state.json $HOME/.kyve/priv_validator_state.json.backup
rm -rf $HOME/.kyve/data
curl -o - -L http://kyve.snapshot.stavr.tech:1007/kyve/kyve-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.kyve --strip-components 2
mv $HOME/.kyve/priv_validator_state.json.backup $HOME/.kyve/data/priv_validator_state.json
wget -O $HOME/.kyve/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Kyve/addrbook.json"
sudo systemctl restart kyved && journalctl -u kyved -f -o cat
```

<h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Kyve/staking        Indexer "ON" \
🔥API🔥: 			 		https://kyve.api.m.stavr.tech \
🔥RPC🔥:          https://kyve.rpc.m.stavr.tech:443	              Snapshot-interval = 100 \
🔥gRPC🔥:         http://kyve.grpc.stavr.tech:7106 \
🔥peer🔥:					`23f2668adb6d7387c8bc7fdc8a9d10430a092df7@kyve.peer.stavr.tech:12356` \
🔥Addrbook🔥:    ```wget -O $HOME/.kyve/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Kyve/addrbook.json"``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Kyve/Decentralization)🔥

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

[raw json Mainnet](https://rpc-check.kyvem.stavr.tech/kyvem/rpc-kyvem-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>141.95.99.111:21016</td><td>kyve-1</td><td>node 🟢</td><td>5305604</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T23:17:59.830372967UTC</td></tr><tr><td>15.235.11.136:21016</td><td>kyve-1</td><td>node 🟢</td><td>5305607</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T23:18:14.697091129UTC</td></tr><tr><td>146.59.69.211:21016</td><td>kyve-1</td><td>node 🟢</td><td>5305610</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-10T23:18:34.365240990UTC</td></tr><tr><td>194.233.93.126:26657</td><td>kyve-1</td><td>BimaSakti_SG 🔴</td><td>5305614</td><td>2646001</td><td>False</td><td>off</td><td>651</td><td>2024-03-10T23:19:02.226927401UTC</td></tr><tr><td>95.217.8.158:26657</td><td>kyve-1</td><td>StolenKrown 🔴</td><td>5305613</td><td>5193501</td><td>False</td><td>on</td><td>2499</td><td>2024-03-10T23:18:51.104130056UTC</td></tr><tr><td>75.119.132.25:32657</td><td>kyve-1</td><td>moodman 🔴</td><td>5305607</td><td>5205607</td><td>False</td><td>off</td><td>6865</td><td>2024-03-10T23:18:17.659865001UTC</td></tr><tr><td>130.255.170.126:56657</td><td>kyve-1</td><td>Sr20de 🔴</td><td>5305607</td><td>5217201</td><td>False</td><td>off</td><td>5970</td><td>2024-03-10T23:18:15.087119017UTC</td></tr><tr><td>65.108.230.113:12357</td><td>kyve-1</td><td>STAVR-Service 🟢</td><td>5305603</td><td>5302901</td><td>False</td><td>on</td><td>0</td><td>2024-03-10T23:17:53.504916942UTC</td></tr></table>
