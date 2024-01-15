<h1 align="center"> 🔥Ojo🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Ojo)
=

<h1 align="center"> TESTNET</h1>

# StateSync Ojo Testnet
```python
SNAP_RPC=http://ojo.rpc.t.stavr.tech:37097
peers="1f091cf9567c0d72a0f93877007379e0298b8860@ojo.peer.stavr.tech:37096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.ojo/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.ojo/config/config.toml
ojod tendermint unsafe-reset-all --home /root/.ojo --keep-addr-book
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.ojo/config/app.toml
sudo systemctl restart ojod && journalctl -u ojod -f -o cat
```
# SnapShot (~0.4 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop ojod
cp $HOME/.ojo/data/priv_validator_state.json $HOME/.ojo/priv_validator_state.json.backup
rm -rf $HOME/.ojo/data
curl -o - -L http://ojo.snapshot.stavr.tech:1026/ojo/ojo-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.ojo --strip-components 2
mv $HOME/.ojo/priv_validator_state.json.backup $HOME/.ojo/data/priv_validator_state.json
wget -O $HOME/.ojo/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/addrbook.json"
sudo systemctl restart ojod && journalctl -u ojod -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:        https://explorer.stavr.tech/Ojo-Devnet/staking        `Indexer "ON"` \
🔥API🔥:                     https://ojo.api.t.stavr.tech \
🔥RPC🔥:                    http://ojo.rpc.t.stavr.tech:37097              `Snapshot-interval = 100` \
🔥gRPC🔥:                  http://ojo.grpc.t.stavr.tech:7729 \
🔥peer🔥:                   `1f091cf9567c0d72a0f93877007379e0298b8860@ojo.peer.stavr.tech:37096` \
🔥Genesis🔥:    ```wget -O $HOME/.ojo/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/genesis.json"``` \
🔥Addrbook🔥:    ```wget -O $HOME/.ojo/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O ojjo https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Ojo/ojjo && chmod +x ojjo && ./ojjo``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Ojo/Decentralization)🔥



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

[raw json Testnet](https://rpc-check.ojot.stavr.tech/ojot/rpc-ojot-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.108.199.120:54657</td><td>ojo-devnet</td><td>RAMZES 🔴</td><td>4974457</td><td>306156</td><td>False</td><td>on</td><td>15420</td><td>2024-01-15T11:44:49.640228343UTC</td></tr><tr><td>136.243.88.91:7331</td><td>ojo-devnet</td><td>ojo_testnet 🔴</td><td>4974458</td><td>308845</td><td>False</td><td>on</td><td>1000</td><td>2024-01-15T11:44:55.899225205UTC</td></tr><tr><td>142.132.209.236:21657</td><td>ojo-devnet</td><td>node 🔴</td><td>4974461</td><td>350001</td><td>False</td><td>on</td><td>1999</td><td>2024-01-15T11:45:11.440230133UTC</td></tr><tr><td>65.109.70.45:16657</td><td>ojo-devnet</td><td>L0vd.com 🔴</td><td>4974463</td><td>695918</td><td>False</td><td>off</td><td>998</td><td>2024-01-15T11:45:21.467327767UTC</td></tr><tr><td>158.220.92.97:26677</td><td>ojo-devnet</td><td>AVIAONE 🔴</td><td>4974460</td><td>2754001</td><td>False</td><td>on</td><td>19926</td><td>2024-01-15T11:45:06.489539001UTC</td></tr><tr><td>95.217.225.212:36657</td><td>ojo-devnet</td><td>Firstcome 🔴</td><td>4974458</td><td>2985946</td><td>False</td><td>on</td><td>13566</td><td>2024-01-15T11:44:55.665538688UTC</td></tr><tr><td>213.239.194.132:50657</td><td>ojo-devnet</td><td>semalist 🔴</td><td>4974457</td><td>3223522</td><td>False</td><td>on</td><td>21037</td><td>2024-01-15T11:44:49.883915291UTC</td></tr><tr><td>95.217.224.252:19657</td><td>ojo-devnet</td><td>Galaxynode 🔴</td><td>4974463</td><td>3685492</td><td>False</td><td>on</td><td>11888</td><td>2024-01-15T11:45:18.764435200UTC</td></tr><tr><td>65.108.238.61:20657</td><td>ojo-devnet</td><td>alex 🔴</td><td>4974457</td><td>4158001</td><td>False</td><td>on</td><td>11359</td><td>2024-01-15T11:44:49.324930150UTC</td></tr><tr><td>78.46.99.50:22657</td><td>ojo-devnet</td><td>Staketab 🔴</td><td>4974463</td><td>4254801</td><td>False</td><td>on</td><td>1276</td><td>2024-01-15T11:45:21.716618137UTC</td></tr><tr><td>178.18.254.211:11657</td><td>ojo-devnet</td><td>CosmoBook 🔴</td><td>4974462</td><td>4392001</td><td>False</td><td>off</td><td>1057</td><td>2024-01-15T11:45:13.842506322UTC</td></tr><tr><td>51.159.220.202:26657</td><td>ojo-devnet</td><td>Blockscope.net 🔴</td><td>4974457</td><td>4425001</td><td>False</td><td>on</td><td>1707</td><td>2024-01-15T11:44:48.955147283UTC</td></tr><tr><td>88.198.32.17:39657</td><td>ojo-devnet</td><td>node 🔴</td><td>4974462</td><td>4710001</td><td>False</td><td>on</td><td>85924</td><td>2024-01-15T11:45:14.096765268UTC</td></tr><tr><td>142.132.134.112:25357</td><td>ojo-devnet</td><td>Pro-Nodes75 🔴</td><td>4974458</td><td>4874458</td><td>False</td><td>on</td><td>24651</td><td>2024-01-15T11:44:52.888803768UTC</td></tr><tr><td>65.21.170.3:38657</td><td>ojo-devnet</td><td>Munris 🔴</td><td>4974458</td><td>4874458</td><td>False</td><td>off</td><td>20123</td><td>2024-01-15T11:44:55.321092831UTC</td></tr><tr><td>138.201.85.176:26697</td><td>ojo-devnet</td><td>ojo-devnet 🔴</td><td>4974463</td><td>4874463</td><td>False</td><td>on</td><td>1000024000</td><td>2024-01-15T11:45:21.108288525UTC</td></tr><tr><td>65.109.93.152:33657</td><td>ojo-devnet</td><td>AlxVoy 🔴</td><td>4974461</td><td>4943001</td><td>False</td><td>on</td><td>4491415</td><td>2024-01-15T11:45:11.180633270UTC</td></tr><tr><td>213.239.207.175:47657</td><td>ojo-devnet</td><td>landeros 🔴</td><td>4974460</td><td>4967924</td><td>False</td><td>off</td><td>11083</td><td>2024-01-15T11:45:06.742669481UTC</td></tr><tr><td>135.181.210.171:37097</td><td>ojo-devnet</td><td>STAVR-Service 🟢</td><td>4974457</td><td>4972501</td><td>False</td><td>on</td><td>0</td><td>2024-01-15T11:44:50.510217915UTC</td></tr></table>
