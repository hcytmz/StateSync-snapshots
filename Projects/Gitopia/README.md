<h1 align="center"> 🔥Gitopia🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Gitopia)
=

<h1 align="center"> MAINNET</h1>

# StateSync
```python
SNAP_RPC=http://gitopia.rpc.m.stavr.tech:51057
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
🔥RPC🔥:           http://gitopia.rpc.m.stavr.tech:51057              `Snapshot-interval = 300` \
🔥GRPC🔥:          http://gitopia.grpc.m.stavr.tech:5123 \
🔥peer🔥:					 `6f9f729f2d4a9c3cbab3130157f5200a61bbb273@gitopia.peers.stavr.tech:51056` \
🔥Addrbook🔥:    ```wget -O $HOME/.gitopia/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O gitopm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Gitopia/gitopm && chmod +x gitopm && ./gitopm``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Gitopia/Decentralization)🔥

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

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>213.239.194.132:14157</td><td>gitopia</td><td>semalist 🔴</td><td>11646882</td><td>6071990</td><td>False</td><td>off</td><td>430705</td><td>2024-01-03T07:30:48.054340252UTC</td></tr><tr><td>144.76.174.27:21657</td><td>gitopia</td><td>kokos 🔴</td><td>11646888</td><td>6071990</td><td>False</td><td>off</td><td>936374</td><td>2024-01-03T07:30:57.774001216UTC</td></tr><tr><td>142.132.202.86:20001</td><td>gitopia</td><td>ramuchi.tech 🟢</td><td>11646886</td><td>6548337</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:30:55.071199671UTC</td></tr><tr><td>65.108.226.26:20657</td><td>gitopia</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>11646897</td><td>6846001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:31:16.894217057UTC</td></tr><tr><td>135.181.133.249:12857</td><td>gitopia</td><td>StakeUp_rpc 🟢</td><td>11646886</td><td>8010001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:30:55.405896146UTC</td></tr><tr><td>65.108.75.107:30657</td><td>gitopia</td><td>node 🟢</td><td>11646893</td><td>8802845</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:31:06.267570918UTC</td></tr><tr><td>148.251.235.130:11657</td><td>gitopia</td><td>snap-gitopia 🟢</td><td>11646886</td><td>9516001</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:30:54.813394924UTC</td></tr><tr><td>65.108.141.109:30657</td><td>gitopia</td><td>node 🟢</td><td>11646886</td><td>10145845</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:30:54.560759608UTC</td></tr><tr><td>152.53.16.81:27057</td><td>gitopia</td><td>openstake.net 🔴</td><td>11646868</td><td>10455001</td><td>False</td><td>off</td><td>12631</td><td>2024-01-03T07:30:21.989012834UTC</td></tr><tr><td>174.138.180.190:46657</td><td>gitopia</td><td>UTSA_guide 🟢</td><td>11646875</td><td>11194706</td><td>False</td><td>on</td><td>0</td><td>2024-01-03T07:30:32.886076760UTC</td></tr></table>
