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


<table><tr><th>IP-Address</th><th>Network</th><th>Moniker</th><th>Latest Block Height</th><th>Earliest Block Height</th><th>Catching Up</th><th>Tx Index</th><th>Voting Power</th><th>Scan Time</th></tr><tr><td>161.97.180.20:36657</td><td>entangle_33133-1</td><td>Blockscope 🔴</td><td>2663520</td><td>1</td><td>False</td><td>off</td><td>309757544522759</td><td>2024-03-16T05:07:31.886435467UTC</td></tr><tr><td>34.118.55.23:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2663520</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T05:07:34.617151671UTC</td></tr><tr><td>34.118.4.252:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2617124</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T05:07:34.932189548UTC</td></tr><tr><td>34.77.213.145:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2663521</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T05:07:37.241337525UTC</td></tr><tr><td>34.174.1.1:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2663521</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T05:07:37.965365108UTC</td></tr><tr><td>34.118.79.149:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2663524</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T05:08:01.707145953UTC</td></tr><tr><td>34.118.35.218:26657</td><td>entangle_33133-1</td><td>validator 🟢</td><td>2622113</td><td>1</td><td>False</td><td>on</td><td>0</td><td>2024-03-16T05:08:06.339350348UTC</td></tr><tr><td>167.235.117.3:36657</td><td>entangle_33133-1</td><td>tRDM 🔴</td><td>2663524</td><td>1</td><td>False</td><td>on</td><td>216776925020225</td><td>2024-03-16T05:08:06.609282583UTC</td></tr><tr><td>136.243.33.177:26657</td><td>entangle_33133-1</td><td>Staketab 🔴</td><td>2663523</td><td>660001</td><td>False</td><td>on</td><td>181133950212536</td><td>2024-03-16T05:07:52.996175348UTC</td></tr><tr><td>65.109.82.17:12357</td><td>entangle_33133-1</td><td>ruangnode 🔴</td><td>2663520</td><td>1312001</td><td>False</td><td>off</td><td>661261205895222</td><td>2024-03-16T05:07:32.229470516UTC</td></tr><tr><td>65.21.226.187:36657</td><td>entangle_33133-1</td><td>Sr20de 🔴</td><td>2663520</td><td>2049001</td><td>False</td><td>off</td><td>29534655065001</td><td>2024-03-16T05:07:29.373785842UTC</td></tr><tr><td>168.119.10.134:26655</td><td>entangle_33133-1</td><td>TrustedPoint-1 🟢</td><td>2663524</td><td>2268001</td><td>False</td><td>off</td><td>0</td><td>2024-03-16T05:08:06.846109314UTC</td></tr><tr><td>144.76.236.211:23657</td><td>entangle_33133-1</td><td>[NODERS]TEAM 🔴</td><td>2663522</td><td>2304001</td><td>False</td><td>off</td><td>26809518609480680</td><td>2024-03-16T05:07:50.731824708UTC</td></tr><tr><td>167.235.14.83:14657</td><td>entangle_33133-1</td><td>Appieasahbie 🔴</td><td>2663524</td><td>2436001</td><td>False</td><td>on</td><td>43265832790044774</td><td>2024-03-16T05:08:06.016089971UTC</td></tr><tr><td>149.102.146.157:17157</td><td>entangle_33133-1</td><td>warren4 🔴</td><td>2663522</td><td>2558001</td><td>False</td><td>on</td><td>505849050783707</td><td>2024-03-16T05:07:48.462654977UTC</td></tr><tr><td>213.239.217.52:33657</td><td>entangle_33133-1</td><td>n0ok 🔴</td><td>2663523</td><td>2563523</td><td>False</td><td>off</td><td>46611081777498279</td><td>2024-03-16T05:07:59.329641286UTC</td></tr><tr><td>148.251.235.130:14657</td><td>entangle_33133-1</td><td>Staketab 🟢</td><td>2663520</td><td>2617001</td><td>False</td><td>off</td><td>0</td><td>2024-03-16T05:07:29.043352670UTC</td></tr><tr><td>142.132.202.50:33657</td><td>entangle_33133-1</td><td>cryptobtcbuyer 🔴</td><td>2663520</td><td>2619001</td><td>False</td><td>off</td><td>38886577247155343</td><td>2024-03-16T05:07:31.625200310UTC</td></tr></table>
