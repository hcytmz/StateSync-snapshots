<h1 align="center"> 🔥BAND PROTOCOL🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/BandProtocol)
=

<h1 align="center"> MAINNET</h1>

# StateSync Band Mainnet
```python
RPC=https://band.rpc.m.stavr.tech:443
peers=0bfd5d7355ebf38e35af619ae0cab70aa21675a5@band-m.peer.stavr.tech:11026
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.band/config/config.toml
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 1500)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.band/config/config.toml
sudo systemctl stop bandd && bandd tendermint unsafe-reset-all --keep-addr-book
curl -o - -L http://band.files.stavr.tech:1103/files-band.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
sudo systemctl restart bandd && journalctl -u bandd -f -o cat
```
# SnapShot updated every 14 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop bandd
cp $HOME/.band/data/priv_validator_state.json $HOME/.band/priv_validator_state.json.backup
rm -rf $HOME/.band/data
curl -o - -L http://band.snapshot.stavr.tech:1022/band/band-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
curl -o - -L http://band.files.stavr.tech:1103/files-band.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
mv $HOME/.band/priv_validator_state.json.backup $HOME/.band/data/priv_validator_state.json
wget -O $HOME/.band/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/addrbook.json"
sudo systemctl restart bandd && journalctl -u bandd -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/BandProtocol/Testnet)
=

# StateSync Band Testnet
```python
RPC=https://band.rpc.t.stavr.tech:443
peers=7f03c7f4a41300348afce4b51774ab3fab8ae3c2@band-t.peer.stavr.tech:11016
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.band/config/config.toml
LATEST_HEIGHT=$(curl -s $RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$RPC,$RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.band/config/config.toml
sudo systemctl stop bandd && bandd tendermint unsafe-reset-all --keep-addr-book
curl -o - -L http://band-t.files.stavr.tech:1103/files-bandt.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
sudo systemctl restart bandd && journalctl -u bandd -f -o cat
```

# SnapShot Testnet updated every 12 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop bandd
cp $HOME/.band/data/priv_validator_state.json $HOME/.band/priv_validator_state.json.backup
rm -rf $HOME/.band/data
curl -o - -L http://band-t.snapshot.stavr.tech:1025/bandt/bandt-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
curl -o - -L http://band-t.files.stavr.tech:1103/files-bandt.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
mv $HOME/.band/priv_validator_state.json.backup $HOME/.band/data/priv_validator_state.json
wget -O $HOME/.band/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/Testnet/addrbook.json"
sudo systemctl restart bandd && journalctl -u bandd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Band-Mainnet		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      https://explorer.stavr.tech/Band-Testnet       `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://band.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 https://band.api.t.stavr.tech \
🔥RPC Mainnet🔥:           https://band.rpc.m.stavr.tech:443              `Snapshot-interval = 1500` \
🔥RPC Testnet🔥:           https://band.rpc.t.stavr.tech:443              `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:          http://band.grpc.m.stavr.tech:7803 \
🔥gRPC Testnet🔥:          http://band.grpc.t.stavr.tech:6804 \
🔥peer Mainnet🔥:					 `0bfd5d7355ebf38e35af619ae0cab70aa21675a5@band-m.peer.stavr.tech:11026` \
🔥peer Testnet🔥:					 `7f03c7f4a41300348afce4b51774ab3fab8ae3c2@band-t.peer.stavr.tech:11016` \
🔥Files Mainnet🔥: ```curl -o - -L http://band.files.stavr.tech:1103/files-band.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2``` \
🔥Files Testnet🔥: ```curl -o - -L http://band-t.files.stavr.tech:1103/files-bandt.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.band/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.band/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O bandm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/bandm && chmod +x bandm && ./bandm``` \
🔥Auto_install script Testnet🔥: ```wget -O bandt https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/Testnet/bandt && chmod +x bandt && ./bandt```

🔥[Decentralization Info](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/BandProtocol/Decentralization)🔥
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

[raw json Mainnet](https://rpc-check.bandm.stavr.tech/bandm/rpcbandm_result.json) \
[raw json Testnet](https://github.com/obajay/StateSync-snapshots/tree/main/Projects/BandProtocol/Rpc-Check-Testnet)
=

<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>213.239.192.52:26657</td><td>laozi-mainnet</td><td>node 🟢</td><td>27154480</td><td>21737961</td><td>False</td><td>on</td><td>0</td><td>2024-03-21T15:19:23.739311247UTC</td></tr><tr><td>91.246.64.247:26657</td><td>laozi-mainnet</td><td>band4 🟢</td><td>27154488</td><td>24780001</td><td>False</td><td>off</td><td>0</td><td>2024-03-21T15:19:46.556303982UTC</td></tr><tr><td>137.184.224.198:41657</td><td>laozi-mainnet</td><td>WeStaking 🟢</td><td>27154445</td><td>25541046</td><td>False</td><td>off</td><td>0</td><td>2024-03-21T15:17:53.031530080UTC</td></tr><tr><td>51.15.208.237:26657</td><td>laozi-mainnet</td><td>Meria 🔴</td><td>27154472</td><td>26599563</td><td>False</td><td>on</td><td>303349</td><td>2024-03-21T15:19:04.872978794UTC</td></tr><tr><td>167.235.9.223:61457</td><td>laozi-mainnet</td><td>F5Nodes 🔴</td><td>27154450</td><td>26790093</td><td>False</td><td>off</td><td>115</td><td>2024-03-21T15:18:05.544422968UTC</td></tr><tr><td>46.137.209.178:26657</td><td>laozi-mainnet</td><td>b-band-s0-sg 🔴</td><td>27154493</td><td>27131070</td><td>False</td><td>off</td><td>2573630</td><td>2024-03-21T15:20:00.077877044UTC</td></tr></table>
