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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>15578</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:44.021337225UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15579</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:48.808811762UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>15579</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:49.566501400UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>15579</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:49.998714396UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15580</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:50.496682335UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>15580</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:51.147072548UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15580</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:55.521772851UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>15581</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:58.396385001UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>15581</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:00.739056199UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15582</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:05.139204783UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15584</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:17.801748595UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15584</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:18.655340255UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>15584</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:19.071889010UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15584</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:21.487442335UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:22.388409061UTC</td></tr><tr><td>45.76.86.41:26657</td><td>dymension_1100-1</td><td>KudasaiJP 🔴</td><td>15585</td><td>1</td><td>False</td><td>on</td><td>1650124</td><td>2024-02-07T16:16:24.697319154UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>15585</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:27.159321298UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>15586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:30.133581519UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:30.498419358UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>15586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:30.866339216UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>15586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:31.955701453UTC</td></tr><tr><td>144.91.68.181:26657</td><td>dymension_1100-1</td><td>vmi1526870.contaboserver.net 🟢</td><td>15586</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:32.254936035UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>15587</td><td>1</td><td>False</td><td>off</td><td>442747</td><td>2024-02-07T16:16:34.650189957UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15587</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:35.565825680UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15589</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:42.357268607UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>15590</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:48.825823280UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>15590</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:53.408023146UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15591</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:55.862984562UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15591</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:56.278896182UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15591</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:58.737185849UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>15591</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:16:59.047595356UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>15592</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-07T16:17:05.553672783UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>15593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:07.955078925UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:08.225611156UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15593</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:10.569893862UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15594</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:12.922135032UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15594</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:15.341816302UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15595</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:24.016552878UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15596</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:30.548558872UTC</td></tr><tr><td>65.108.228.163:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15597</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:32.954953820UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>15598</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:37.432249932UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15598</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:38.279091157UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15598</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:42.749556552UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15599</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:45.510386303UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>15599</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:47.910144348UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15599</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:48.830668470UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>15599</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-07T16:17:49.265143440UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15600</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:17:49.607548315UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>15603</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:04.425499606UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>15607</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:33.559528662UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15608</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:38.011459330UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15609</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:44.498600469UTC</td></tr><tr><td>5.161.228.151:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15609</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:45.185349276UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15610</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:47.634440542UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15610</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:48.060584743UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>15611</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:54.570669848UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15612</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:18:56.945842136UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>15613</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:19:01.415338135UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15613</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:19:01.778160154UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>15612</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:19:02.430529113UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>15579</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-07T16:15:49.208540767UTC</td></tr></table>
