<h1 align="center"> 🔥BAND PROTOCOL🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/BandProtocol)
=

<h1 align="center"> MAINNET</h1>

# StateSync Band Mainnet
```python
RPC=http://band.rpc.m.stavr.tech:11067
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
sudo systemctl restart bandd && journalctl -u bandd -f -o cat
```
# SnapShot (~15 GB) updated every 10 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop bandd
cp $HOME/.band/data/priv_validator_state.json $HOME/.band/priv_validator_state.json.backup
rm -rf $HOME/.band/data
curl -o - -L http://band.snapshot.stavr.tech:1022/band/band-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.band --strip-components 2
mv $HOME/.band/priv_validator_state.json.backup $HOME/.band/data/priv_validator_state.json
wget -O $HOME/.band/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/addrbook.json"
sudo systemctl restart bandd && journalctl -u bandd -f -o cat
```

<h1 align="center"> TESTNET</h1>

[Node installation instructions]()
=

# StateSync Band Testnet (Temporarily stopped)
```python
SOON
```

# SnapShot (~5GB) updated every 5 hours
```python
SOON
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:      https://explorer.stavr.tech/Band-Mainnet		        `Indexer "ON"` \
🔥EXPLORER Testnet🔥:      SOON       `Indexer "ON"` \
🔥API Mainnet🔥: 			 		 https://band.api.m.stavr.tech \
🔥API Testnet🔥: 			 		 SOON \
🔥RPC Mainnet🔥:           http://band.rpc.m.stavr.tech:11067              `Snapshot-interval = 1000` \
🔥RPC Testnet🔥:           SOON              `Snapshot-interval = 1000` \
🔥gRPC Mainnet🔥:          http://band.grpc.m.stavr.tech:7803 \
🔥gRPC Testnet🔥:          SOON \
🔥peer Mainnet🔥:					 `0bfd5d7355ebf38e35af619ae0cab70aa21675a5@band-m.peer.stavr.tech:11026` \
🔥peer Testnet🔥:					 SOON \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.band/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/addrbook.json"``` \
🔥Addrbook Testnet🔥:    SOON \
🔥Auto_install script Mainnet🔥: ```wget -O bandm https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/BandProtocol/bandm && chmod +x bandm && ./bandm``` \
🔥Auto_install script Testnet🔥: SOON
