<h1 align="center"> 🔥CROWD CONTROL TESTNET🔥</h1>


[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Crowd_Control)
=

## StateSync
```python
cd $HOME
SNAP_RPC=https://crowd.rpc.t.stavr.tech:443
PEERS="ec585d7fb38b67619dcb79aad90722f0eaf0faa3@crowd.peer.stavr.tech:21206"
sed -i.bak -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.Cardchain/config/config.toml
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height) \
&& BLOCK_HEIGHT=$((LATEST_HEIGHT - 100)) \
&& TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash); \

echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH

sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"|" $HOME/.Cardchain/config/config.toml; \
Cardchaind tendermint unsafe-reset-all
wget -O $HOME/.Cardchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crowd_Control/addrbook.json"
sudo systemctl restart Cardchaind && journalctl -u Cardchaind -f -o cat
```
## SnapShot (~0.3 GB) updated every 5 hours
```python
cd $HOME
apt install lz4
sudo systemctl stop Cardchaind
cp $HOME/.Cardchain/data/priv_validator_state.json $HOME/.Cardchain/priv_validator_state.json.backup
rm -rf $HOME/.Cardchain/data
curl -o - -L http://crowd.snapshot.stavr.tech:1013/crowd/crowd-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.Cardchain --strip-components 2
mv $HOME/.Cardchain/priv_validator_state.json.backup $HOME/.Cardchain/data/priv_validator_state.json
wget -O $HOME/.Cardchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crowd_Control/addrbook.json"
sudo systemctl restart Cardchaind && journalctl -u Cardchaind -f -o cat
```
 <h1 align="center"> Useful Tools</h1>

🔥EXPLORER🔥:    https://explorer.stavr.tech/CARDCHAIN/staking        `Indexer "ON"` \
🔥API🔥:         https://cc.api.t.stavr.tech \
🔥RPC🔥:         https://crowd.rpc.t.stavr.tech:443                  `Snapshot-interval = 100` \
🔥gRPC🔥:        http://crowd.grpc.t.stavr.tech:9907 \
🔥peer🔥:        `ec585d7fb38b67619dcb79aad90722f0eaf0faa3@crowd.peer.stavr.tech:21206` \
🔥Addrbook🔥:    ```wget -O $HOME/.Cardchain/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crowd_Control/addrbook.json"``` \
🔥Auto_install script🔥: ```wget -O crowd https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Crowd_Control/crowd && chmod +x crowd && ./crowd``` \
[🔥RPC Scanner🔥](https://github.com/obajay/nodes-Guides/tree/main/Projects/Crowd_Control#-we-scan-nodes-in-real-time-every-4-hours-and-we-provide-the-final-result-of-rpc-endpointswe-cannot-influence-the-operation-of-these-nodes-in-any-way-) [RAW JSON](https://rpc-check.crowd.stavr.tech/crowd/rpc_result.json)


# Cardchain Parameters:

| Parameter:                    | Value:      | 
|-------------------------------|-------------|
| Voting Rights Expiration Time |  100000     |
| Set Size                      |  5          |
| Set Price	                    |  10000000   |
| Active Sets Amount	        |  3          |
| Set Creation Fee	            |  5000000000 |
| Collateral Deposit	        |  50000000   |
| Winner Reward	                |  1000000    |
| Hourly Faucet	                |  50000000   |
| Inflation Rate	            |  1.1        |
| Rares Per Pack	            |  1          |
| Commons Per Pack	            |  4          |
| Un Commons Per Pack	        |  2          |
| Trial Period	                |  168000     |
| Game Vote Ratio	            |  20         |
| Card Auction Price Reduction Period|  20    |
| Air Drop Value	            |  5000000    |
| Air Drop Max Block Height	    |  5000000    |
| Trial Vote Reward	            |  1000000    |
| Vote Pool Fraction	        |  1000000    |
| Voting Reward Cap	            |  1000000    |
| Match Worker Delay	        |  1200       |
| Rare Drop Ratio	            |  150        |
| Exceptional Drop Ratio	    |  50         |
| Unique Drop Ratio	            |  1          |
