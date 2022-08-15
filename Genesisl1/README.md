# SnapSHot 13.08.22 (23 GB)
```bash
# install the node as standard, but do not launch. Then we delete the .data directory and create an empty directory
rm -rf $HOME/.genesisd/data/
mkdir $HOME/.genesisd/data/

# download archive
cd $HOME
wget http://195.201.165.123:8000/genesisddata.tar.gz

# unpack the archive
tar -C $HOME/ -zxvf genesisddata.tar.gz --strip-components 1

# after unpacking, run the node
# don't forget to delete the archive to save space
cd $HOME
rm genesisddata.tar.gz
```
