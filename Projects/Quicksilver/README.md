<h1 align="center"> 🔥QUICKSILVER🔥</h1>

<h1 align="center"> MAINNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Quicksilver)
=

# StateSync
```python
SNAP_RPC=https://quick.rpc.m.stavr.tech:443
peers="f2846ba84070d3fdc21c09ef44bac4eeed2f8722@quick.peers.stavr.tech:21026"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.quicksilverd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 300)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.quicksilverd/config/config.toml
quicksilverd tendermint unsafe-reset-all --home $HOME/.quicksilverd --keep-addr-book
systemctl restart quicksilverd && sudo journalctl -u quicksilverd -f -o cat
```

# SnapShot (~0.4GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop quicksilverd
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.quicksilverd/config/config.toml
cp $HOME/.quicksilverd/data/priv_validator_state.json $HOME/.quicksilverd/priv_validator_state.json.backup
rm -rf $HOME/.quicksilverd/data
curl -o - -L http://quick.snapshot.stavr.tech:1009/quick/quick-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.quicksilverd --strip-components 2
mv $HOME/.quicksilverd/priv_validator_state.json.backup $HOME/.quicksilverd/data/priv_validator_state.json
wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/addrbook.json"
sudo systemctl restart quicksilverd && journalctl -u quicksilverd -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Quicksilver/Tetstnet)
=

# StateSync Testnet
```python
SNAP_RPC=https://quick.rpc.t.stavr.tech:443
peers="b3b0b1dfa5feb35b6ed88f409c2e9182784e122c@quickt.peers.stavr.tech:20026"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.quicksilverd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" ~/.quicksilverd/config/config.toml
quicksilverd tendermint unsafe-reset-all --home $HOME/.quicksilverd
systemctl restart quicksilverd && sudo journalctl -u quicksilverd -f -o cat

```

# SnapShot Testnet (~0.2GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop quicksilverd
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.quicksilverd/config/config.toml
cp $HOME/.quicksilverd/data/priv_validator_state.json $HOME/.quicksilverd/priv_validator_state.json.backup
rm -rf $HOME/.quicksilverd/data
curl -o - -L http://quickt.snapshot.stavr.tech:1016/quickt/quickt-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.quicksilverd --strip-components 2
mv $HOME/.quicksilverd/priv_validator_state.json.backup $HOME/.quicksilverd/data/priv_validator_state.json
wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/Tetstnet/addrbook.json"
sudo systemctl restart quicksilverd && journalctl -u quicksilverd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:        https://explorer.stavr.tech/Quicksilver-Mainnet/staking    `Indexer "ON"` \
🔥EXPLORER Testnet🔥:        https://explorer.stavr.tech/Quicksilver/staking	        `Indexer "ON"` \
🔥API Mainnet🔥: 			 https://quick.api.m.stavr.tech \
🔥API Testnet🔥: 			 https://quick.api.t.stavr.tech \
🔥RPC Mainnet🔥:             https://quick.rpc.m.stavr.tech:443              `Snapshot-interval = 300` \
🔥RPC Testnet🔥:             https://quick.rpc.t.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:                    http://quick.grpc.m.stavr.tech:9113 \
🔥gRPC Testnet🔥:                    http://quick.grpc.t.stavr.tech:9112 \
🔥Genesis Mainnet🔥: `wget -O $HOME/.quicksilverd/config/genesis.json https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/genesis.json` \
🔥Genesis Testnet🔥: `wget -O ~/.quicksilverd/config/genesis.json https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/Tetstnet/genesis.json` \
🔥peer Mainnet🔥:					 `f2846ba84070d3fdc21c09ef44bac4eeed2f8722@quick.peers.stavr.tech:21026` \
🔥peer Testnet🔥:					 `b3b0b1dfa5feb35b6ed88f409c2e9182784e122c@quickt.peers.stavr.tech:20026` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O quick https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/quick && chmod +x quick && ./quick``` \
🔥Auto_install script Testnet🔥: ```wget -O quicktest https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Quicksilver/Tetstnet/quicktest && chmod +x quicktest && ./quicktest```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Quicksilver/Decentralization)🔥
=

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

[raw json Mainnet](https://rpc-check.quickm.stavr.tech/quickm/rpc-quickm-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Quicksilver/Rpc-Check-Testnet)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.28.177:28657</td><td>quicksilver-2</td><td>AlxVoy 🟢</td><td>6571025</td><td>3562001</td><td>False</td><td>off</td><td>0</td><td>2024-03-26T16:21:44.978999027UTC</td></tr><tr><td>47.147.226.147:51657</td><td>quicksilver-2</td><td>Node15 🔴</td><td>6571018</td><td>5151648</td><td>False</td><td>off</td><td>924971</td><td>2024-03-26T16:21:07.642840004UTC</td></tr><tr><td>137.184.184.96:26657</td><td>quicksilver-2</td><td>Tester 🟢</td><td>6571009</td><td>5550692</td><td>False</td><td>off</td><td>0</td><td>2024-03-26T16:20:15.296241822UTC</td></tr><tr><td>75.119.144.167:26657</td><td>quicksilver-2</td><td>mahof 🔴</td><td>6571016</td><td>5654794</td><td>False</td><td>on</td><td>285749</td><td>2024-03-26T16:20:52.182931132UTC</td></tr><tr><td>142.132.136.106:22657</td><td>quicksilver-2</td><td>SERVICES 🟢</td><td>6571012</td><td>5920001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:33.107505282UTC</td></tr><tr><td>66.172.36.134:14857</td><td>quicksilver-2</td><td>node 🟢</td><td>6571005</td><td>5950756</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:19:51.294417410UTC</td></tr><tr><td>66.172.36.136:14857</td><td>quicksilver-2</td><td>node 🟢</td><td>6571006</td><td>5950756</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:19:54.093111091UTC</td></tr><tr><td>46.4.121.72:26657</td><td>quicksilver-2</td><td>nkbblocks 🟢</td><td>6571011</td><td>6056301</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:21.788536456UTC</td></tr><tr><td>65.108.195.29:31127</td><td>quicksilver-2</td><td>Staketab-snap 🟢</td><td>6571008</td><td>6075001</td><td>False</td><td>off</td><td>0</td><td>2024-03-26T16:20:06.978174719UTC</td></tr><tr><td>158.69.27.233:26657</td><td>quicksilver-2</td><td>KYN-SIDE 🟢</td><td>6571011</td><td>6159001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:26.427953695UTC</td></tr><tr><td>94.130.13.187:26657</td><td>quicksilver-2</td><td>Huginn 🟢</td><td>6365700</td><td>6231630</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:33.330981357UTC</td></tr><tr><td>57.128.175.133:26657</td><td>quicksilver-2</td><td>joe 🟢</td><td>6571001</td><td>6246344</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:19:24.769203063UTC</td></tr><tr><td>144.76.29.90:61157</td><td>quicksilver-2</td><td>UTSA_guide 🟢</td><td>6571000</td><td>6316825</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:19:24.468495868UTC</td></tr><tr><td>135.181.133.16:26657</td><td>quicksilver-2</td><td>DStake 🔴</td><td>6571001</td><td>6378597</td><td>False</td><td>on</td><td>79272</td><td>2024-03-26T16:19:23.915405779UTC</td></tr><tr><td>95.214.53.76:11157</td><td>quicksilver-2</td><td>Equinox 🔴</td><td>6571009</td><td>6459097</td><td>False</td><td>on</td><td>214741</td><td>2024-03-26T16:20:13.412275323UTC</td></tr><tr><td>116.202.217.20:26657</td><td>quicksilver-2</td><td>dteam 🟢</td><td>6571014</td><td>6474101</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:41.712595787UTC</td></tr><tr><td>135.181.229.110:31657</td><td>quicksilver-2</td><td>rpc 🟢</td><td>6571003</td><td>6479823</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:19:37.883297475UTC</td></tr><tr><td>51.68.170.145:26657</td><td>quicksilver-2</td><td>openbitlab 🟢</td><td>6571007</td><td>6507144</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:00.464536841UTC</td></tr><tr><td>161.97.82.203:26257</td><td>quicksilver-2</td><td>Fort 🟢</td><td>6571000</td><td>6565996</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:19:21.463224845UTC</td></tr><tr><td>135.181.210.171:21027</td><td>quicksilver-2</td><td>STAVR-Service 🟢</td><td>6571011</td><td>6568001</td><td>False</td><td>on</td><td>0</td><td>2024-03-26T16:20:26.721319651UTC</td></tr></table>
