<h1 align="center"> 🔥Umee🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Umee)
=
# StateSync Umee
```python
SNAP_RPC=https://umee.rpc.m.stavr.tech:443
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
🔥RPC🔥:                           https://umee.rpc.m.stavr.tech:443                     `Snapshot-interval = 300` \
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



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>94.130.52.123:26657</td><td>umee-1</td><td>ELYSIUM 🔴</td><td>10557438</td><td>3216011</td><td>False</td><td>on</td><td>23096614</td><td>2024-02-12T08:01:23.508575221UTC</td></tr><tr><td>135.125.4.73:26657</td><td>umee-1</td><td>rpc-1.umee.nodes.guru 🟢</td><td>10557438</td><td>5167386</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:01:23.811811030UTC</td></tr><tr><td>213.246.45.198:26657</td><td>umee-1</td><td>id577 🔴</td><td>10557425</td><td>7100001</td><td>False</td><td>on</td><td>35104889</td><td>2024-02-12T08:00:09.643244351UTC</td></tr><tr><td>5.9.106.214:10257</td><td>umee-1</td><td>node 🟢</td><td>10557434</td><td>7942001</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:01:00.202477790UTC</td></tr><tr><td>95.216.76.51:26657</td><td>umee-1</td><td>Egozit 🔴</td><td>10557437</td><td>8262001</td><td>False</td><td>off</td><td>38504898</td><td>2024-02-12T08:01:23.084551624UTC</td></tr><tr><td>65.108.235.36:19657</td><td>umee-1</td><td>umee-yieldmos-2 🟢</td><td>10557419</td><td>9575548</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T07:59:34.450523279UTC</td></tr><tr><td>65.21.91.99:16857</td><td>umee-1</td><td>Staketab-snapshot 🟢</td><td>10557430</td><td>9992001</td><td>False</td><td>off</td><td>0</td><td>2024-02-12T08:00:38.783302437UTC</td></tr><tr><td>161.97.96.91:11657</td><td>umee-1</td><td>ams-rpc 🟢</td><td>10557441</td><td>10352001</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:01:42.378841791UTC</td></tr><tr><td>185.162.249.161:27657</td><td>umee-1</td><td>ttt 🟢</td><td>10557432</td><td>10381617</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:00:51.451890387UTC</td></tr><tr><td>195.201.130.235:26657</td><td>umee-1</td><td>PRO-NODES75-RPC 🟢</td><td>10557433</td><td>10457433</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:00:57.887954635UTC</td></tr><tr><td>95.216.77.56:26657</td><td>umee-1</td><td>L0vd2 🔴</td><td>10557441</td><td>10457441</td><td>False</td><td>off</td><td>37624016</td><td>2024-02-12T08:01:42.094385173UTC</td></tr><tr><td>207.148.74.236:26657</td><td>umee-1</td><td>ContributionDAO 🟢</td><td>10557439</td><td>10484838</td><td>False</td><td>off</td><td>0</td><td>2024-02-12T08:01:31.066397979UTC</td></tr><tr><td>23.92.76.110:26657</td><td>umee-1</td><td>node 🟢</td><td>10557444</td><td>10526001</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:02:03.609251911UTC</td></tr><tr><td>135.181.210.171:10457</td><td>umee-1</td><td>STAVR-Service 🟢</td><td>10557439</td><td>10555568</td><td>False</td><td>on</td><td>0</td><td>2024-02-12T08:01:31.407417149UTC</td></tr></table>
