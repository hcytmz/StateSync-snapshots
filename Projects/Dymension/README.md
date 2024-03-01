[🔥OUR VALIDATOR🔥](https://restake.app/dymension/dymvaloper1amxp0k0hg4edrxg85v07t9ka2tfuhamhldgf8e)
=

<h1 align="center"> 🔥Dymension🔥</h1>

<h1 align="center"> MAINNET</h1>

[Node installation instructions Mainnet](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
=

# StateSync Dymension Mainnet
```python
SNAP_RPC=https://dym.rpc.m.stavr.tech:443
peers="e0d84deab2d0fd85f447c5c417fecbbdba584be0@dymension-m.peer.stavr.tech:17086"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.dymension/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1000)); \
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
# SnapShot Mainnet - updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L https://dymension-m.snapshot.stavr.tech/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```


<h1 align="center"> TESTNET</h1>

[Node installation instructions Testnet](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension/Testnet)
=

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
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/addrbook.json"
systemctl restart dymd && journalctl -u dymd -f -o cat

```
# SnapShot Testnet - updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop dymd
cp $HOME/.dymension/data/priv_validator_state.json $HOME/.dymension/priv_validator_state.json.backup
rm -rf $HOME/.dymension/data
curl -o - -L http://dymension.snapshot.stavr.tech:1019/dymension/dymension-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.dymension --strip-components 2
mv $HOME/.dymension/priv_validator_state.json.backup $HOME/.dymension/data/priv_validator_state.json
wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/addrbook.json"
sudo systemctl restart dymd && journalctl -u dymd -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER-M🔥:     https://explorer.stavr.tech/Dymension-Mainnet/        `Indexer "ON"` \
🔥EXPLORER-T🔥:     https://explorer.stavr.tech/Dymension-testnet/        `Indexer "ON"` \
🔥API-M🔥:          https://dymension.api.m.stavr.tech \
🔥API-T🔥:          https://dymension.api.t.stavr.tech \
🔥RPC-M🔥:          https://dym.rpc.m.stavr.tech:443                  `Snapshot-interval = 1000` \
🔥RPC-T🔥:          https://dym.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC-M🔥:         http://dymension.grpc.m.stavr.tech:7119 \
🔥gRPC-T🔥:         http://dymension.grpc.t.stavr.tech:7119 \
🔥peer-M🔥:         `e0d84deab2d0fd85f447c5c417fecbbdba584be0@dymension-m.peer.stavr.tech:17086` \
🔥peer-T🔥:         `263195d9dd5274d337c7dff03019a7fbad4ff165@dymension.peers.stavr.tech:17086` \
🔥Genesis-T🔥:     ```wget wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/genesis.json -O $HOME/.dymension/config/genesis.json``` \
🔥Addrbook-M🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/addrbook.json"``` \
🔥Addrbook-T🔥:    ```wget -O $HOME/.dymension/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/addrbook.json"``` \
🔥Auto_install script-M🔥: ```wget -O dymm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/dymm && chmod +x dymm && ./dymm``` \
🔥Auto_install script-T🔥: ```wget -O dym https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Dymension/Testnet/dym && chmod +x dym && ./dym```

<h4 align="center"> 🔥ARCHIVE NODE🔥    </h4>

API https://dym.api-archive.m.stavr.tech/ \
RPC https://dym.rpc-archive.m.stavr.tech/

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Dymension/Decentralization)🔥
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

[raw json](https://rpc-check.dymt.stavr.tech/dymt/rpc-dymt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>353206</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:06:49.974476359UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>353207</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:06:54.697288524UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>353208</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:02.245255743UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>353208</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:04.540781992UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>353211</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:17.142177076UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>353211</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:19.481973389UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>353212</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:28.136117311UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>353212</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:28.568168232UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>353213</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:31.489784860UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>353214</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:35.862441966UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>353214</td><td>1</td><td>False</td><td>off</td><td>732700</td><td>2024-03-01T02:07:40.303839128UTC</td></tr><tr><td>75.119.139.53:26667</td><td>dymension_1100-1</td><td>AVIAONE_Blockchains_Service 🟢</td><td>353215</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:44.884661988UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>353216</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:51.641605491UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>353217</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:56.334499306UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>353219</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:07.250218083UTC</td></tr><tr><td>46.4.36.190:2082</td><td>dymension_1100-1</td><td>node 🟢</td><td>353223</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:32.181068536UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>353226</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:44.726196997UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>353226</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:45.593127353UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>353228</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-03-01T02:08:56.809737653UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>353235</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:09:38.347520023UTC</td></tr><tr><td>65.109.23.55:17187</td><td>dymension_1100-1</td><td>STAVR-Archive 🟢</td><td>353237</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:09:50.935441622UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>353237</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:09:51.155698310UTC</td></tr><tr><td>65.108.74.54:2082</td><td>dymension_1100-1</td><td>node 🟢</td><td>353237</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:09:53.552306234UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>353239</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:10:02.087651201UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>353239</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:10:02.433228112UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>353207</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:06:54.380818789UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>353215</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:45.199098541UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>353227</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:49.961044313UTC</td></tr><tr><td>212.23.222.109:26757</td><td>dymension_1100-1</td><td>jaha_rpc 🟢</td><td>353217</td><td>40001</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:07:56.095124727UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>353219</td><td>202400</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:07.032621147UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>353207</td><td>316001</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:06:57.363391132UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>353227</td><td>327801</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:08:52.339680001UTC</td></tr><tr><td>109.199.118.239:14657</td><td>dymension_1100-1</td><td>VNBNODE 🟢</td><td>353221</td><td>333592</td><td>False</td><td>off</td><td>0</td><td>2024-03-01T02:08:21.804243802UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>353229</td><td>352001</td><td>False</td><td>on</td><td>0</td><td>2024-03-01T02:09:05.386415204UTC</td></tr></table>
