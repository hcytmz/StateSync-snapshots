<h1 align="center"> 🔥Dymension🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

<h1 align="center"> TESTNET</h1>

# StateSync Dymension Testnet
```python
SNAP_RPC=https://dym.rpc.t.stavr.tech:443
peers="263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.dymension/config/config.toml
dymd tendermint unsafe-reset-all --home /root/.dymension
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot (~3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:     https://explorer.stavr.tech/Dymension-testnet/staking        `Indexer "ON"` \
🔥API🔥:          https://dymension.api.t.stavr.tech \
🔥RPC🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis🔥:     ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dym && chmod +x dym && ./dym``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dymension/Decentralization)🔥


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

[raw json](https://rpc-check.dymt.stavr.tech/dymt/rpc-dymt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>136.38.55.33:26657</td><td>froopyland_100-1</td><td>Silk Nodes 🟢</td><td>2059169</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:13:19.762374502UTC</td></tr><tr><td>51.15.212.195:26657</td><td>froopyland_100-1</td><td>Meria 🟢</td><td>1651535</td><td>1238063</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:12:13.012091806UTC</td></tr><tr><td>167.86.127.105:36657</td><td>froopyland_100-1</td><td>local 🟢</td><td>1651535</td><td>1318001</td><td>False</td><td>off</td><td>0</td><td>2024-01-10T07:13:18.893011797UTC</td></tr><tr><td>74.208.16.201:26647</td><td>froopyland_100-1</td><td>sentinelCumulo 🟢</td><td>2059158</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:12:16.654545173UTC</td></tr><tr><td>65.108.206.118:60757</td><td>froopyland_100-1</td><td>lesnik_utsa 🔴</td><td>2059161</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:32.590572692UTC</td></tr><tr><td>199.60.101.162:56657</td><td>froopyland_100-1</td><td>mydymnode1 🔴</td><td>2059161</td><td>1652923</td><td>False</td><td>off</td><td>2</td><td>2024-01-10T07:12:33.357062346UTC</td></tr><tr><td>88.99.61.173:36657</td><td>froopyland_100-1</td><td>deNodes 🔴</td><td>2059166</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-10T07:13:00.991440330UTC</td></tr><tr><td>135.181.58.28:10357</td><td>froopyland_100-1</td><td>Validatrium.com 🟢</td><td>2059166</td><td>1652923</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:13:01.465625625UTC</td></tr><tr><td>136.243.88.91:3241</td><td>froopyland_100-1</td><td>node 🔴</td><td>2059167</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:13:06.722610741UTC</td></tr><tr><td>176.9.48.38:26657</td><td>froopyland_100-1</td><td>MZONDER 🔴</td><td>2059168</td><td>1652923</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:13:15.273329985UTC</td></tr><tr><td>168.119.114.206:26657</td><td>froopyland_100-1</td><td>Crypton 🔴</td><td>2059170</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-10T07:13:24.721836990UTC</td></tr><tr><td>213.239.207.175:13057</td><td>froopyland_100-1</td><td>StakeUp 🔴</td><td>2059171</td><td>1652923</td><td>False</td><td>off</td><td>1</td><td>2024-01-10T07:13:30.413213175UTC</td></tr><tr><td>146.19.24.101:26647</td><td>froopyland_100-1</td><td>duality 🔴</td><td>2059165</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:53.366783388UTC</td></tr><tr><td>195.3.220.169:23467</td><td>froopyland_100-1</td><td>Olga7 🔴</td><td>2059168</td><td>1655313</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:13:15.654555536UTC</td></tr><tr><td>195.14.6.191:26657</td><td>froopyland_100-1</td><td>01node 🔴</td><td>2059170</td><td>1655732</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:13:24.408292970UTC</td></tr><tr><td>88.198.39.169:36657</td><td>froopyland_100-1</td><td>TAKESHI 🔴</td><td>2059158</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:16.924456839UTC</td></tr><tr><td>135.181.113.225:25657</td><td>froopyland_100-1</td><td>[NODERS]TEAM 🔴</td><td>2059166</td><td>1656584</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:13:01.963227816UTC</td></tr><tr><td>146.19.24.53:26557</td><td>froopyland_100-1</td><td>Jaha 🔴</td><td>2059167</td><td>1656584</td><td>False</td><td>off</td><td>1</td><td>2024-01-10T07:13:06.456759941UTC</td></tr><tr><td>89.117.49.68:26657</td><td>froopyland_100-1</td><td>dymension-test 🔴</td><td>2059170</td><td>1723012</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:13:25.134498426UTC</td></tr><tr><td>135.181.73.170:25157</td><td>froopyland_100-1</td><td>Pro-Nodes75 🔴</td><td>2059160</td><td>1759160</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:28.058626371UTC</td></tr><tr><td>142.132.134.112:23787</td><td>froopyland_100-1</td><td>dymension_rpc 🟢</td><td>2059164</td><td>1759164</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:12:50.555309143UTC</td></tr><tr><td>38.242.151.229:33657</td><td>froopyland_100-1</td><td>salomonval 🟢</td><td>2059168</td><td>1773995</td><td>False</td><td>off</td><td>0</td><td>2024-01-10T07:13:16.035290708UTC</td></tr><tr><td>192.99.160.197:26657</td><td>froopyland_100-1</td><td>NodeName 🟢</td><td>1829304</td><td>1826584</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:13:30.160186951UTC</td></tr><tr><td>66.45.236.14:46657</td><td>froopyland_100-1</td><td>Galaxynode 🟢</td><td>2059158</td><td>1938874</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:12:17.572457654UTC</td></tr><tr><td>95.217.222.4:26657</td><td>froopyland_100-1</td><td>STAVR_guide 🔴</td><td>2059168</td><td>1971362</td><td>False</td><td>off</td><td>1</td><td>2024-01-10T07:13:16.566937503UTC</td></tr><tr><td>135.181.210.171:17087</td><td>froopyland_100-1</td><td>STAVR-Service 🟢</td><td>2059159</td><td>2007663</td><td>False</td><td>on</td><td>0</td><td>2024-01-10T07:12:22.065000390UTC</td></tr><tr><td>194.233.90.134:26657</td><td>froopyland_100-1</td><td>geonodes 🔴</td><td>2059165</td><td>2015001</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:54.447907077UTC</td></tr><tr><td>5.161.57.83:26557</td><td>froopyland_100-1</td><td>Provalidator 🔴</td><td>2059158</td><td>2016682</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:13.749101080UTC</td></tr><tr><td>5.189.152.187:14657</td><td>froopyland_100-1</td><td>Equinox 🔴</td><td>2059162</td><td>2044181</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:35.870380644UTC</td></tr><tr><td>65.108.105.48:20557</td><td>froopyland_100-1</td><td>71cae993-39c4-58f8-b276-d809ef28a33e 🔴</td><td>2059164</td><td>2052923</td><td>False</td><td>on</td><td>1</td><td>2024-01-10T07:12:50.900756491UTC</td></tr></table>
