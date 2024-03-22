<h1 align="center"> 🔥Entangle🔥</h1>

[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Projects/Entangle)
=

<h1 align="center"> TESTNET</h1>

# StateSync Entangle Testnet
```python
SOON
```
# SnapShot (~50 GB) Arhive node
```python
cd $HOME
apt install lz4
sudo systemctl stop entangled
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1false|" ~/.entangled/config/config.toml
cp $HOME/.entangled/data/priv_validator_state.json $HOME/.entangled/priv_validator_state.json.backup
rm -rf $HOME/.entangled/data
curl -o - -L https://entangle.snapshot.stavr.tech/entagle/entagle-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.entangled --strip-components 2
mv $HOME/.entangled/priv_validator_state.json.backup $HOME/.entangled/data/priv_validator_state.json
wget -O $HOME/.entangled/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Entangle/addrbook.json"
sudo systemctl restart entangled && journalctl -u entangled -f -o cat
```
 <h1 align="center"> Useful Tools</h1>
 
🔥EXPLORER🔥: https://explorer.stavr.tech/Entangle-testnet/staking        `Indexer "ON"` \
🔥API🔥:      https://entangle.api.t.stavr.tech \
🔥Addrbook🔥: ```wget -O $HOME/.entangled/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Entangle/addrbook.json"``` \
🔥Auto_install script🔥:  `wget -O entaglet https://raw.githubusercontent.com/obajay/nodes-Guides/main/Projects/Entangle/entaglet && chmod +x entaglet && ./entaglet`


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

[raw json](https://rpc-check.entangt.stavr.tech/entangt/rpc-entangt-result.json)
=


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2747839</td><td>1</td><td>False</td><td>off</td><td>309760544247204</td><td>2024-03-22T02:08:58.016154013UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2747839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-22T02:09:00.724596573UTC</td></tr><tr><td>34.77.213.145:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2747839</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-22T02:09:03.017538809UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2747841</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-22T02:09:20.042866726UTC</td></tr><tr><td>34.118.35.218:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2622113</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-22T02:09:22.404570713UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2747842</td><td>1</td><td>False</td><td>on</td><td>216776925020225</td><td>2024-03-22T02:09:22.722818905UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2747840</td><td>660001</td><td>False</td><td>on</td><td>181152470618817</td><td>2024-03-22T02:09:11.395912044UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2747839</td><td>1312001</td><td>False</td><td>off</td><td>661262305895222</td><td>2024-03-22T02:08:58.376466190UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2747839</td><td>2049001</td><td>False</td><td>off</td><td>29534655065001</td><td>2024-03-22T02:08:55.359783707UTC</td></tr><tr><td>168.119.10.134:26655</td><td>entangle_33133-1</td><td>TrustedPoint-1 🟢</td><td>2747842</td><td>2268001</td><td>False</td><td>off</td><td>0</td><td>2024-03-22T02:09:22.971790394UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2747838</td><td>2617001</td><td>False</td><td>off</td><td>0</td><td>2024-03-22T02:08:55.048039507UTC</td></tr><tr><td>142.132.202.50:33657</td><td>entangle_33133-1</td><td>cryptobtcbuyer 🔴</td><td>2747839</td><td>2647839</td><td>False</td><td>off</td><td>38886577247155343</td><td>2024-03-22T02:08:57.621435613UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2747841</td><td>2647841</td><td>False</td><td>off</td><td>46611081777498279</td><td>2024-03-22T02:09:17.696788286UTC</td></tr></table>
