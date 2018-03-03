# RPC Calls - Mempool

## getmempoolinfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getmempoolinfo"
  }'
```

```shell--CLI
wmcc cli rpc getmempoolinfo
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getmempoolinfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "size": 10,
  "bytes": 30432,
  "usage": 30432,
  "maxmempool": 100000000,
  "mempoolminfee": 0.00001
}
later
```

Returns informations about mempool.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getmempoolancestors

```shell--cURL
txhash='later';
verbose=1;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getmempoolancestors",
    "params": [ "'$txhash'", "'$verbose'" ]
  }'
```

```shell--CLI
txhash='later';
verbose=1;

wmcc cli rpc getmempoolancestors $txhash $verbose
```

```javascript
const txhash = 'later';
const verbose = 1;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getmempoolancestors', [ txhash, verbose ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Returns all in-mempool ancestors for a transaction in the mempool.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | txhash | Required | Transaction Hash
| 2 | verbose | false | False - returns only tx hashs, true - returns dependency tx info

## getmempooldescendants

```shell--cURL
txhash='later';

verbose=1;
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getmempooldescendants",
    "params": [ "'$txhash'", "'$verbose'" ]
  }'
```

```shell--CLI
txhash='later';
verbose=1;

wmcc cli rpc getmempooldescendants $txhash $verbose
```

```javascript
const txhash = 'later';
const verbose = 1;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getmempooldescendants', [ txhash, verbose ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Returns all in-mempool descendants for a transaction in the mempool.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | txhash | Required | Transaction Hash
| 2 | verbose | false | False - returns only tx hashs, true - returns dependency tx info

## getmempoolentry

```shell--cURL
txhash='later';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getmempoolentry",
    "params": [ "'$txhash'" ]
  }'
```

```shell--CLI
txhash='later';

wmcc cli rpc getmempoolentry $txhash
```

```javascript
const txhash = 'later';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getmempoolentry', [ txhash ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Returns mempool transaction info by its hash.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | txhash | Required | Transaction Hash

## getrawmempool

```shell--cURL
verbose=1;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getrawmempool",
    "params": [ "'$verbose'" ]
  }'
```

```shell--CLI
verbose=1;

wmcc cli rpc getrawmempool $verbose
```

```javascript
const verbose = 1;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getrawmempool', [ verbose ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Returns mempool detailed information (on verbose). Or mempool tx list.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | verbose | false  | False - returns only tx hashs, true - returns full tx info

## prioritisetransaction

```shell--cURL
txhash='';
priorityDelta=1000;
feeDelta=1000;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "prioritisetransaction",
    "params": [ "'$txhash'", "'$priorityDelta'", "'$feeDelta'" ]
  }'
```

```shell--CLI
txhash='';
priorityDelta=1000;
feeDelta=1000;

wmcc cli rpc prioritisetransaction $txhash $priorityDelta $feeDelta
```

```javascript
const txhash = '';
const priorityDelta = 1000;
const feeDelta = 1000;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('prioritisetransaction', [ txhash, priorityDelta, feeDelta ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
true
```

Prioritises the transaction.

<aside class="notice">
Changing fee or priority will only trick local miner (using this mempool) into accepting Transaction(s) into the block. (even if Priority/Fee doen't qualify)
</aside>

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | txid | Required | Transaction hash
| 2 | priority delta | Required | Virtual priority to add/subtract to the entry
| 3 | fee delta | Required | Virtual fee to add/subtract to the entry

## estimatefee

```shell--cURL
nblocks=10;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "estimatefee",
    "params": [ "'$nblocks'" ]
  }'
```

```shell--CLI
nblocks=10;

wmcc cli rpc estimatefee $nblocks
```

```javascript
const nblocks = 10;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('estimatefee', [ nblocks ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Estimates fee to be paid for transaction.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | nblocks | 1 | Number of blocks to check for estimation

## estimatepriority

```shell--cURL
nblocks=10;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "estimatepriority",
    "params": [ "'$nblocks'" ]
  }'
```

```shell--CLI
nblocks=10;

wmcc cli rpc estimatepriority $nblocks
```

```javascript
const nblocks = 10;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('estimatepriority', [ nblocks ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Estimates the priority (coin age) that a transaction needs in order to be included within a certain number of blocks as a free high-priority transaction.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | nblocks | 1 | Number of blocks to check for estimation

## estimatesmartfee

```shell--cURL
nblocks=10;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "estimatesmartfee",
    "params": [ "'$nblocks'" ]
  }'
```

```shell--CLI
nblocks=10;

wmcc cli rpc estimatesmartfee $nblocks
```

```javascript
const nblocks = 10;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('estimatesmartfee', [ nblocks ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Estimates smart fee to be paid for transaction.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | nblocks | 1 | Number of blocks to check for estimation

## estimatesmartpriority

```shell--cURL
nblocks=10;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "estimatesmartpriority",
    "params": [ "'$nblocks'" ]
  }'
```

```shell--CLI
nblocks=10;

wmcc cli rpc estimatesmartpriority $nblocks
```

```javascript
const nblocks = 10;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('estimatesmartpriority', [ nblocks ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Estimates smart priority (coin age) that a transaction needs in order to be included within a certain number of blocks as a free high-priority transaction.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | nblocks | 1 | Number of blocks to check for estimation
