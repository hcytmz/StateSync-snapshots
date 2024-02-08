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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>31288</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:16.271390813UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31289</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:18.996299726UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>31289</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:19.740441273UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>31289</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:20.098378957UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31289</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:20.443452286UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>31289</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:21.091381262UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31290</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:25.519559322UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>31290</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:28.467960239UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>31292</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:30.779817053UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31292</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:35.226738356UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31294</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:47.894483505UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31294</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:48.894504942UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>31295</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:49.260168468UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31295</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:51.724635320UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31295</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:52.638125674UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>31296</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:57.143601705UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>31296</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:57.628798666UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>31296</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:58.611046471UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31296</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:59.031223903UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>31296</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:59.346747138UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>31296</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:00.457107218UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>31297</td><td>1</td><td>False</td><td>off</td><td>565069</td><td>2024-02-08T17:10:02.884994237UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31297</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:03.767513882UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31298</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:10.575119393UTC</td></tr><tr><td>65.21.229.60:37657</td><td>dymension_1100-1</td><td>r-index-bh 🟢</td><td>31298</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:13.031437992UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>31301</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:22.133826804UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31301</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:24.586770467UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31301</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:25.054581043UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31301</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:27.488268793UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>31302</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:29.798387517UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>31303</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T17:10:34.330943191UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31303</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:38.725246671UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31304</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:41.317131914UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31304</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:43.671718674UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31305</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:48.107221800UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31306</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:58.744086449UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31307</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:03.307122959UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>31308</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:09.766851683UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31308</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:10.679259161UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31310</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:15.139511448UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31310</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:18.157060880UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>31311</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:20.600469505UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31311</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:21.543032411UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>31311</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T17:11:22.017847830UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31311</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:24.449091785UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>31314</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:39.228278689UTC</td></tr><tr><td>65.108.132.254:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31315</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:45.816821858UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>31319</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:08.714906349UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31320</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:13.254154529UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>31320</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:15.701204015UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31321</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:20.227016556UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31321</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:22.664359736UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31322</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:23.084794082UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>31323</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:29.515445892UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31323</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:31.942027319UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>31324</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:36.420744882UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31324</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:36.783127629UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>31324</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:12:37.421863620UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>31289</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:09:19.394016070UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>31299</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:17.583189444UTC</td></tr><tr><td>209.182.238.140:26657</td><td>dymension_1100-1</td><td>SECARDRPC 🟢</td><td>31310</td><td>16013</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:11:17.534761104UTC</td></tr><tr><td>78.47.67.0:26657</td><td>dymension_1100-1</td><td>bfxd 🟢</td><td>26001</td><td>26001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T17:10:38.989019669UTC</td></tr></table>
