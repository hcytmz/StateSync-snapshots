<h1 align="center"> 🔥Gitopia🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Gitopia)
=

<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=https://gitopia.rpc.m.stavr.tech:443
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.gitopia/config/config.toml
gitopiad tendermint unsafe-reset-all --home /root/.gitopia
wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"
systemctl restart gitopiad && journalctl -u gitopiad -f -o cat
```
# SnapShot (~2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop gitopiad
cp $HOME/.gitopia/data/priv_validator_state.json $HOME/.gitopia/priv_validator_state.json.backup
rm -rf $HOME/.gitopia/data
curl -o - -L http://gitopia.snapshot.stavr.tech:1030/gitopia/gitopia-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.gitopia --strip-components 2
mv $HOME/.gitopia/priv_validator_state.json.backup $HOME/.gitopia/data/priv_validator_state.json
wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"
sudo systemctl restart gitopiad && journalctl -u gitopiad -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:      https://explorer.stavr.tech/Gitopia-M/staking  `Indexer "ON"` \
🔥API🔥: 			 		 https://gitopia.api.m.stavr.tech \
🔥RPC🔥:           https://gitopia.rpc.m.stavr.tech:443              `Snapshot-interval = 300` \
🔥GRPC🔥:          http://gitopia.grpc.m.stavr.tech:5123 \
🔥peer🔥:					 `6f9f729f2d4a9c3cbab3130157f5200a61bbb273@gitopia.peers.stavr.tech:51056` \
🔥Addrbook🔥:    ```wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O gitopm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/gitopm && chmod +x gitopm && ./gitopm```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Gitopia/Decentralization)🔥
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

[raw Mainnet json](https://rpc-check.gitopm.stavr.tech/gitopm/rpc-gitopm-result.json)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>142.132.202.86:20001</td><td>gitopia</td><td>ramuchi.tech 🟢</td><td>14753478</td><td>6548337</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:36.999615952UTC</td></tr><tr><td>135.181.133.249:12857</td><td>gitopia</td><td>StakeUp_rpc 🟢</td><td>14753478</td><td>8010001</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:37.306887335UTC</td></tr><tr><td>152.53.16.81:27057</td><td>gitopia</td><td>openstake.net 🔴</td><td>14753458</td><td>10455001</td><td>False</td><td>off</td><td>54193</td><td>2024-03-03T19:01:56.381828154UTC</td></tr><tr><td>65.108.141.109:30657</td><td>gitopia</td><td>node 🟢</td><td>14753477</td><td>12299845</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:34.479387183UTC</td></tr><tr><td>138.201.21.197:26657</td><td>gitopia</td><td>StakeTown-API 🟢</td><td>14753481</td><td>12733501</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:41.693961042UTC</td></tr><tr><td>144.126.200.166:26657</td><td>gitopia</td><td>tester-121 🟢</td><td>14753460</td><td>12832814</td><td>False</td><td>off</td><td>0</td><td>2024-03-03T19:01:58.725879710UTC</td></tr><tr><td>144.76.29.90:46657</td><td>gitopia</td><td>UTSA_guide 🟢</td><td>14753476</td><td>13035301</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:27.988327537UTC</td></tr><tr><td>148.251.235.130:11657</td><td>gitopia</td><td>snap-gitopia 🟢</td><td>14753477</td><td>14079001</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:34.729740568UTC</td></tr><tr><td>65.108.75.107:30657</td><td>gitopia</td><td>node 🟢</td><td>14753485</td><td>14269230</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:48.103409351UTC</td></tr><tr><td>66.45.246.166:51057</td><td>gitopia</td><td>STAVR-Service 🟢</td><td>14753452</td><td>14745401</td><td>False</td><td>on</td><td>0</td><td>2024-03-03T19:02:17.599056095UTC</td></tr></table>
