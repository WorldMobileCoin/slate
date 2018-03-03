# RPC Calls - Block

## getblockchaininfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "method": "getblockchaininfo" }'
```

```shell--CLI
wmcc cli rpc getblockchaininfo
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblockchaininfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "chain": "mainnet",
  "blocks": 1798,
  "headers": 1798,
  "bestblockhash": "000008ec940a34757a5dcf1dad1414f48eedb41fcdd248022d53793b2db2d99c",
  "difficulty": 0.000244140625,
  "mediantime": 1513832890,
  "verificationprogress": 0.017091019843844264,
  "chainwork": "0000000000000000000000000000000000000000000000000000000070707070",
  "pruned": false,
  "softforks": [
    {
      "id": "bip34",
      "version": 2,
      "reject": {
        "status": true
      }
    },
    {
      "id": "bip66",
      "version": 3,
      "reject": {
        "status": true
      }
    },
    {
      "id": "bip65",
      "version": 4,
      "reject": {
        "status": true
      }
    }
  ],
  "bip9_softforks": {
    "csv": {
      "status": "defined",
      "bit": 0,
      "startTime": 1509494400,
      "timeout": 1541030400
    },
    "segwit": {
      "status": "defined",
      "bit": 1,
      "startTime": 1509494400,
      "timeout": 1541030400
    },
    "segsignal": {
      "status": "active",
      "bit": 4,
      "startTime": 1509494400,
      "timeout": 1541030400
    },
    "testdummy": {
      "status": "defined",
      "bit": 28,
      "startTime": 1509494400,
      "timeout": 1541030400
    }
  },
  "pruneheight": null
}
```

Returns blockchain information.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getbestblockhash

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "method": "getbestblockhash" }'
```

```shell--CLI
wmcc cli rpc getbestblockhash
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getbestblockhash');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
"0000093b3947f33f00ee5e4247606d78be62d0ac41059dbad1203d01779ee470"
```

Returns Block Hash of the tip.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getblockcount

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "method": "getblockcount" }'
```

```shell--CLI
wmcc cli rpc getblockcount
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblockcount');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
38495
```

Returns block count.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getblock

```shell--cURL
blockhash='000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774';
verbose=1;
details=0;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getblock",
    "params": [ "'$blockhash'", "'$verbose'", "'$details'" ]
  }'
```

```shell--CLI
blockhash='000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774';
verbose=1;
details=0;

wmcc cli rpc getblock $blockhash $verbose $details
```

```javascript
const blockhash = '000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774';
const verbose = 1;
const details = 0;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblock', [ blockhash, verbose, details ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "hash": "000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774",
  "confirmations": 35499,
  "strippedsize": 280,
  "size": 316,
  "weight": 1156,
  "height": 3000,
  "version": 536870912,
  "nonce": 2541542,
  "versionHex": "20000000",
  "merkleroot": "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385",
  "coinbase": "02b80b126d696e656420627920776d63635f636f726504daddb6ac080000000000000000",
  "tx": [
    "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385"
  ],
  "time": 1514098188,
  "mediantime": 1514096878,
  "bits": 503578620,
  "difficulty": 0.0009765625,
  "chainwork": "0000000000000000000000000000000000000000000000000000000174417440",
  "previousblockhash": "000000ea5b593cd198ee136524be6ca46a25154765b2eccf3d6ceff13f243562",
  "nextblockhash": "000000b0346a304c4f9bb7b672bc10cdac3cd203f105962fa64faa594cebc465"
}
```

Returns information about block.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockhash | Required | Hash of the block
| 2 | verbose | true | If set to false, it will return hex of the block
| 3 | details | false | If set to true, it will return transaction details too

## getblockbyheight

```shell--cURL
blockheight=3000;
verbose=1;
details=0;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getblockbyheight",
    "params": [ "'$blockheight'", "'$verbose'", "'$details'" ]
  }'
```

```shell--CLI
blockheight=3000;
verbose=1;
details=0;

wmcc cli rpc getblockbyheight $blockheight $verbose $details
```

```javascript
const blockheight = 3000;
const verbose = 1;
const details = 0;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblockbyheight', [ blockheight, verbose, details ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "hash": "000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774",
  "confirmations": 35500,
  "strippedsize": 280,
  "size": 316,
  "weight": 1156,
  "height": 3000,
  "version": 536870912,
  "nonce": 2541542,
  "versionHex": "20000000",
  "merkleroot": "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385",
  "coinbase": "02b80b126d696e656420627920776d63635f636f726504daddb6ac080000000000000000",
  "tx": [
    "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385"
  ],
  "time": 1514098188,
  "mediantime": 1514096878,
  "bits": 503578620,
  "difficulty": 0.0009765625,
  "chainwork": "0000000000000000000000000000000000000000000000000000000174417440",
  "previousblockhash": "000000ea5b593cd198ee136524be6ca46a25154765b2eccf3d6ceff13f243562",
  "nextblockhash": "000000b0346a304c4f9bb7b672bc10cdac3cd203f105962fa64faa594cebc465"
}
```

Returns information about block by height.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockheight | Required | Height of the block in the blockchain
| 2 | verbose | true | If set to false, it will return hex of the block
| 3 | details | false | If set to true, it will return transaction details too

## getblockhash

```shell--cURL
blockheight=3000;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getblockhash",
    "params": [ "'$blockheight'" ]
  }'
```

```shell--CLI
blockheight=3000;

wmcc cli rpc getblockhash $blockheight
```

```javascript
const blockheight = 3000;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblockhash', [ blockheight ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
"000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774"
```

Returns block's hash by height.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockheight | Required | Height of the block in the blockchain

## getblockheader

```shell--cURL
blockhash='000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774';
verbose=1;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getblockheader",
    "params": [ "'$blockhash'", "'$details'" ]
  }'
```

```shell--CLI
blockhash='000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774';
verbose=1;

wmcc cli rpc getblockheader $blockhash $verbose
```

```javascript
const blockhash = '000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774';
const verbose = 1;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getblockheader', [ blockheight, verbose ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "hash": "000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774",
  "confirmations": 35501,
  "height": 3000,
  "version": 536870912,
  "versionHex": "20000000",
  "merkleroot": "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385",
  "time": 1514098188,
  "mediantime": 1514096878,
  "bits": 503578620,
  "difficulty": 0.0009765625,
  "chainwork": "0000000000000000000000000000000000000000000000000000000174417440",
  "previousblockhash": "000000ea5b593cd198ee136524be6ca46a25154765b2eccf3d6ceff13f243562",
  "nextblockhash": "000000b0346a304c4f9bb7b672bc10cdac3cd203f105962fa64faa594cebc465"
}
```

Returns block's header by hash.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockheight | Required | Height of the block in the blockchain
| 2 | verbose | true | If set to false, it will return hex of the block

## getchaintips

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getchaintips"
  }'
```

```shell--CLI
wmcc cli rpc getchaintips
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getchaintips');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
[
  {
    "height": 33389,
    "hash": "000000000373310bebeefd0996baccc67c8efe7c8b0e9916e38c840d8cdf2e00",
    "branchlen": 1,
    "status": "valid-headers"
  },
  {
    "height": 38419,
    "hash": "000000000025e47166b1aeee010e7745708b5653c75ce74e252a9ac36cea0608",
    "branchlen": 1,
    "status": "valid-headers"
  },
  {
    "height": 31060,
    "hash": "00000000032589e67ea46869d1b9417f86cdba3ed2323800b876d7602e7a330a",
    "branchlen": 1,
    "status": "valid-headers"
  },
  ...
]
```

Returns chaintips.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getdifficulty

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getdifficulty"
  }'
```

```shell--CLI
wmcc cli rpc getdifficulty
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getdifficulty');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
689.0484608679707
```

Returns block difficulty.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None
