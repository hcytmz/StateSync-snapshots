[🔥OUR VALIDATOR🔥](https://restake.app/dymension/dymvaloper1amxp0k0hg4edrxg85v07t9ka2tfuhamhldgf8e)
=

<h1 align="center"> 🔥Dymension🔥</h1>

<h1 align="center"> MAINNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension)
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

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Dymension/Testnet)
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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>236490</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:51:43.405267510UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>236491</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:51:46.172792203UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>236491</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:51:49.100913267UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>236492</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:51:51.387968748UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>236494</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:04.109694477UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>236494</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:06.596568498UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>236496</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:15.238046854UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>236496</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:15.725063332UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>236496</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:18.708076004UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>236497</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:21.437630533UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>236498</td><td>1</td><td>False</td><td>off</td><td>747286</td><td>2024-02-22T07:52:27.995816965UTC</td></tr><tr><td>75.119.139.53:26667</td><td>dymension_1100-1</td><td>AVIAONE_Blockchains_Service 🟢</td><td>236499</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:34.796888965UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>236502</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:48.670379689UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>236503</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-22T07:52:53.387075569UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>236503</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:55.776094685UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>236504</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:58.077632169UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>236510</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:53:33.352955017UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>236510</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:53:34.313959777UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>236511</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:53:43.242559063UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>236511</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-22T07:53:43.655732191UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>236518</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:54:25.652356354UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>236520</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:54:30.110783021UTC</td></tr><tr><td>65.109.23.55:17187</td><td>dymension_1100-1</td><td>STAVR-Archive 🟢</td><td>236522</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:54:42.938616405UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>236522</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:54:43.347565704UTC</td></tr><tr><td>65.108.74.54:2082</td><td>dymension_1100-1</td><td>node 🟢</td><td>236522</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:54:45.904200668UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>236523</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:54:52.472547207UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>236490</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:51:43.020555019UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>236499</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:35.167720430UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>236511</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:53:40.783189721UTC</td></tr><tr><td>84.46.245.250:14657</td><td>dymension_1100-1</td><td>VNBNODE 🟢</td><td>236496</td><td>39843</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:19.042613580UTC</td></tr><tr><td>212.23.222.109:26757</td><td>dymension_1100-1</td><td>jaha_rpc 🟢</td><td>236502</td><td>40001</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:52:46.295400383UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>236513</td><td>234001</td><td>False</td><td>on</td><td>0</td><td>2024-02-22T07:53:54.408623249UTC</td></tr></table>
