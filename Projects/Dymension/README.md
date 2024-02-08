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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>137.184.231.239:26657</td><td>dymension_1100-1</td><td>Vkwlsidw12 🟢</td><td>28681</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:22.190378632UTC</td></tr><tr><td>5.161.222.250:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28681</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:24.908804786UTC</td></tr><tr><td>37.27.56.238:5701</td><td>dymension_1100-1</td><td>monitor 🟢</td><td>28681</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:25.807053942UTC</td></tr><tr><td>135.181.133.249:11657</td><td>dymension_1100-1</td><td>StakeUp_rpc 🟢</td><td>28681</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:26.170649047UTC</td></tr><tr><td>65.108.45.34:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28681</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:26.524823727UTC</td></tr><tr><td>158.69.27.233:19657</td><td>dymension_1100-1</td><td>KYN-PUBLIC 🟢</td><td>28682</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:27.195624285UTC</td></tr><tr><td>138.201.187.36:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28682</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:31.628342100UTC</td></tr><tr><td>74.208.16.201:26647</td><td>dymension_1100-1</td><td>SentinelCumulo 🟢</td><td>28683</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:34.536392095UTC</td></tr><tr><td>138.201.63.42:26647</td><td>dymension_1100-1</td><td>sentry 🟢</td><td>28684</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:36.887602151UTC</td></tr><tr><td>142.132.209.135:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28684</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:41.268215829UTC</td></tr><tr><td>65.109.64.99:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28687</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:53.918729935UTC</td></tr><tr><td>108.171.217.26:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28687</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:54.804920095UTC</td></tr><tr><td>65.109.118.169:60557</td><td>dymension_1100-1</td><td>jayjayservice 🟢</td><td>28687</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:55.197748514UTC</td></tr><tr><td>65.108.234.173:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28687</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:57.669500744UTC</td></tr><tr><td>5.78.111.42:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28687</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:58.585146084UTC</td></tr><tr><td>65.108.75.107:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>28688</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:03.066092944UTC</td></tr><tr><td>159.146.54.127:16657</td><td>dymension_1100-1</td><td>MAHOF 🟢</td><td>28688</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:03.597755573UTC</td></tr><tr><td>52.52.188.228:26657</td><td>dymension_1100-1</td><td>starchild-dymentia 🟢</td><td>28688</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:04.533265337UTC</td></tr><tr><td>65.108.97.58:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28688</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:04.886507977UTC</td></tr><tr><td>142.132.136.106:36657</td><td>dymension_1100-1</td><td>TAKESHI 🟢</td><td>28688</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:05.132634572UTC</td></tr><tr><td>94.74.114.58:26657</td><td>dymension_1100-1</td><td>sixnetwork-dymension-sentry-node-001 🟢</td><td>28688</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:06.304839283UTC</td></tr><tr><td>212.47.253.23:26657</td><td>dymension_1100-1</td><td>Meria 🔴</td><td>28689</td><td>1</td><td>False</td><td>off</td><td>551277</td><td>2024-02-08T13:01:08.735131507UTC</td></tr><tr><td>107.182.163.2:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28689</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:09.641338506UTC</td></tr><tr><td>65.109.157.104:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28690</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:14.299778876UTC</td></tr><tr><td>84.247.139.25:14657</td><td>dymension_1100-1</td><td>CoreNode 🟢</td><td>28692</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:21.117142974UTC</td></tr><tr><td>217.66.20.45:26657</td><td>dymension_1100-1</td><td>zuka 🟢</td><td>28692</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:26.080110792UTC</td></tr><tr><td>65.109.145.132:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28693</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:28.523417233UTC</td></tr><tr><td>65.108.103.37:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28693</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:29.005711456UTC</td></tr><tr><td>65.108.79.218:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28693</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:31.428938981UTC</td></tr><tr><td>94.130.32.41:40157</td><td>dymension_1100-1</td><td>node 🟢</td><td>28694</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:33.737951687UTC</td></tr><tr><td>142.132.202.92:27757</td><td>dymension_1100-1</td><td>TrustedPoint 🟢</td><td>28694</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T13:01:38.171945877UTC</td></tr><tr><td>85.10.200.232:23837</td><td>dymension_1100-1</td><td>dym_rpc 🟢</td><td>28695</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:42.578074928UTC</td></tr><tr><td>142.132.250.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28695</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:42.828728955UTC</td></tr><tr><td>49.12.100.223:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28695</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:45.484856809UTC</td></tr><tr><td>46.4.36.190:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28696</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:47.839699574UTC</td></tr><tr><td>65.109.101.246:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28697</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:52.306065302UTC</td></tr><tr><td>65.108.74.54:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28698</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:02.980239653UTC</td></tr><tr><td>65.21.146.120:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28699</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:09.486416179UTC</td></tr><tr><td>37.60.252.41:26657</td><td>dymension_1100-1</td><td>potatoe 🟢</td><td>28701</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:16.032503211UTC</td></tr><tr><td>108.171.217.154:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28701</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:16.916511988UTC</td></tr><tr><td>65.108.228.164:21891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28702</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:21.360842899UTC</td></tr><tr><td>5.161.72.186:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28702</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:24.124157246UTC</td></tr><tr><td>34.90.178.157:26657</td><td>dymension_1100-1</td><td>twinstake 🟢</td><td>28703</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:26.465574538UTC</td></tr><tr><td>5.78.84.11:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28703</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:27.450300660UTC</td></tr><tr><td>80.39.181.74:36657</td><td>dymension_1100-1</td><td>Validavia 🟢</td><td>28703</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-02-08T13:02:27.902090214UTC</td></tr><tr><td>95.217.57.217:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28703</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:30.314122653UTC</td></tr><tr><td>65.109.23.55:17087</td><td>dymension_1100-1</td><td>STAVR-Service 🟢</td><td>28706</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:02:45.116678338UTC</td></tr><tr><td>89.117.56.126:24757</td><td>dymension_1100-1</td><td>d 🟢</td><td>28711</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:14.159180795UTC</td></tr><tr><td>65.21.89.44:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28712</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:18.651444418UTC</td></tr><tr><td>149.50.101.13:26657</td><td>dymension_1100-1</td><td>node 🟢</td><td>28712</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:21.059691074UTC</td></tr><tr><td>65.108.142.109:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28713</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:25.550529078UTC</td></tr><tr><td>65.109.157.178:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28713</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:27.954942963UTC</td></tr><tr><td>65.108.132.163:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28713</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:28.386834310UTC</td></tr><tr><td>144.76.29.90:61057</td><td>dymension_1100-1</td><td>UTSA_guide 🟢</td><td>28715</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:34.856098329UTC</td></tr><tr><td>49.13.78.30:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28715</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:37.262997880UTC</td></tr><tr><td>65.108.141.109:40657</td><td>dymension_1100-1</td><td>node 🟢</td><td>28716</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:41.730335136UTC</td></tr><tr><td>65.108.127.107:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28716</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:42.135760261UTC</td></tr><tr><td>5.161.93.207:31891</td><td>dymension_1100-1</td><td>node 🟢</td><td>28716</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:03:42.775808649UTC</td></tr><tr><td>65.109.27.253:26612</td><td>dymension_1100-1</td><td>dymd 🟢</td><td>28681</td><td>329</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:00:25.350071677UTC</td></tr><tr><td>37.27.61.49:42657</td><td>dymension_1100-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>28692</td><td>16001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:21.511290478UTC</td></tr><tr><td>78.47.67.0:26657</td><td>dymension_1100-1</td><td>bfxd 🟢</td><td>26001</td><td>26001</td><td>False</td><td>on</td><td>0</td><td>2024-02-08T13:01:43.151269385UTC</td></tr></table>
