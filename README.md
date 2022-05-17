# hyperism-ether
Private ethereum network for decentralized storage network

## Quick Overview

```bash
git clone https://github.com/hyperism/hyperism-ether
cd hyperism-ether
docker-compose up -d
```

https://ravinayag.medium.com/ethereum-private-network-with-ipfs-f97dc39c5d68
```bash
# Node1
geth --identity "Node1" --datadir node1-datadir init ./genesis.json

WADDR1=`geth --datadir ./node1-datadir --password pass.txt account new | egrep "Public address of the key:" | awk '{print $6}'`

geth --port 30303 --networkid 1369 --nodiscover --syncmode 'full' --datadir=./node1-datadir --maxpeers=10  -http  -http.api "eth,personal,web3,miner,net,admin,personal,debug" --http.vhosts localhost.local,localhost,127.0.0.1 --http.rpcprefix / -http.port="8545" --http.addr 127.0.0.1 --http.corsdomain "*" --allow-insecure-unlock --mine --miner.threads=1 --miner.etherbase=0x0000000000000000000000000000000000000000 --unlock $WADDR1 --password  pass.txt --verbosity 5 --nat extip:172.26.7.19

# Node2
geth --identity "Node2" --datadir node2-datadir init ./genesis.json

geth --datadir ./node2-datadir --networkid 1369 --port 30305 --bootnodes "enode://7bea031adf1d26999fa181430e0b40e2e7703c32a7834bfdbf4ca91f94882932d8ddac3aa2b9773bbc68162742a30ef6768cd24db0356bfa0e34c5c5586e9a88@172.26.7.19:30303"

# IPFS Setup
ifps init
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Origin '["*"]'
ipfs config --json Gateway.HTTPHeaders.Access-Control-Allow-Origin '["*"]'
ipfs config --json API.HTTPHeaders.Access-Control-Allow-Methods '["PUT", "POST"]'
```
# Demo

```bash
geth -datadir ./miner1 init genesis.json

geth -networkid 42 -datadir "~/miner1" -http -http.port "8545" -ipcpath "~/Library/Ethereum/geth.ipc" -http.api="debug,eth,net,web3,personal,web3" -http.corsdomain "*" --snapshot=false
```

## Contact

You can contact me via e-mail (sinjihng at gmail.com). I am always happy to answer questions or help with any issues you might have, and please be sure to share any additional work or your creations with me, I love seeing what other people are making.

## License
<img align="right" src="http://opensource.org/trademarks/opensource/OSI-Approved-License-100x137.png">

The class is licensed under the [MIT License](http://opensource.org/licenses/MIT):

Copyright (c) 2022 Team Hyperism
*   [Jihong Shin](https://github.com/Snowapril)
*   [Hyungeun Lee](https://github.com/leehyunk6310)

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:
The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.
THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

