[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/Nois)
=
# Snaphot 06.10.22 (8 GB) block height --> 
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
sudo systemctl stop noisd
rm -rf $HOME/.noisd/data/
mkdir $HOME/.noisd/data/
# download archive
cd $HOME
wget http://195.201.165.123:7050/noisddata.tar.gz
# unpack the archive
tar -C $HOME/ -zxvf noisddata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.noisd/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .noisd/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}
# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm noisddata.tar.gz
systemctl restart noisd && journalctl -u noisd -f -o cat
```
