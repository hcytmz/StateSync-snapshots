<h1 align="center"> 🔥Eywa🔥</h1>

![eywa](https://user-images.githubusercontent.com/44331529/233964599-6d89835c-b2f4-4b4c-9814-c2fbc2b30db3.png)

<h1 align="center"> 🟢MAINNET🟢</h1>

## Automatic Mainnet snapshot unpacking  (database is updated every 5 minutes)
```python
wget -O eywam https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Projects/Eywa/eywam && chmod +x eywam && ./eywam
```

<h1 align="center"> 🔴TESTNET🔴</h1>


## Automatic Testnet snapshot unpacking (Temporarily Stopped)
```python
wget -O eywa https://raw.githubusercontent.com/obajay/StateSync-snapshots/main/Projects/Eywa/eywa && chmod +x eywa && ./eywa
```
<h1 align="center"> 📚Useful Commands📚</h1>

`Docker restart`
```python
docker restart $(docker ps -a --format='{{json .}}'|jq -r 'select(.Image|match("eywa-p2p-bridge")).Names')
```

`Logs`
```python
docker logs -f $(docker ps -a --format='{{json .}}'|jq -r 'select(.Image|match("eywa-p2p-bridge")).Names')
docker logs -f $(docker ps -a --format='{{json .}}'|jq -r 'select(.Image|match("eywa-p2p-bridge")).Names') --follow --tail=500
```
`Synchronization status`
```python
curl -s 127.0.0.1:8081/v1/sync_state|jq -r '("NODE SYNC STATE: "+.result.state),((["CHAIN","SYNCED","DIFFS","sysDIFFS"] | (., map(length*"-"))),(.result.details|keys[] as $k |["\($k)", "\(.[$k].synced)", "\(.[$k].diffs.processedHeight)", "\(.[$k].diffs.sysProcessedHeight)"])|@tsv)'
```
`Auto restart docker`
```python
docker update --restart=always $(docker ps -a --format='{{json .}}'|jq -r 'select(.Image|match("eywa-p2p-bridge")).Names')
docker restart $(docker ps -a --format='{{json .}}'|jq -r 'select(.Image|match("eywa-p2p-bridge")).Names')
```
