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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2227028</td><td>1</td><td>False</td><td>off</td><td>291505448859642</td><td>2024-02-17T00:25:52.068610343UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>2227029</td><td>1</td><td>False</td><td>off</td><td>27067334033496295</td><td>2024-02-17T00:25:57.871068368UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2227031</td><td>1</td><td>False</td><td>on</td><td>181490473308767</td><td>2024-02-17T00:26:07.412136335UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2227030</td><td>660001</td><td>False</td><td>on</td><td>152589157277482</td><td>2024-02-17T00:26:00.234752903UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2227028</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-02-17T00:25:51.331687248UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>2227029</td><td>962001</td><td>False</td><td>on</td><td>330341387407861</td><td>2024-02-17T00:25:52.696700242UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2227029</td><td>1312001</td><td>False</td><td>off</td><td>500155432656040</td><td>2024-02-17T00:25:52.437018180UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>2227029</td><td>1910001</td><td>False</td><td>off</td><td>311415349656046</td><td>2024-02-17T00:25:53.118633200UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>2227031</td><td>2042001</td><td>False</td><td>on</td><td>43255612751945201</td><td>2024-02-17T00:26:07.004362279UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2227028</td><td>2049001</td><td>False</td><td>off</td><td>17505985152165</td><td>2024-02-17T00:25:51.706432774UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>2227029</td><td>2098001</td><td>False</td><td>on</td><td>493316762961910</td><td>2024-02-17T00:25:57.618083858UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2227030</td><td>2127030</td><td>False</td><td>off</td><td>46591059137506417</td><td>2024-02-17T00:26:04.589075813UTC</td></tr></table>
