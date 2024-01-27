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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>1874575</td><td>1</td><td>False</td><td>off</td><td>260910631668846</td><td>2024-01-27T01:07:32.398335100UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>1874578</td><td>1</td><td>False</td><td>off</td><td>27051343670028437</td><td>2024-01-27T01:07:44.455700660UTC</td></tr><tr><td>34.116.174.56:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1874579</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T01:07:51.344610577UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>1874580</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T01:07:54.103119540UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>1874580</td><td>1</td><td>False</td><td>on</td><td>157323948832723</td><td>2024-01-27T01:07:55.263376311UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>1874578</td><td>660001</td><td>False</td><td>on</td><td>122591340155031</td><td>2024-01-27T01:07:46.805146604UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>1874575</td><td>660801</td><td>False</td><td>on</td><td>0</td><td>2024-01-27T01:07:31.999540984UTC</td></tr><tr><td>188.165.220.208:17157</td><td>entangle_33133-1</td><td>lankouFUF 🔴</td><td>1874577</td><td>725001</td><td>False</td><td>on</td><td>312957857450251</td><td>2024-01-27T01:07:37.374068246UTC</td></tr><tr><td>168.119.38.252:17157</td><td>entangle_33133-1</td><td>gumat 🔴</td><td>1874577</td><td>962001</td><td>False</td><td>on</td><td>322771596871955</td><td>2024-01-27T01:07:37.098267731UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>1874576</td><td>1312001</td><td>False</td><td>off</td><td>445887998773718</td><td>2024-01-27T01:07:32.778513467UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>1874578</td><td>1436001</td><td>False</td><td>on</td><td>485006183854259</td><td>2024-01-27T01:07:44.216973357UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>1874580</td><td>1716001</td><td>False</td><td>on</td><td>44123292301989996</td><td>2024-01-27T01:07:54.881098459UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>1874580</td><td>1774580</td><td>False</td><td>off</td><td>46574465273662988</td><td>2024-01-27T01:07:51.599405692UTC</td></tr><tr><td>158.220.91.214:17157</td><td>entangle_33133-1</td><td>Iryna2 🔴</td><td>1874580</td><td>1822001</td><td>False</td><td>on</td><td>298476322778473</td><td>2024-01-27T01:07:54.586642650UTC</td></tr></table>
