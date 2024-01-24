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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🟢</td><td>1830545</td><td>1</td><td>False</td><td>off</td><td>0</td><td>2024-01-24T00:39:12.965739646UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1830548</td><td>1</td><td>False</td><td>off</td><td>27049800500000000</td><td>2024-01-24T00:39:24.745138755UTC</td></tr><tr><td>34.116.174.56:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1830326</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-24T00:39:29.559049995UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1830435</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-24T00:39:32.245483424UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🟢</td><td>1830549</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-24T00:39:33.122351745UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1830548</td><td>660001</td><td>False</td><td>on</td><td>0</td><td>2024-01-24T00:39:27.154928651UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1830545</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-01-24T00:39:12.622912864UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🟢</td><td>1830547</td><td>725001</td><td>False</td><td>on</td><td>0</td><td>2024-01-24T00:39:18.001644747UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1830547</td><td>962001</td><td>False</td><td>on</td><td>311893412878335</td><td>2024-01-24T00:39:17.648948966UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1830546</td><td>1312001</td><td>False</td><td>off</td><td>409033785205252</td><td>2024-01-24T00:39:13.310793104UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>1830548</td><td>1436001</td><td>False</td><td>on</td><td>484417023854259</td><td>2024-01-24T00:39:24.506432174UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1830549</td><td>1716001</td><td>False</td><td>on</td><td>44123221801989996</td><td>2024-01-24T00:39:32.789860824UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1830548</td><td>1730548</td><td>False</td><td>off</td><td>46574392273662988</td><td>2024-01-24T00:39:29.781906697UTC</td></tr><tr><td>158.220.91.214:17157</td><td>entangle_33133-1</td><td>Iryna2 🔴</td><td>1830549</td><td>1822001</td><td>False</td><td>on</td><td>298287408343724</td><td>2024-01-24T00:39:32.553198454UTC</td></tr></table>
