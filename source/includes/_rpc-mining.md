# RPC Calls - Mining

## getnetworkhashps

```shell--cURL
blocks=100;
height=40000;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getnetworkhashps",
    "params": [ "'$blocks'", "'$height'" ]
  }'
```

```shell--CLI
blocks=100;
height=40000;

wmcc cli rpc getnetworkhashps $blocks $height
```

```javascript
const blocks = 100;
const height = 40000;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getnetworkhashps', [ blocks, height ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
137203790586.74084
```

Returns the estimated current or historical network hashes per second, based on last blocks.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blocks | 120 | Number of blocks to lookup
| 2 | height | 1 | Starting height for calculations

## getmininginfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getmininginfo",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getmininginfo
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getmininginfo', []);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "blocks": 40362,
  "currentblocksize": 0,
  "currentblockweight": 0,
  "currentblocktx": 0,
  "difficulty": 0,
  "errors": "",
  "genproclimit": 0,
  "networkhashps": 24046735192.49907,
  "pooledtx": 0,
  "testnet": false,
  "chain": "mainnet",
  "generate": false
}
```

Returns mining info.

<aside class="notice3">
Currentblocksize, currentblockweight, currentblocktx, difficulty are returned when there's active work. generate - is true when wmcc itself is mining.
</aside>

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getwork

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getwork",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getwork
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getwork');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "data": "200000000114a149005805d7815d010fd8fb72cea9b71962c4ee903e000b86d60000000092b433f3ca27bc115a243022a0687d9f129c032ef2d7e4e2d88375318fc40f3e5a9985c51b17c70000000000000000800000000000000000000000000000000000000000000000000000000000000000000000000000000080020000",
  "target": "00000000000000000000000000000000000000000000000000c7170000000000",
  "height": 40365
}
```

Returns hashing work to be solved by miner. Or submits solved block.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | data |  | Data to be submitted to the network.

## getworklp

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getworklp",
    "params": []
  }'
```

```shell--CLI
# Because there is a request timeout set on CLI http requests
# without manually adjusting the timeout, this call will timeout before the request is complete

wmcc cli rpc getworklp
```

```javascript
# Because there is a request timeout set on CLI http requests
# without manually adjusting the timeout, this call will timeout before the request is complete

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getworklp');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later *timeout*
```

Returns hashing work to be solved by miner. Or submits solved block.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | data |  | Data to be submitted to the network.

## getblocktemplate

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getblocktemplate",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getblocktemplate
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblocktemplate');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later *segwit*
```

Returns block template or proposal for use with mining. Also validates proposal if mode is specified as proposal.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | jsonrequestobject | {} | JSONRequestObject

## submitblock

```shell--cURL
blockdata='1000002042c21ec39ff2fe5627cadccb74d5bd96f946d32e43f22966b94f77b47f060000e2838023c7111d8454129bcb334cbe5bb1aa54a6624c12516209bac4453be42ca48a3a5af0ff0f1e5e89030001010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000ffffffff0300f2052a010000001600148dca4b88efee49e6756ba2ed09e1e27e994a679e0065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000';

# Block data is old, so it should return error
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "submitblock",
    "params": [ "'$blockdata'" ]
  }'
```

```shell--CLI
blockdata='1000002042c21ec39ff2fe5627cadccb74d5bd96f946d32e43f22966b94f77b47f060000e2838023c7111d8454129bcb334cbe5bb1aa54a6624c12516209bac4453be42ca48a3a5af0ff0f1e5e89030001010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000ffffffff0300f2052a010000001600148dca4b88efee49e6756ba2ed09e1e27e994a679e0065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000';

# Block data is old, so it should return error
wmcc cli rpc submitblock $blockdata
```

```javascript
const blockdata = '1000002042c21ec39ff2fe5627cadccb74d5bd96f946d32e43f22966b94f77b47f060000e2838023c7111d8454129bcb334cbe5bb1aa54a6624c12516209bac4453be42ca48a3a5af0ff0f1e5e89030001010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000ffffffff0300f2052a010000001600148dca4b88efee49e6756ba2ed09e1e27e994a679e0065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  // Block data is old, so it should return error
  const res = await rpc.execute('submitblock', [ blockdata ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
true
```

Adds block to chain.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockdata | Required | Mined block data (hex)

## setgenerate

```shell--cURL
blockdata='1000002042c21ec39ff2fe5627cadccb74d5bd96f946d32e43f22966b94f77b47f060000e2838023c7111d8454129bcb334cbe5bb1aa54a6624c12516209bac4453be42ca48a3a5af0ff0f1e5e89030001010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000ffffffff0300f2052a010000001600148dca4b88efee49e6756ba2ed09e1e27e994a679e0065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000';

# Block data is old, so it should return error
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "verifyblock",
    "params": [ "'$blockdata'" ]
  }'
```

```shell--CLI
blockdata='1000002042c21ec39ff2fe5627cadccb74d5bd96f946d32e43f22966b94f77b47f060000e2838023c7111d8454129bcb334cbe5bb1aa54a6624c12516209bac4453be42ca48a3a5af0ff0f1e5e89030001010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000ffffffff0300f2052a010000001600148dca4b88efee49e6756ba2ed09e1e27e994a679e0065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000';

# Block data is old, so it should return error
wmcc cli rpc verifyblock $blockdata
```

```javascript
const blockdata = '1000002042c21ec39ff2fe5627cadccb74d5bd96f946d32e43f22966b94f77b47f060000e2838023c7111d8454129bcb334cbe5bb1aa54a6624c12516209bac4453be42ca48a3a5af0ff0f1e5e89030001010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000ffffffff0300f2052a010000001600148dca4b88efee49e6756ba2ed09e1e27e994a679e0065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  // Block data is old, so it should return error
  const res = await rpc.execute('verifyblock', [ blockdata ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
true
```

Verifies the block data.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockdata | Required | Mined block data (hex)

## setgenerate

```shell--cURL
mining=1;
proclimit=1;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "setgenerate",
    "params": [ "'$mining'", "'$proclimit'" ]
  }'
```

```shell--CLI
mining=1;
proclimit=1;

wmcc cli rpc setgenerate $mining $proclimit
```

```javascript
const mining = 1;
const proclimit = 1;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('setgenerate', [ mining, proclimit ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
true
```

Will start/stop the mining on CPU.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | mining | 0 | Set to true will start mining, false will stop.
| 2 | proclimit | 0 | 

## getgenerate

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getgenerate",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getgenerate
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getgenerate');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
true
```

Returns status of mining on Node.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## generate

```shell--cURL
numblocks=2;

# Will return once all blocks are mined.
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "generate",
    "params": [ "'$numblocks'" ]
  }'
```

```shell--CLI
numblocks=2;

# Timeout error
wmcc cli rpc generate $numblocks
```

```javascript
const numblocks = 2;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  // Timeout error
  const res = await rpc.execute('generate', [ numblocks ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Mines `numblocks` number of blocks.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | numblocks | 1 | Number of blocks to mine
| 2 | maxtries |  | 

## generatetoaddress

```shell--cURL
numblocks=2;
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

# Will return once all blocks are mined.
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "generatetoaddress",
    "params": [ "'$numblocks'", "'$address'" ]
  }'
```

```shell--CLI
numblocks=2;
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

# Timeout error
wmcc cli rpc generatetoaddress $numblocks $address
```

```javascript
const numblocks = 2;
const address = 'wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  // Timeout error
  const res = await rpc.execute('generate', [ numblocks ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Mines `blocknumber` blocks, with `address` as coinbase.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | numblocks | 1 | Number of blocks to mine
| 2 | address |  | Coinbase address for new blocks
