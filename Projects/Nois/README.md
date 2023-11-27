<h1 align="center"> 🔥Nois MAINNET🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Nois)
=
# StateSync MAINNET
```python
SNAP_RPC=https://nois.rpc.m.stavr.tech:443
peers="9fa9b59890187293a8f6b57d1f606fdfe751396e@nois.peer.stavr.tech:40136"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$peers\"/" $HOME/.noisd/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" $HOME/.noisd/config/config.toml
noisd tendermint unsafe-reset-all --home $HOME/.noisd
wget -O $HOME/.noisd/config/addrbook.json https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/addrbook.json
sed -i -e "s/^snapshot-interval *=.*/snapshot-interval = \"1500\"/" $HOME/.noisd/config/app.toml
curl -o - -L http://nois.wasm.stavr.tech:1004/wasm-nois.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.noisd --strip-components 2
systemctl restart noisd && journalctl -u noisd -f -o cat

```

# SnapShot MAINNET (~0.2 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop noisd
cp $HOME/.noisd/data/priv_validator_state.json $HOME/.noisd/priv_validator_state.json.backup
rm -rf $HOME/.noisd/data
curl -o - -L http://nois.snapshot.stavr.tech:1028/noisd/noisd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.noisd --strip-components 2
curl -o - -L http://nois.wasm.stavr.tech:1004/wasm-nois.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.noisd --strip-components 2
mv $HOME/.noisd/priv_validator_state.json.backup $HOME/.noisd/data/priv_validator_state.json
wget -O $HOME/.noisd/config/addrbook.json https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/addrbook.json
sudo systemctl restart noisd && journalctl -u noisd -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER Mainnet🔥:       https://explorer.stavr.tech/Nois-Mainnet         `Indexer "ON"` \
🔥EXPLORER Testnet🔥:         https://explorer.stavr.tech/Nois-Testnet                 `Indexer "ON"` \
🔥API Mainnet🔥:                    https://nois.api.m.stavr.tech \
🔥API Testnet🔥:                      https://nois3.api.t.stavr.tech \
🔥RPC Mainnet🔥:                   http://nois.rpc.m.stavr.tech          `Snapshot-interval = 100` \
🔥gRPC Mainnet🔥:                 http://nois.grpc.m.stavr.tech:191 \
🔥gRPC Testnet🔥:                   http://nois.grpc.t.stavr.tech:191 \
🔥peer Mainnet🔥:           `9fa9b59890187293a8f6b57d1f606fdfe751396e@nois.peer.stavr.tech:40136` \
🔥Genesis Mainnet🔥:     ```wget -O $HOME/.noisd/config/genesis.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/genesis.json"``` \
🔥WASM Mainnet🔥:        ```curl -o - -L http://nois.wasm.stavr.tech:1004/wasm-nois.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.noisd --strip-components 2``` \
🔥Addrbook Mainnet🔥:    ```wget -O $HOME/.noisd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/addrbook.json"``` \
🔥Addrbook Testnet🔥:    ```wget -O $HOME/.noisd/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/Noist_Testnet/addrbook.json"``` \
🔥Auto_install script Mainnet🔥: ```wget -O noism https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/noism && chmod +x noism && ./noism``` \
🔥Auto_install script Testnet🔥: ```wget -O nois https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Nois/Noist_Testnet/nois && chmod +x nois && ./nois```

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

[raw json Mainnet](https://rpc-check.noism.stavr.tech/noism/rpc-noism-result.json)
=

