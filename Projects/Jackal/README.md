<h1 align="center"> 🔥JACKAL🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Jakal)
=

<h1 align="center"> MAINNET</h1>

# StateSync Jackal Mainnet
```python
SNAP_RPC=https://jkl.rpc.m.stavr.tech:443
peers="ddb821309deba8f274b18ef3ae8731f239569b5c@jkl.rpc.m.stavr.tech:11126"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.canine/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 500)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
canined tendermint unsafe-reset-all --home /root/.canine --keep-addr-book
systemctl restart canined && journalctl -u canined -f -o cat
```
# SnapShot (~1.2GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop canined
cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup
rm -rf $HOME/.canine/data
curl -o - -L http://jkl.snapshot.stavr.tech:1018/jackal/jackal-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.canine --strip-components 2
mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json
wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"
sudo systemctl restart canined && journalctl -u canined -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Jakal/Jackal-Testnet)
=

# StateSync Jackal Testnet
```python
SNAP_RPC=https://jkl.rpc.t.stavr.tech:443
peers="80613772b20df144945801b42f327d0945a24374@jkltest.peer.stavr.tech:19126"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.canine/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.canine/config/config.toml
canined tendermint unsafe-reset-all --home /root/.canine --keep-addr-book
systemctl restart canined && journalctl -u canined -f -o cat
```
# SnapShot (~0.5 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop canined
cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup
rm -rf $HOME/.canine/data
curl -o - -L http://jkltest.snapshot.stavr.tech:1015/jackalt/jackalt-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.canine --strip-components 2
mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json
wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"
sudo systemctl restart canined && journalctl -u canined -f -o cat
```

 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Jackal/staking		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Jackal-Testnet/staking     `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://jkl.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://jkl.api.t.stavr.tech \
🔥RPC Mainnet🔥:           https://jkl.rpc.m.stavr.tech:443              `Snapshot-interval = 300` \
🔥RPC Testnet🔥:           https://jkl.rpc.t.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:          http://jkl.grpc.m.stavr.tech:5013 \
🔥gRPC Testnet🔥:          http://jkl.grpc.t.stavr.tech:5913 \
🔥peer Mainnet🔥:					 `ddb821309deba8f274b18ef3ae8731f239569b5c@jkl.peer.stavr.tech:11126` \
🔥peer Testnet🔥:					 `80613772b20df144945801b42f327d0945a24374@jkltest.peer.stavr.tech:19126` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O jkl https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/jkl && chmod +x jkl && ./jkl``` \
🔥Auto_install script Testnet🔥: ```wget -O jkltest https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/jkltest && chmod +x jkltest && ./jkltest``` \
🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Jackal/Decentralization)🔥


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

[raw json Mainnet](https://rpc-check.jaclalm.stavr.tech/jaclalm/rpc-jaclalm-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Jackal/Rpc-Check-Testnet)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>167.142.158.242:36657</td><td>jackal-1</td><td>jackal-archive 🟢</td><td>6610946</td><td>2770293</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:31:08.115608060UTC</td></tr><tr><td>142.132.202.92:26757</td><td>jackal-1</td><td>TrustedPoint 🔴</td><td>6610922</td><td>6129401</td><td>False</td><td>on</td><td>290891</td><td>2024-02-24T01:28:47.240642423UTC</td></tr><tr><td>144.76.29.90:60857</td><td>jackal-1</td><td>UTSA_guide 🟢</td><td>6610936</td><td>6280001</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:30:06.829140028UTC</td></tr><tr><td>208.77.197.83:28657</td><td>jackal-1</td><td>vidulum.app 🟢</td><td>6610945</td><td>6296001</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:31:05.243829084UTC</td></tr><tr><td>94.130.13.187:24657</td><td>jackal-1</td><td>Huginn 🟢</td><td>6588265</td><td>6424001</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:31:23.393828855UTC</td></tr><tr><td>65.108.141.109:18657</td><td>jackal-1</td><td>node 🟢</td><td>6610918</td><td>6444728</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:28:25.570817772UTC</td></tr><tr><td>65.108.232.181:28657</td><td>jackal-1</td><td>Vagif 🔴</td><td>6610937</td><td>6462201</td><td>False</td><td>off</td><td>60003</td><td>2024-02-24T01:30:15.890374101UTC</td></tr><tr><td>65.109.116.57:13757</td><td>jackal-1</td><td>nkbblocks 🟢</td><td>6610950</td><td>6468668</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:31:34.089995304UTC</td></tr><tr><td>65.21.139.150:37657</td><td>jackal-1</td><td>nkbblocks 🟢</td><td>6610920</td><td>6473101</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:28:36.216558738UTC</td></tr><tr><td>65.109.61.114:37657</td><td>jackal-1</td><td>nkbblocks 🟢</td><td>6610928</td><td>6473101</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:29:22.666503237UTC</td></tr><tr><td>65.109.118.148:26657</td><td>jackal-1</td><td>BccNodes-Relayer 🟢</td><td>6610934</td><td>6489001</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:29:58.353658638UTC</td></tr><tr><td>65.108.66.174:27657</td><td>jackal-1</td><td>hello-BccNodesRPC 🟢</td><td>6610936</td><td>6489001</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:30:07.184031162UTC</td></tr><tr><td>65.108.41.177:26657</td><td>jackal-1</td><td>skynodejs 🔴</td><td>6610946</td><td>6509001</td><td>False</td><td>on</td><td>83702</td><td>2024-02-24T01:31:08.503888742UTC</td></tr><tr><td>65.21.90.141:12131</td><td>jackal-1</td><td>SerGo 🔴</td><td>6610921</td><td>6510921</td><td>False</td><td>off</td><td>51100</td><td>2024-02-24T01:28:40.681864362UTC</td></tr><tr><td>95.165.89.222:24474</td><td>jackal-1</td><td>maxfoton 🔴</td><td>6610937</td><td>6510937</td><td>False</td><td>off</td><td>117661</td><td>2024-02-24T01:30:16.317222370UTC</td></tr><tr><td>65.108.75.107:18657</td><td>jackal-1</td><td>node 🟢</td><td>6610930</td><td>6564077</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:29:33.345403500UTC</td></tr><tr><td>65.108.44.149:23657</td><td>jackal-1</td><td>ams 🟢</td><td>6610940</td><td>6571141</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:30:31.123314305UTC</td></tr><tr><td>154.12.227.132:26657</td><td>jackal-1</td><td>D-stake 🔴</td><td>6610918</td><td>6591001</td><td>False</td><td>off</td><td>130243</td><td>2024-02-24T01:28:20.981318557UTC</td></tr><tr><td>37.27.61.49:43657</td><td>jackal-1</td><td>[NODERS]TEAM_SERVICE 🟢</td><td>6610915</td><td>6591201</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:28:03.800491691UTC</td></tr><tr><td>65.108.230.113:11127</td><td>jackal-1</td><td>STAVR-Service 🟢</td><td>6610940</td><td>6609101</td><td>False</td><td>on</td><td>0</td><td>2024-02-24T01:30:35.574432524UTC</td></tr></table>
