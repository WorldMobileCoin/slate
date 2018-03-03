# Node

## JSON-RPC Requests

```shell--cURL
curl $url \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "method": "getblockchaininfo", "params": [] }'
```

Route for JSON-RPC requests, most of which mimic the bitcoind RPC calls completely.

### HTTP Request

`POST /`

More about RPC Requests in RPC Docs.

## Get server info

```shell--cURL
curl $url/
```

```shell--CLI
wmcc cli info
```

```javascript
const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();
  const info = await client.getInfo();

  console.log(info);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "version": "v1.0.0-beta.1",
  "network": "mainnet",
  "chain": {
    "height": 37766,
    "tip": "000000000064cabec0739edc60c976bb6be8175f0631dfcd6a908b61545f63c6",
    "progress": 1
  },
  "pool": {
    "host": "115.164.83.225",
    "port": 8880,
    "agent": "/wmcc:v1.0.0-beta.1/",
    "services": "1001",
    "outbound": 27,
    "inbound": 58
  },
  "mempool": {
    "tx": 0,
    "size": 0
  },
  "time": {
    "uptime": 23,
    "system": 1519816083,
    "adjusted": 1519816132,
    "offset": 49
  },
  "memory": {
    "total": 98,
    "jsHeap": 23,
    "jsHeapTotal": 38,
    "nativeHeap": 60,
    "external": 62
  }
}
```

Get server Info.

### HTTP Request

Get server info. No params.

`GET /`

No Params.

## Get mempool snapshot

```shell--cURL
curl $url/mempool
```

```shell--CLI
wmcc cli mempool
```

```javascript
const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();
  const mempoolTxs = await client.getMempool();

  console.log(mempoolTxs);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
[
  "58a16a5ad4baaf061360ae2cf8ed3fb1fff53d46394a245721166df444c88427",
  "ef54e616f21d517bb7f5bf690892afc4a64313a910f176e9f329767bc89067fc",
  "e0e7b6a6354b9dd85b019536d6636a2ec56cedaf5f6fca7dda9ad96abafac298",
  ...
]
```

Get mempool snapshot (array of json txs).

### HTTP Request

`GET /mempool`

No Params.

## Get block by hash or height

```shell--cURL
blockHash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';
blockHeight='1000';

curl $url/block/$blockHash # by hash
curl $url/block/$blockHeight # by height
```

```shell--CLI
blockHash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';
blockHeight='1000';

wmcc cli block $blockHash # by hash
wmcc cli block $blockHeight # by height
```

```javascript
const blockHash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';
const blockHeight='1000';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();
  const blockByHash = await client.getBlock(blockHash);
  const blockByHeight = await client.getBlock(blockHeight);

  console.log(blockByHash, blockByHeight);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "hash": "00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38",
  "height": 1000,
  "version": 536870928,
  "prevBlock": "0000067fb4774fb96629f2432ed346f996bdd574cbdcca2756fef29fc31ec242",
  "merkleRoot": "2ce43b45c4ba096251124c62a654aab15bbe4c33cb9b1254841d11c7238083e2",
  "time": 1513786020,
  "bits": 504365040,
  "nonce": 231774,
  "txs": [
    {
      "hash": "2ce43b45c4ba096251124c62a654aab15bbe4c33cb9b1254841d11c7238083e2",
      "witnessHash": "96b8e9877e0e025157c27818d18aa7c58192500ac051d6457474c5a3678e1b05",
      "fee": 0,
      "rate": 0,
      "mtime": 1519816880,
      "index": 0,
      "version": 1,
      "inputs": [
        {
          "prevout": {
            "hash": "0000000000000000000000000000000000000000000000000000000000000000",
            "index": 4294967295
          },
          "script": "02e803126d696e656420627920776d63635f636f72650457e3f57b080000000000000000",
          "witness": "01200000000000000000000000000000000000000000000000000000000000000000",
          "sequence": 4294967295,
          "address": null
        }
      ],
      "outputs": [
        {
          "value": 5000000000,
          "script": "00148dca4b88efee49e6756ba2ed09e1e27e994a679e",
          "address": "wc1q3h9yhz80aey7vatt5tksnc0z06v55eu78dqwxt"
        },
        {
          "value": 500000000,
          "script": "76a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac",
          "address": "WV17cxcpPmNNJYuFp7nkNoXJ75uZj11zTC"
        },
        {
          "value": 0,
          "script": "6a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf9",
          "address": null
        }
      ],
      "locktime": 0,
      "hex": "010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402e803126..."
    }
  ]
}
```

Returns block info by block hash or height.

### HTTP Request

`GET /block/:blockhashOrHeight`

### URL Parameters

Parameter | Description
--------- | -----------
:blockhashOrHeight | Hash or Height of block

## Broadcast transaction

```shell--cURL
tx='0100000001c3f71d1defd642062799dc895ca8bc6e6b1e27e994ca8bc6e6ba799962b48b...';

curl $url/broadcast \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "tx": "'$tx'" }'
```

```shell--CLI
tx='0100000001c3f71d1defd642062799dc895ca8bc6e6b1e27e994ca8bc6e6ba799962b48b...';

wmcc cli broadcast $tx
```

```javascript
const tx='0100000001c3f71d1defd642062799dc895ca8bc6e6b1e27e994ca8bc6e6ba799962b48b...';

const client = new Core.http.Client({
  network: 'mainnet',
});

(async () => {
  await client.open();

  const result = await client.broadcast(tx);

  console.log(result);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{
  "success": true
}
```

Broadcast a transaction by adding it to the node's mempool. If mempool verification fails, the node will still forcefully advertise and relay the transaction for the next 60 seconds.

### HTTP Request

`POST /broadcast`

### POST Parameters (JSON)

Parameter | Description
--------- | -----------
tx | transaction hash