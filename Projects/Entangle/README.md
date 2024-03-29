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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2861351</td><td>1</td><td>False</td><td>off</td><td>309761262199940</td><td>2024-03-29T03:14:13.683421348UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2861352</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T03:14:16.339631215UTC</td></tr><tr><td>34.77.213.145:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2861352</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T03:14:18.656962376UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2861355</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T03:14:31.582724684UTC</td></tr><tr><td>34.118.35.218:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2861356</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-29T03:14:33.951135128UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2861356</td><td>1</td><td>False</td><td>on</td><td>216775925020225</td><td>2024-03-29T03:14:34.246231495UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2861354</td><td>660001</td><td>False</td><td>on</td><td>181153136618817</td><td>2024-03-29T03:14:27.034527952UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2861352</td><td>1312001</td><td>False</td><td>off</td><td>661264415321192</td><td>2024-03-29T03:14:14.008267038UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2861350</td><td>2049001</td><td>False</td><td>off</td><td>29534655065001</td><td>2024-03-29T03:14:11.180949025UTC</td></tr><tr><td>168.119.10.134:26655</td><td>entangle_33133-1</td><td>TrustedPoint-1 🟢</td><td>2861356</td><td>2268001</td><td>False</td><td>off</td><td>0</td><td>2024-03-29T03:14:34.463988483UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2861350</td><td>2617001</td><td>False</td><td>off</td><td>0</td><td>2024-03-29T03:14:10.895861352UTC</td></tr><tr><td>142.132.202.50:33657</td><td>entangle_33133-1</td><td>cryptobtcbuyer 🟢</td><td>2861351</td><td>2761351</td><td>False</td><td>off</td><td>0</td><td>2024-03-29T03:14:13.413476018UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2861355</td><td>2761355</td><td>False</td><td>off</td><td>46611115204469771</td><td>2024-03-29T03:14:29.255955809UTC</td></tr></table>
