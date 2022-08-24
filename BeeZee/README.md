[Node installation instructions](https://github.com/obajay/nodes-Guides/tree/main/BeeZee)
=
# Snaphot 24.08.22 (0.1 GB) block height --> 2293057
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
rm -rf $HOME/.bze/data/
mkdir $HOME/.bze/data/

# download archive
cd $HOME
wget http://116.202.236.115:7001/bzedata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf bzedata.tar.gz --strip-components 1
# !! IMPORTANT POINT. If the validator was created earlier. Need to reset priv_validator_state.json  !!
wget -O $HOME/.bze/data/priv_validator_state.json "https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/priv_validator_state.json"
cd && cat .bze/data/priv_validator_state.json
{
  "height": "0",
  "round": 0,
  "step": 0
}

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm bzedata.tar.gz
sudo systemctl restart bzed && sudo journalctl -u bzed -f -o cat
```
