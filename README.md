# locals-faucetserver
a (testnet) Ether faucet with a Polymer frontend and a REST API

#prerequisites
- A running local GETH node. ( or access to a node ) with RPC-JSON enabled.
- A free Firebase account to host the queue

# installing


```
cd locals-faucetserver
npm install
cd static/locals-fawcet
bower install && npm install
gulp
cd ../../..
```

Create a lightwallet ```wallet.json```
Create a config file ```config.json```

```
{
	"etherscanroot": "http://testnet.etherscan.io/address/",
	"payoutfrequencyinsec": 60,
	"payoutamountinether": 1,
	"queuesize": 5,
	"httpport": 3000,
	"firebase": {
		"secret": "xxxxxxxxxxx",
		"url": "https://xxxxxxxxx.firebaseio.com/"
	},
	"web3": {
		"host": "http://<YOUR ETH NODE>:8545"
	}
}
```

If you made it this far, just start your faucet:

```
node index.js
```

...and point your browser to http://localhost:3000/

# Demo

You can access our faucet at:
http://faucet.ma.cx:3000/

# API

##Endpoint
```GET http://faucet.ma.cx:3000/donate/{ethereum address}```

##Request parameters
```ethereum address``` your ethereum address

##Response format
```
{
"paydate": 1461335186,
"address": "0x687422eea2cb73b5d3e242ba5456b782919afc85",
"amount": 1000000000000000000
}
```

* ```paydate``` the unix timestamp when the transaction will be executed. Depends on the current length of the queue
* ```address``` the address where the payment will be done
* ```amount``` the amount in Wei that will be transferred

##HTTP Return / error codes

* ```200``` : Request OK
* ```400``` : The address in invalid
* ```403``` : The queue is full. You should wait a moment and try again later. 










