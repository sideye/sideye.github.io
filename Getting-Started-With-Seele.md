## Setting up a Node
### Preparations
1. Install [go](https://golang.org/dl/) v1.7 or higher and the [C compiler](https://gcc.gnu.org/). 
2. In a terminal window, navigate to the `src\github.com\seeleteam` in the [GOPATH](https://github.com/golang/go/wiki/SettingGOPATH) directory. You will have to create these folders and path if it does not exist.
3. Clone the go-seele repository by running: `git clone https://github.com/seeleteam/go-seele`
3. Navigate to `\go-seele\cmd\node`, then run: `go build`
When you run this for the first time,  a node executable object should appear. 

### Running a Node
#### On Windows
**Running a Singular Node**
Execute the following command: `node start -c .\config\node1.json`
By default this will start the miner, not metrics. You can add flags at the end of the line `-m "stop"` to not start the miner, or `-t true` to [start metrics](#metrics).

**Running Multiple Nodes**
Execute the following command: `node start -c .\config\node1.json`
Then, in another terminal window, run: `node start -c .\config\node2.json`

#### On Linux & Mac
**Running a Singular Node**
Execute the following command: `./node start -c .\config\node1.json`
By default this will start the miner, not metrics. You can add flags at the end of the line `-m "stop"` to not start the miner, or `-t true` to [start metrics](#metrics).

**Running Multiple Nodes**
Execute the following command: `./node start -c .\config\node1.json`
Then, in another terminal window, run: `./node start -c .\config\node2.json`

*Note: in the [config file](#node1), there are 4 different module configurations that you can choose from to start your node.*

### Custom Configurations
You can choose your own custom module configurations and not use the default module configurations to start your node. The custom configurations can be found in the same `node` directory with file path `seeleteam\go-seele\cmd\node`.
The custom configurations are below:

<a name="node1">

	{
	  "basic":{
	    "name": "seele node1",
	    "version": "1.0",
	    "dataDir": "node1",
	    "address": "0.0.0.0:55027",
	    "coinbase": "0x010117ee8edfd14a1925e45e4cb698f195651b5a136e69ee9b394b7e8166cb1f"
	  },
	  "p2p": {
	    "privateKey": "0x8c5fe84f836732ae7935e70ed7f578851fabf533d327a36b4e9fc49b455aa721",
	    "staticNodes": [],
	    "address": "0.0.0.0:39007",
	    "networkID": 1
	  },
	  "log": {
	    "isDebug": true,
	    "printLog": false
	  },
	  "httpServer": {
	    "address": "127.0.0.1:65027",
	    "crosssorgins": [
	      "*"
	    ],
	    "whiteHost": [
	      "*"
	    ]
	  },
	  "wsserver": {
	    "address": "127.0.0.1:8080",
	    "pattern": "/ws"
	  },
	  "genesis": {
	    "accounts":{
	      "0x010171048615cfef6d03e10df133200a4266d3a8856795dd7e8873e300ecfbe4":100,
	      "0x01014a36b60fbd2bf80b1f9da08d98b11166075a595622fedca4435ec35533e0":200
	    },
	    "difficult":10000000,
	    "shard":1
	  }
	}

</a>

<table> <tbody>
<tr>
<th>Domain</th>
<th>Parameter</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="5">basic</th>
<td>name</td>
<td>Name of node</td>
</tr>
<tr>
<td>version</td>
<td>Version of node</td>
</tr>
<tr>
<td>dataDir</td>
<td>System file path of node, used to store data</td>
</tr>
<tr>
<td>address</td>
<td>Address to start RPC server</td>
</tr>
<tr>
<td>coinbase</td>
<td>Coinbase used to mine</td>
</tr>


<tr>
<th rowspan="4">p2p</th>
<td>privateKey</td>
<td>Private key for the p2p module, not used as an account</td>
</tr>
<tr>
<td>staticNodes</td>
<td>A static node. When the node is started, it will be connected to search for more nodes.</td>
</tr>
<tr>
<td>address</td>
<td>The p2p server will listen on the TCP connection, which is used as the UDP address for the Kad protocol.</td>
</tr>
<tr>
<td>networkID</td>
<td>Used to indicate the network type. For example, 1 is testnet, 2 is mainnet.</td>
</tr>


<tr>
<th rowspan="2">log</th>
<td>isDebug</td>
<td>If IsDebug is true, the log will be on the debug level, otherwise it will be on the info level.</td>
</tr>
<tr>
<td>printLog</td>
<td>If PrintLog is true, then all logs will be printed on the console, otherwise it will be written and stored in a file.</td>
</tr>


<tr>
<th rowspan="3">httpServer</th>
<td>address</td>
<td>HTTP RPC's service address.</td>
</tr>
<tr>
<td>crosssorgins</td>
<td>Sent to the client's cross-origin resource sharing origin. Note that CORS is a type of forced safety measure by the browser, which is irrelevant to the client's custom HTTP.</td>
</tr>
<tr>
<td>whiteHost</td>
<td>Whitelist of permitted hosts.</td>
</tr>


<tr>
<th rowspan="2">wsserver</th>
<td>address</td>
<td>Address of Websocket RPC server.</td>
</tr>
<tr>
<td>pattern</td>
<td>Pattern to request path.</td>
</tr>

<tr>
<th rowspan="3">genesis</th>
<td>accounts</td>
<td>Account information of the genesis block, used for testing.</td>
</tr>
<tr>
<td>difficult</td>
<td>Difficulty level: should be difficult near the beginning in order for easier block creation.</td>
</tr>
<tr>
<td>shard</td>
<td>Number of shards in the genesis block.</td>
</tr>
</table>


### Help
To get help, run `node -h` on Windows or `./node -h` on Mac or Linux. The help window displays the following:
<a name="help1">

	use "node help [<command>]" for detailed usage
	
	Usage:
	  node [command]

	Available Commands:
	  help        Help about any command
	  key         generate a key pair with specified shard number
	  start       start the node of Seele
	  validatekey validate the private key and generate its public key

	Flags:
	  -a, --addr string   rpc address (default "127.0.0.1:55027")
	  -h, --help          help for node

	Use "node [command] --help" for more information about a command.
</a>

### Others
#### Create Keys
To create a public and private key, run in the command window: `node key` on Windows or `./node key` on Mac or Linux.

To create a new public key based on an existing private key, run in the command window `node validatekey -k PRIVATEKEY` on Windows or `./node validatekey -k PRIVATEKEY` on Mac or Linux, where the PRIVATEKEY is your private key.

### Start metrics
First install [influxdb](https://github.com/influxdata/influxdb), and add the following code to your custom module [configurations](#node1):

<a>

	"metrics": {
	    "address": "127.0.0.1:8086",
	    "duration": 10,
	    "database": "influxdb",
	    "username": "test",
	    "password": "test123"
	  }

</a>

<table> <tbody>
<tr>
<th>Domain</th>
<th>Parameter</th>
<th>Explanation</th>
</tr>
<tr>
<th rowspan="5">metrics</th>
<td>addres</td>
<td>Address of Metrics RPC server.</td>
</tr>
<tr>
<td>duration</td>
<td>Interval of write to influxdb database</td>
</tr>
<tr>
<td>database</td>
<td>Name of influxdb database</td>
</tr>
<tr>
<td>username</td>
<td>Username of influxdb database</td>
</tr>
<tr>
<td>password</td>
<td>Password of influxdb database</td>
</tr>
</table>

## Create a Client Node
### Preparations
1. Install [go](https://golang.org/dl/) v1.7 or higher and the [C compiler](https://gcc.gnu.org/). 
2. Navigate to `seeleteam\go-seele\cmd\client`, then run: `go build`
If you are running this for the first time, a client executable object will appear.

### Running a Client Node
**On Windows**
In the command window, run: `client`
**On Mac & Linux**
In the command window, run: `./client`

### Help
To get help, run `client -h` on Windows or `./client -h` on Mac or Linux. The help window displays the following:
<a name="help">

	rpc client to interact with node process

	Usage:
	  client [command]

	Available Commands:
	  getbalance              get the balance of an account
	  getblockbyhash          get block info by block hash
	  getblockbyheight        get block info by block height
	  getblockheight          get block height of the chain head
	  getblockrlp             get block rlp hex by block height
	  getblocktxcountbyhash   get block transaction count by hash
	  getblocktxcountbyheight get block transaction count by height
	  getinfo                 get the miner info
	  getnetworkversion       get current network version
	  getpeercount            get count of connected peers
	  getpeersinfo            get seele peers info
	  getprotocolversion      get seele protocol version
	  gettransactionbyhash    get transaction count by hash
	  gettxbyhashandindex     get transaction by hash and index
	  gettxbyheightandindex   get transaction by block height and index
	  gettxpoolcontent        get content of the tx pool
	  gettxpooltxcount        get the number of all processable transactions contained within the transaction pool
	  help                    Help about any command
	  key                     generate a key pair with specified shard number
	  miner                   miner actions
	  printblock              get block pretty printed form by block height
	  savekey                 save the key
	  sendtx                  send a tx to the miner

	Flags:
	  -a, --addr string     rpc address (default "127.0.0.1:55027")
	  -h, --help            help for client
	  -w, --wsaddr string   websocket rpc address (default "ws://127.0.0.1:8080/ws")

	Use "client [command] --help" for more information about a command.
</a>

| [中文(简体)](https://github.com/seeleteam/go-seele/wiki/seele%E5%90%AF%E5%8A%A8%E8%AF%B4%E6%98%8E%E6%96%87%E6%A1%A3)
| [English](https://github.com/seeleteam/go-seele/wiki/Getting-Started-With-Seele)
