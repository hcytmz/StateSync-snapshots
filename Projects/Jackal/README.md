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
🔥GENESIS Mainnet🔥:    `wget https://jackal-m.genesis.stavr.tech/genesis.json` \
🔥peer Mainnet🔥:					 `ddb821309deba8f274b18ef3ae8731f239569b5c@jkl.peer.stavr.tech:11126` \
🔥peer Testnet🔥:					 `80613772b20df144945801b42f327d0945a24374@jkltest.peer.stavr.tech:19126` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.canine/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O jkl https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/jkl && chmod +x jkl && ./jkl``` \
🔥Auto_install script Testnet🔥: ```wget -O jkltest https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Jakal/Jackal-Testnet/jkltest && chmod +x jkltest && ./jkltest```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Jackal/Decentralization)🔥
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

[raw json Mainnet](https://rpc-check.jaclalm.stavr.tech/jaclalm/rpc-jaclalm-result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/Jackal/Rpc-Check-Testnet)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>208.77.197.83:28657</td><td>jackal-1</td><td>vidulum.app 🟢</td><td>6996519</td><td>0</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:54.853746740UTC</td></tr><tr><td>167.142.158.242:36657</td><td>jackal-1</td><td>jackal-archive 🟢</td><td>6996517</td><td>2770293</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:57.610307037UTC</td></tr><tr><td>142.132.202.92:26757</td><td>jackal-1</td><td>TrustedPoint 🔴</td><td>6996510</td><td>6129401</td><td>False</td><td>on</td><td>298059</td><td>2024-03-24T04:12:07.857171180UTC</td></tr><tr><td>65.108.232.181:28657</td><td>jackal-1</td><td>Vagif 🔴</td><td>6835000</td><td>6462201</td><td>False</td><td>off</td><td>60003</td><td>2024-03-24T04:12:42.824025127UTC</td></tr><tr><td>94.130.13.187:24657</td><td>jackal-1</td><td>Huginn 🟢</td><td>6996520</td><td>6707772</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:13:01.929724344UTC</td></tr><tr><td>65.108.141.109:18657</td><td>jackal-1</td><td>node 🟢</td><td>6996508</td><td>6773189</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:11:55.280819108UTC</td></tr><tr><td>65.109.116.57:13757</td><td>jackal-1</td><td>nkbblocks 🟢</td><td>6996521</td><td>6785001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:13:06.300508447UTC</td></tr><tr><td>65.109.61.114:37657</td><td>jackal-1</td><td>nkbblocks 🟢</td><td>6996512</td><td>6785101</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:19.564538562UTC</td></tr><tr><td>162.247.131.18:26657</td><td>jackal-1</td><td>ubuntu22-template 🟢</td><td>6996512</td><td>6836503</td><td>False</td><td>off</td><td>0</td><td>2024-03-24T04:12:19.173221329UTC</td></tr><tr><td>154.12.227.132:26657</td><td>jackal-1</td><td>D-stake 🔴</td><td>6996508</td><td>6836601</td><td>False</td><td>off</td><td>130248</td><td>2024-03-24T04:11:52.966301138UTC</td></tr><tr><td>65.109.118.148:26657</td><td>jackal-1</td><td>BccNodes-Relayer 🟢</td><td>6996515</td><td>6882401</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:36.109836020UTC</td></tr><tr><td>65.108.44.149:23657</td><td>jackal-1</td><td>AM-Solutions 🟢</td><td>6996517</td><td>6891001</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:47.596655791UTC</td></tr><tr><td>65.108.75.107:18657</td><td>jackal-1</td><td>node 🟢</td><td>6996513</td><td>6891691</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:21.938351898UTC</td></tr><tr><td>95.165.89.222:24474</td><td>jackal-1</td><td>maxfoton 🔴</td><td>6996517</td><td>6896517</td><td>False</td><td>off</td><td>117959</td><td>2024-03-24T04:12:43.229760555UTC</td></tr><tr><td>144.76.29.90:60857</td><td>jackal-1</td><td>UTSA_guide 🟢</td><td>6996515</td><td>6902855</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:38.358120539UTC</td></tr><tr><td>65.108.121.227:12857</td><td>jackal-1</td><td>StakeUp-rpc 🟢</td><td>6996510</td><td>6905701</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:08.239252668UTC</td></tr><tr><td>99.209.150.74:26457</td><td>jackal-1</td><td>praetor-jackal-mainnet-node 🟢</td><td>6996515</td><td>6959365</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:33.773934751UTC</td></tr><tr><td>65.108.230.113:11127</td><td>jackal-1</td><td>STAVR-Service 🟢</td><td>6996514</td><td>6993801</td><td>False</td><td>on</td><td>0</td><td>2024-03-24T04:12:49.945955114UTC</td></tr></table>
