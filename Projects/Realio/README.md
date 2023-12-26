<h1 align="center"> 🔥Realio🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Realio)
=

<h1 align="center"> MAINNET</h1>

# StateSync Realio Mainnet
```python
SNAP_RPC=http://realio.rpc.m.stavr.tech:21097
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.realio-network/config/config.toml
realio-networkd tendermint unsafe-reset-all --home /root/.realio-network
wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/addrbook.json"
sudo systemctl restart realio-networkd && journalctl -u realio-networkd -f -o cat
```
# SnapShot (~0.1 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop realio-networkd
cp $HOME/.realio-network/data/priv_validator_state.json $HOME/.realio-network/priv_validator_state.json.backup
rm -rf $HOME/.realio-network/data
curl -o - -L http://realio.snapshot.stavr.tech:1029/realio/realio-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.realio-network --strip-components 2
mv $HOME/.realio-network/priv_validator_state.json.backup $HOME/.realio-network/data/priv_validator_state.json
wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/addrbook.json"
sudo systemctl restart realio-networkd && journalctl -u realio-networkd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:       https://explorer.stavr.tech/Realio-Mainnet  `Indexer "ON"` \
🔥EXPLORER Testnet🔥:         https://explorer.stavr.tech/Realio             `Indexer "ON"` \
🔥API Mainnet🔥:                    https://realio.api.m.stavr.tech \
🔥API Testnet🔥:                      https://realio.api.t.stavr.tech \
🔥RPC Mainnet🔥:                   http://realio.rpc.m.stavr.tech:21097              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:                 http://realio.grpc.m.stavr.tech:9062 \
🔥peer Mainnet🔥:                   `0f1a87ee4400c0b6332343775a4ff659bc3daf29@realio.peers.stavr.tech:21096` \
🔥Genesis Mainnet🔥:     ```wget -O $HOME/.realio-network/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/genesis.json"``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.realio-network/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet(StateSync/SnapShot included)🔥: ```wget -O realio https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Realio/realio && chmod +x realio && ./realio``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Realio/Decentralization)🔥

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

[raw json Mainnet](https://rpc-check.realiom.stavr.tech/realiom/rpc-realiom-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>135.181.114.86:25557</td><td>realionetwork_3301-1</td><td>NodeName 🔴</td><td>4395377</td><td>3529801</td><td>False</td><td>on</td><td>350110</td><td>2023-12-26T17:46:48.857664582UTC</td></tr><tr><td>65.109.28.177:30657</td><td>realionetwork_3301-1</td><td>AlxVoy 🔴</td><td>4395380</td><td>3560001</td><td>False</td><td>on</td><td>125617</td><td>2023-12-26T17:47:02.148646207UTC</td></tr><tr><td>5.9.61.78:11657</td><td>realionetwork_3301-1</td><td>Kynraze 🔴</td><td>4395377</td><td>3717201</td><td>False</td><td>on</td><td>547790</td><td>2023-12-26T17:46:48.454697377UTC</td></tr><tr><td>65.108.66.174:45657</td><td>realionetwork_3301-1</td><td>hello-BccNodesRPC 🟢</td><td>4395379</td><td>3883201</td><td>False</td><td>off</td><td>0</td><td>2023-12-26T17:46:56.864745739UTC</td></tr><tr><td>95.168.173.33:33657</td><td>realionetwork_3301-1</td><td>RIO-mainnet-prod 🔴</td><td>4395378</td><td>3944101</td><td>False</td><td>on</td><td>44526</td><td>2023-12-26T17:46:51.906662288UTC</td></tr><tr><td>158.69.27.233:25657</td><td>realionetwork_3301-1</td><td>KYN-ENDPOINT 🟢</td><td>4395379</td><td>4224001</td><td>False</td><td>on</td><td>0</td><td>2023-12-26T17:46:59.525726530UTC</td></tr><tr><td>65.109.29.224:28657</td><td>realionetwork_3301-1</td><td>Munris 🟢</td><td>4395378</td><td>4295378</td><td>False</td><td>off</td><td>0</td><td>2023-12-26T17:46:51.237361298UTC</td></tr><tr><td>65.21.90.141:12261</td><td>realionetwork_3301-1</td><td>SerGo 🔴</td><td>4395378</td><td>4295378</td><td>False</td><td>off</td><td>38886</td><td>2023-12-26T17:46:51.618990295UTC</td></tr><tr><td>142.132.202.50:39657</td><td>realionetwork_3301-1</td><td>rpc 🔴</td><td>4395378</td><td>4295378</td><td>False</td><td>off</td><td>1731447</td><td>2023-12-26T17:46:54.372920702UTC</td></tr><tr><td>173.249.59.70:32657</td><td>realionetwork_3301-1</td><td>moodman 🔴</td><td>4395379</td><td>4295379</td><td>False</td><td>off</td><td>107488</td><td>2023-12-26T17:46:59.779349435UTC</td></tr><tr><td>46.17.250.108:56657</td><td>realionetwork_3301-1</td><td>Sr20de 🔴</td><td>4395378</td><td>4311801</td><td>False</td><td>on</td><td>108133</td><td>2023-12-26T17:46:53.817720686UTC</td></tr><tr><td>135.181.210.171:21097</td><td>realionetwork_3301-1</td><td>STAVR-Service 🟢</td><td>4395378</td><td>4393001</td><td>False</td><td>on</td><td>0</td><td>2023-12-26T17:46:54.145047796UTC</td></tr></table>
