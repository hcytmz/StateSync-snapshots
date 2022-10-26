[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Pylons)
=
# SnapShot 26.10.22 (4.7 GB) block height --> 2700740
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop pylonsd
rm -rf $HOME/.pylons/data/
mkdir $HOME/.pylons/data/

# download archive
cd $HOME
wget http://pylons.snap.stavr.tech:7140/pylonsdata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf pylonsdata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.pylons/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Canto/priv_validator_state.json"
cd && cat .pylons/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}
# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm pylonsdata.tar.gz
wget -O $HOME/.pylons/config/addrbook.json "https://raw.githubusercontent.com/obajay/nodes-Guides/main/Pylons/addrbook.json"
systemctl restart pylonsd && journalctl -u pylonsd -f -o cat
```
