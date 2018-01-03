## UltraNote For Online Services 

Depending on how your system accounts user funds there are two ways to integrate UltraNote into an application to receive and send transactions.

UltraNote distributes two wallet solutions: `ultranotewallet` and `walletd`. Both daemons are capable of recieving and sending mass payouts. The difference is that `walletd` provides multiple wallet addresses when `ultranotewallet` provides only one wallet address. 

In this document we'll show how to use  `ultranotewallet`. If you need a multi-wallet solution (one wallet per user) refer to (./paymentgate.md)[paymentgate documentation]. Or as an example of rest microservice refer to (https://github.com/xun-project/ultra-rest)[ultra-rest].



### Using `ultranotewallet`

`ultranotewallet` provides *JSON RPC* service. At the time this is the only way to use wallet methods if your application cannot call `c++` methods directly. 


### Running

1. Before running `ultranotewallet` you need to generate a new wallet:

```sh
	~# ultranotewallet --generate-new-wallet walletname

```

2. Run the node daemon `ultranoted`:

```sh
	~# ultranoted --config-file /etc/ultranote/node.conf
```   

3. Run the wallet in RPC Server mode

```sh
	~# ultranotewallet  --wallet-file walletname --password 1234 --rpc-bind-port 8078 --rpc-user test --rpc-password 1234
``` 

Now the rpc server runs at `http://127.0.0.1:8078/json_rpc` and you can call following methods:


### Method: `getbalance()`
Get current balance

Request:
```json
{
	"method":"getbalance", 
	"params": {},
	"jsonrpc": "2.0", 
	"id": "1"
}
```


Response:
```json
{
	"id":"1",
	"jsonrpc":"2.0",
	"result":{
		"available_balance":1000,
		"balance":1000,
		"locked_amount":0,
		"unlocked_balance":0
	}
}
```


### Method: `getbalance()`



### Use cases

#### _Case 1:_ Using PaymentID 