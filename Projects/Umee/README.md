<h1 align="center"> 🔥Umee🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Umee)
=
# StateSync Umee
```python
SNAP_RPC=http://umee.rpc.m.stavr.tech:10457
peers="c014463cb2de618bef420e40f503c5e57decade4@umee.peers.m.stavr.tech:10456"
sed -i -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" ~/.umee/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.umee/config/config.toml
umeed tendermint unsafe-reset-all --home $HOME/.umee
wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
# SnapShot (~0.9 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop umeed
cp $HOME/.umee/data/priv_validator_state.json $HOME/.umee/priv_validator_state.json.backup
rm -rf $HOME/.umee/data
curl -o - -L http://umee.snapshot.stavr.tech:1000/umee/umee-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.umee --strip-components 2
wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"
mv $HOME/.umee/priv_validator_state.json.backup $HOME/.umee/data/priv_validator_state.json
sudo systemctl restart umeed && journalctl -u umeed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Umee/staking             `Indexer "ON"` \
🔥EXPLORER Testnet🔥:        https://explorer.stavr.tech/umee-canon/staking      `Indexer "ON"` \
🔥API Mainnet🔥:                   https://umee.api.m.stavr.tech \
🔥API Testnet🔥:                     https://umee.api.t.stavr.tech \
🔥RPC🔥:                                   http://umee.rpc.m.stavr.tech:10457                     `Snapshot-interval = 300` \
🔥gRPC🔥:                              http://umee.grpc.m.stavr.tech:1190 \
🔥peer🔥:                     `c014463cb2de618bef420e40f503c5e57decade4@umee.peers.m.stavr.tech:10456` \
🔥Addrbook🔥:    ```wget -O $HOME/.umee/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O Ume https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Umee/Ume && chmod +x Ume && ./Ume``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Umee/Decentralization)🔥

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

[raw json Mainnet](https://rpc-check.umeem.stavr.tech/umeem/rpc-umeem-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>10178179</td><td>5167386</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:35:09.743147111UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>10178164</td><td>7100001</td><td>False</td><td>on</td><td>35105594</td><td>2024-01-17T14:33:39.695792017UTC</td></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>10178175</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:34:44.541312313UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>10178179</td><td>8262001</td><td>False</td><td>off</td><td>38284999</td><td>2024-01-17T14:35:09.430929124UTC</td></tr><tr><td>85.10.197.58:13657</td><td>umee-1</td><td>BRAND-umee-main 🟢</td><td>10178167</td><td>8427832</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:33:57.182986847UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>10178157</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:33:00.424598505UTC</td></tr><tr><td>185.162.249.161:27657</td><td>umee-1</td><td>ttt 🟢</td><td>10178172</td><td>9733423</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:34:27.074696747UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>10178165</td><td>9984137</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:33:46.362342472UTC</td></tr><tr><td>65.21.91.99:16857</td><td>umee-1</td><td>Staketab-snapshot 🟢</td><td>10178169</td><td>9992001</td><td>False</td><td>off</td><td>0</td><td>2024-01-17T14:34:10.346775009UTC</td></tr><tr><td>65.108.106.252:26657</td><td>umee-1</td><td>qubelabs 🔴</td><td>10178167</td><td>10042989</td><td>False</td><td>on</td><td>36753427</td><td>2024-01-17T14:33:57.517776325UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>10178182</td><td>10078182</td><td>False</td><td>off</td><td>37401369</td><td>2024-01-17T14:35:29.096758801UTC</td></tr><tr><td>94.250.203.6:26697</td><td>umee-1</td><td>AlexRPC 🟢</td><td>10178165</td><td>10132001</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:33:52.863044608UTC</td></tr><tr><td>202.65.150.1:1556</td><td>umee-1</td><td>snap 🟢</td><td>10178174</td><td>10176583</td><td>False</td><td>on</td><td>0</td><td>2024-01-17T14:34:40.182327644UTC</td></tr></table>
