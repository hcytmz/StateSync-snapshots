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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>10041713</td><td>5167386</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:53:42.019698621UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>10041697</td><td>7100001</td><td>False</td><td>on</td><td>35105505</td><td>2024-01-08T07:52:09.300179321UTC</td></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>10041708</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:53:14.337703803UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>10041713</td><td>8262001</td><td>False</td><td>off</td><td>38162097</td><td>2024-01-08T07:53:41.652650661UTC</td></tr><tr><td>85.10.197.58:13657</td><td>umee-1</td><td>BRAND-umee-main 🟢</td><td>10041700</td><td>8427832</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:52:26.675406339UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>10041688</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:51:19.873201937UTC</td></tr><tr><td>185.162.249.161:27657</td><td>umee-1</td><td>ttt 🟢</td><td>10041705</td><td>9733423</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:52:56.417983724UTC</td></tr><tr><td>65.108.106.252:26657</td><td>umee-1</td><td>qubelabs 🔴</td><td>10041266</td><td>9761001</td><td>False</td><td>on</td><td>36641854</td><td>2024-01-08T07:52:27.067922494UTC</td></tr><tr><td>57.128.20.238:27657</td><td>umee-1</td><td>rpc 🟢</td><td>10041709</td><td>9880933</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:53:22.805953751UTC</td></tr><tr><td>195.201.130.235:26657</td><td>umee-1</td><td>PRO-NODES75-RPC 🟢</td><td>10041705</td><td>9941705</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:53:09.039289616UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>10041716</td><td>9941716</td><td>False</td><td>off</td><td>37294568</td><td>2024-01-08T07:53:59.309554081UTC</td></tr><tr><td>23.92.76.110:26657</td><td>umee-1</td><td>node 🟢</td><td>10041719</td><td>9953901</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:54:20.773368878UTC</td></tr><tr><td>194.60.201.146:26657</td><td>umee-1</td><td>medium-rpc 🟢</td><td>10041698</td><td>9984137</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:52:15.784912990UTC</td></tr><tr><td>65.21.91.99:16857</td><td>umee-1</td><td>Staketab-snapshot 🟢</td><td>10041702</td><td>9992001</td><td>False</td><td>off</td><td>0</td><td>2024-01-08T07:52:37.703654582UTC</td></tr><tr><td>94.250.203.6:26697</td><td>umee-1</td><td>AlexRPC 🟢</td><td>10041699</td><td>9998001</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:52:22.269669142UTC</td></tr><tr><td>202.65.150.1:1556</td><td>umee-1</td><td>snap 🟢</td><td>10041707</td><td>10036865</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:53:09.915785835UTC</td></tr><tr><td>135.181.210.171:10457</td><td>umee-1</td><td>STAVR-Service 🟢</td><td>10041714</td><td>10040701</td><td>False</td><td>on</td><td>0</td><td>2024-01-08T07:53:48.667678702UTC</td></tr></table>
