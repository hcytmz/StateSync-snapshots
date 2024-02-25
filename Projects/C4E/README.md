<h1 align="center"> 🔥C4E🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/C4E)
=

<h1 align="center"> MAINNET</h1>

# StateSync C4E Mainnet
```python
SNAP_RPC=https://c4e.rpc.m.stavr.tech:443
peers="5ed0b8f7989d34438f71ccc74b0ab0fbf763a475@c4e.peer.stavr.tech:17096"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.c4e-chain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.c4e-chain/config/config.toml
c4ed tendermint unsafe-reset-all --home /root/.c4e-chain --keep-addr-book
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop c4ed
cp $HOME/.c4e-chain/data/priv_validator_state.json $HOME/.c4e-chain/priv_validator_state.json.backup
rm -rf $HOME/.c4e-chain/data
curl -o - -L http://c4e.snapshot.stavr.tech:1018/c4e/c4e-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.c4e-chain --strip-components 2
mv $HOME/.c4e-chain/priv_validator_state.json.backup $HOME/.c4e-chain/data/priv_validator_state.json
wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/addrbook.json"
sudo systemctl restart c4ed && journalctl -u c4ed -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER MAINNET🔥:  https://explorer.stavr.tech/C4E/staking            `Indexer "ON"` \
🔥EXPLORER TESTET🔥:   https://explorer.stavr.tech/C4E-Testnet/staking     `Indexer "ON"` \
🔥API MAINNET🔥:       https://c4e.api.m.stavr.tech \
🔥API TESTNET🔥:       https://c4e.api.t.stavr.tech \
🔥RPC🔥:               https://c4e.rpc.m.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:              http://c4e.grpc.m.stavr.tech:7029 \
🔥peer🔥:              `5ed0b8f7989d34438f71ccc74b0ab0fbf763a475@c4e.peer.stavr.tech:17096` \
🔥Addrbook-M🔥:    ```wget https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/genesis.json -O $HOME/.c4e-chain/config/genesis.json``` \
🔥Addrbook-T🔥:    ```wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/C4E_Testnet/addrbook.json"``` \
🔥Auto_install script-M🔥: ```wget -O c4 https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/c4 && chmod +x c4 && ./c4``` \
🔥Auto_install script-T🔥: ```wget -O c4et https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/C4E/C4E_Testnet/c4et && chmod +x c4et && ./c4et``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/C4E/Decentralization)🔥




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

[raw json](https://rpc-check.c4e.stavr.tech/c4e/rpc-c4e-result.json)
=



<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>79.137.68.96:26657</td><td>perun-1</td><td>archive-node2 🟢</td><td>7326489</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:09.365840022UTC</td></tr><tr><td>65.108.70.119:33657</td><td>perun-1</td><td>AlxVoy 🟢</td><td>7326491</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:20.932665221UTC</td></tr><tr><td>149.202.66.111:26657</td><td>perun-1</td><td>archive-node1 🟢</td><td>7326494</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:37.638820362UTC</td></tr><tr><td>185.245.182.192:46657</td><td>perun-1</td><td>Meerlabs 🔴</td><td>7326495</td><td>1051501</td><td>False</td><td>on</td><td>344603</td><td>2024-02-25T09:03:44.901219260UTC</td></tr><tr><td>185.215.167.18:26657</td><td>perun-1</td><td>Rawalot 🔴</td><td>7326496</td><td>1090501</td><td>False</td><td>on</td><td>450091</td><td>2024-02-25T09:03:56.176298739UTC</td></tr><tr><td>209.182.239.169:46657</td><td>perun-1</td><td>SECARD 🔴</td><td>7326493</td><td>2616101</td><td>False</td><td>off</td><td>749308</td><td>2024-02-25T09:03:32.898043174UTC</td></tr><tr><td>89.117.58.109:26657</td><td>perun-1</td><td>medes 🔴</td><td>7326496</td><td>2826001</td><td>False</td><td>off</td><td>891015</td><td>2024-02-25T09:03:51.697673035UTC</td></tr><tr><td>65.108.141.109:39657</td><td>perun-1</td><td>node 🟢</td><td>7326490</td><td>5303301</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:11.806935687UTC</td></tr><tr><td>185.252.235.83:26657</td><td>perun-1</td><td>Alien 🔴</td><td>7326494</td><td>6502501</td><td>False</td><td>on</td><td>648211</td><td>2024-02-25T09:03:37.967361284UTC</td></tr><tr><td>116.202.217.20:56657</td><td>perun-1</td><td>dteam 🟢</td><td>7326489</td><td>6800901</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:08.684906054UTC</td></tr><tr><td>38.242.220.64:16657</td><td>perun-1</td><td>MAHOF 🟢</td><td>7326494</td><td>6885501</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:35.257653281UTC</td></tr><tr><td>142.132.136.106:25657</td><td>perun-1</td><td>services 🟢</td><td>7326492</td><td>7012001</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:23.622867291UTC</td></tr><tr><td>65.108.66.174:30657</td><td>perun-1</td><td>hello-BccNodesRPC 🟢</td><td>7089725</td><td>7089601</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:21.248690020UTC</td></tr><tr><td>168.119.226.107:26957</td><td>perun-1</td><td>c4e_rpc 🟢</td><td>7326490</td><td>7226490</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:16.189143362UTC</td></tr><tr><td>65.108.124.219:31657</td><td>perun-1</td><td>MantiCore 🔴</td><td>7326491</td><td>7226491</td><td>False</td><td>off</td><td>729602</td><td>2024-02-25T09:03:20.600211836UTC</td></tr><tr><td>65.109.30.185:26657</td><td>perun-1</td><td>c4e-sentry2-mainnet 🟢</td><td>7326495</td><td>7284001</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:44.563373703UTC</td></tr><tr><td>163.172.18.144:26657</td><td>perun-1</td><td>c4e-sentry3-mainnet 🟢</td><td>7326495</td><td>7297001</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:45.220638052UTC</td></tr><tr><td>65.108.75.107:39657</td><td>perun-1</td><td>node 🟢</td><td>7326492</td><td>7300001</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:23.995697219UTC</td></tr><tr><td>5.135.141.191:26657</td><td>perun-1</td><td>c4e-sentry1-mainnet 🟢</td><td>7326489</td><td>7300501</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:07.996750219UTC</td></tr><tr><td>65.108.121.227:16657</td><td>perun-1</td><td>landeros-rpc 🟢</td><td>7326489</td><td>7321501</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:08.379840191UTC</td></tr><tr><td>135.181.210.171:17097</td><td>perun-1</td><td>STAVR-Service 🟢</td><td>7326492</td><td>7323901</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:24.384455108UTC</td></tr><tr><td>95.216.102.121:26657</td><td>perun-1</td><td>dteam 🟢</td><td>7326489</td><td>7324001</td><td>False</td><td>on</td><td>0</td><td>2024-02-25T09:03:09.047788805UTC</td></tr></table>
