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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>1961560</td><td>1</td><td>False</td><td>off</td><td>279513553364852</td><td>2024-02-01T10:00:38.106622339UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1961560</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T10:00:41.036927223UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1961564</td><td>1</td><td>False</td><td>off</td><td>27051519422893186</td><td>2024-02-01T10:00:53.072704948UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1961565</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T10:01:02.376657709UTC</td></tr><tr><td>34.118.35.218:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1961566</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T10:01:05.121795068UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>1961566</td><td>1</td><td>False</td><td>on</td><td>161372189824067</td><td>2024-02-01T10:01:05.562862209UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>1961564</td><td>660001</td><td>False</td><td>on</td><td>123648547937648</td><td>2024-02-01T10:00:55.443593256UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1961559</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-02-01T10:00:35.749545783UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1961561</td><td>962001</td><td>False</td><td>on</td><td>324016353984329</td><td>2024-02-01T10:00:43.376461591UTC</td></tr><tr><td>89.117.63.35:14257</td><td>entangle_33133-1</td><td>VTB-ENTANGLE 🟢</td><td>1961563</td><td>1162001</td><td>False</td><td>off</td><td>0</td><td>2024-02-01T10:00:50.381628442UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1961560</td><td>1312001</td><td>False</td><td>off</td><td>460261891995009</td><td>2024-02-01T10:00:38.596124224UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1961566</td><td>1716001</td><td>False</td><td>on</td><td>43682117087839595</td><td>2024-02-01T10:01:04.703820431UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1961565</td><td>1861565</td><td>False</td><td>off</td><td>46577001986356485</td><td>2024-02-01T10:00:59.865170234UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>1961561</td><td>1910001</td><td>False</td><td>off</td><td>303677550560871</td><td>2024-02-01T10:00:43.734592772UTC</td></tr></table>
