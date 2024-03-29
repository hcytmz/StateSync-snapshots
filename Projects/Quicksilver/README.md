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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>65.109.28.177:28657</td><td>quicksilver-2</td><td>AlxVoy 🟢</td><td>6604034</td><td>3562001</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T21:50:44.028732878UTC</td></tr><tr><td>47.147.226.147:51657</td><td>quicksilver-2</td><td>Node15 🔴</td><td>6604027</td><td>5151648</td><td>False</td><td>off</td><td>924989</td><td>2024-03-28T21:50:04.772021763UTC</td></tr><tr><td>137.184.184.96:26657</td><td>quicksilver-2</td><td>Tester 🟢</td><td>6604018</td><td>5550692</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T21:49:12.484208255UTC</td></tr><tr><td>75.119.144.167:26657</td><td>quicksilver-2</td><td>mahof 🔴</td><td>6604024</td><td>5654794</td><td>False</td><td>on</td><td>285933</td><td>2024-03-28T21:49:47.171192121UTC</td></tr><tr><td>142.132.136.106:22657</td><td>quicksilver-2</td><td>SERVICES 🟢</td><td>6604021</td><td>5920001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:49:28.304702029UTC</td></tr><tr><td>66.172.36.134:14857</td><td>quicksilver-2</td><td>node 🟢</td><td>6604014</td><td>5950756</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:49.441983071UTC</td></tr><tr><td>66.172.36.136:14857</td><td>quicksilver-2</td><td>node 🟢</td><td>6604015</td><td>5950756</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:52.276530487UTC</td></tr><tr><td>46.4.121.72:26657</td><td>quicksilver-2</td><td>nkbblocks 🟢</td><td>6604019</td><td>6056301</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:49:18.959592626UTC</td></tr><tr><td>65.108.195.29:31127</td><td>quicksilver-2</td><td>Staketab-snap 🟢</td><td>6604017</td><td>6075001</td><td>False</td><td>off</td><td>0</td><td>2024-03-28T21:49:05.198991501UTC</td></tr><tr><td>158.69.27.233:26657</td><td>quicksilver-2</td><td>KYN-SIDE 🟢</td><td>6575633</td><td>6159001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:49:23.653239294UTC</td></tr><tr><td>57.128.175.133:26657</td><td>quicksilver-2</td><td>joe 🟢</td><td>6604010</td><td>6246344</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:22.796495594UTC</td></tr><tr><td>144.76.29.90:61157</td><td>quicksilver-2</td><td>UTSA_guide 🟢</td><td>6604009</td><td>6316825</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:20.453519970UTC</td></tr><tr><td>135.181.133.16:26657</td><td>quicksilver-2</td><td>DStake 🔴</td><td>6604009</td><td>6378597</td><td>False</td><td>on</td><td>79272</td><td>2024-03-28T21:48:19.976363208UTC</td></tr><tr><td>95.214.53.76:11157</td><td>quicksilver-2</td><td>Equinox 🔴</td><td>6604018</td><td>6459097</td><td>False</td><td>on</td><td>214742</td><td>2024-03-28T21:49:11.663347756UTC</td></tr><tr><td>116.202.217.20:26657</td><td>quicksilver-2</td><td>dteam 🟢</td><td>6604022</td><td>6474101</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:49:36.676238739UTC</td></tr><tr><td>135.181.229.110:31657</td><td>quicksilver-2</td><td>rpc 🟢</td><td>6604012</td><td>6479823</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:35.984523430UTC</td></tr><tr><td>51.68.170.145:26657</td><td>quicksilver-2</td><td>openbitlab 🟢</td><td>6604016</td><td>6507144</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:58.732397012UTC</td></tr><tr><td>161.97.82.203:26257</td><td>quicksilver-2</td><td>Fort 🟢</td><td>6604009</td><td>6565996</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:48:19.539644854UTC</td></tr><tr><td>135.181.210.171:21027</td><td>quicksilver-2</td><td>STAVR-Service 🟢</td><td>6604020</td><td>6602001</td><td>False</td><td>on</td><td>0</td><td>2024-03-28T21:49:23.946485879UTC</td></tr></table>
