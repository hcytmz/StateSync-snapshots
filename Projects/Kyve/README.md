<h1 align="center"> 🔥Kyve🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Kyve)
=
# StateSync KYVE Mainnet
```python
SNAP_RPC=http://kyve.rpc.m.stavr.tech:12357
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
🔥RPC🔥:          http://kyve.rpc.m.stavr.tech:12357	              Snapshot-interval = 100 \
🔥gRPC🔥:         http://kyve.grpc.stavr.tech:7106 \
🔥peer🔥:					`23f2668adb6d7387c8bc7fdc8a9d10430a092df7@kyve.peer.stavr.tech:12356` \
🔥Addrbook🔥:    ```wget -O $HOME/.kyve/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Kyve/addrbook.json"```

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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>202.61.252.180:26657</td><td>kyve-1</td><td>dcm 🟢</td><td>4152471</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2023-12-22T09:13:05.713372674UTC</td></tr><tr><td>62.171.184.236:26657</td><td>kyve-1</td><td>bulevar 🔴</td><td>4152464</td><td>3383601</td><td>False</td><td>off</td><td>1928</td><td>2023-12-22T09:12:27.179091937UTC</td></tr><tr><td>130.255.170.126:56657</td><td>kyve-1</td><td>Sr20de 🔴</td><td>4152467</td><td>4050301</td><td>False</td><td>off</td><td>943</td><td>2023-12-22T09:12:40.396208521UTC</td></tr><tr><td>65.109.29.224:27657</td><td>kyve-1</td><td>Munris 🔴</td><td>4152465</td><td>4052465</td><td>False</td><td>off</td><td>30856</td><td>2023-12-22T09:12:29.618459830UTC</td></tr><tr><td>75.119.132.25:32657</td><td>kyve-1</td><td>moodman 🔴</td><td>4152467</td><td>4052467</td><td>False</td><td>off</td><td>7771</td><td>2023-12-22T09:12:42.860977418UTC</td></tr></table>
