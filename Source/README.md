[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Source)
=

# SnapShot (~0.3 GB) updated every 6 hours
```python
cd $HOME
sudo systemctl stop sourced
cp $HOME/.source/data/priv_validator_state.json $HOME/.source/priv_validator_state.json.backup
rm -rf $HOME/.source/data
curl -o - -L http://source.snapshot.stavr.tech:4001/source/source-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.source --strip-components 2
curl -o - -L http://source.wasm.stavr.tech:1050/wasm-snap.tar.lz4 | lz4 -c -d - | tar -x -C $HOME/.source/data --strip-components 3
mv $HOME/.source/priv_validator_state.json.backup $HOME/.source/data/priv_validator_state.json
sudo systemctl restart sourced && journalctl -u sourced -f -o cat
```
