# Transaction

Getting transaction information via API.

<aside class="notice">
You need to enable <code>index-tx</code> in order to lookup transactions by transaction hashes and also enable <code>index-address</code> to lookup transaction by addresses too.
</aside>

## Get tx by txhash

```shell--cURL
txhash='93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';

curl $url/tx/$txhash
```

```shell--CLI
txhash='93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';

wmcc cli tx $txhash
```

```javascript
const hash = '93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();

  const tx = await client.getTX(txhash);

  console.log(tx);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "hash": "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385",
  "witnessHash": "03fa0cc2887608d8e85b11b557f7794786bc823d402f563456a5e92993031a13",
  "fee": 0,
  "rate": 0,
  "mtime": 1516127377,
  "height": 3000,
  "block": "000002d3f7dbc79d1bbaff4cb76e77bc6c8df3728f0c1e419de86b8830056774",
  "time": 1514098188,
  "index": 0,
  "version": 1,
  "inputs": [
    {
      "prevout": {
        "hash": "0000000000000000000000000000000000000000000000000000000000000000",
        "index": 4294967295
      },
      "script": "02b80b126d696e656420627920776d63635f636f726504daddb6ac080000000000000000",
      "witness": "01200000000000000000000000000000000000000000000000000000000000000000",
      "sequence": 4294967295,
      "address": null
    }
  ],
  "outputs": [
    {
      "value": 5000000000,
      "script": "00141e8adf6f166aceec5fc65080aa1f88a3a260dd10",
      "address": "wc1qr69d7mckdt8wch7x2zq258ug5w3xphgs2sxpwg"
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
  "hex": "010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2402b80b126d696e656420627920776d63635f636f726504daddb6ac080000000000000000ffffffff0300f2052a010000001600141e8adf6f166aceec5fc65080aa1f88a3a260dd100065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000"
}
```

Returns transaction objects by transaction hash.

### HTTP Request

`GET /tx/:txhash`

### URL Parameters

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | txhash | Hash of tx

## Get tx by address

```shell--cURL
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

curl $url/tx/address/$address
```

```shell--CLI
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

wmcc cli tx $address
```

```javascript
const address = 'wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();

  const txs = await client.getTXByAddress(address);

  console.log(txs);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  {
    "hash": "1f99f3ea4e8f97428520436d63fc1f2f9a46e052d6cf798ba70881c76f016473",
    "witnessHash": "ab246207ebe4d139e2c8249ddecb59e833e683234193544b8b98e03f012d3fe3",
    "fee": 14000,
    "rate": 99290,
    "mtime": 1516128901,
    "height": 11508,
    "block": "0000003c98972eaf21a5e42b46de6db0baf388e6c637d51a3fece50f63faa2ee",
    "time": 1515440066,
    "index": 1,
    "version": 1,
    "inputs": [
      {
        "prevout": {
          "hash": "9084b8e5f47a907e5f64ab025d9b6e9b8d03f2cb5cb2f43d2dc38502ef489c3e",
          "index": 0
        },
        "script": "",
        "witness": "0247304402201fef4f614d9a3743a7ce1ea4fc08ea605a14f52a3b5500d3b1de855143f736c6022035bfb53e34d1f534f098a3b14b32cabb9b64c8b802c25a275a0c71f2e4d85506012102fc8a6976837630608b2fdcbc8528a43bfc10e1ab473ae65247f3a03d92135605",
        "sequence": 4294967295,
        "coin": {
          "version": 1,
          "height": 1365,
          "value": 5000000000,
          "script": "0014a1925e42c0ff25bebd156891ef0680f573fcffa7",
          "address": "wc1q5xf9uskqlujma0g4dzg77p5q74elela8jexdtz",
          "coinbase": true
        }
      }
    ],
    "outputs": [
      {
        "value": 467610000,
        "script": "00140469e2609ea55b89369b916ba740d8f394bd5c88",
        "address": "wc1qq357ycy754dcjd5mj946wsxc7w2t6hygxfg9ft"
      },
      {
        "value": 4532376000,
        "script": "001443e2aa012ff6c90ca3940679c0a6821c4e41e203",
        "address": "wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav"
      }
    ],
    "locktime": 0,
    "hex": "010000000001013e9c48ef0285c32d3df4b25ccbf2038d9b6e9b5d02ab645f7e907af4e5b884900000000000ffffffff029029df1b000000001600140469e2609ea55b89369b916ba740d8f394bd5c88c091260e0100000016001443e2aa012ff6c90ca3940679c0a6821c4e41e2030247304402201fef4f614d9a3743a7ce1ea4fc08ea605a14f52a3b5500d3b1de855143f736c6022035bfb53e34d1f534f098a3b14b32cabb9b64c8b802c25a275a0c71f2e4d85506012102fc8a6976837630608b2fdcbc8528a43bfc10e1ab473ae65247f3a03d9213560500000000"
  },
  ...
]
```

Returns transaction objects array by address.

### HTTP Request

`GET /tx/address/:address`

### URL Parameters

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | address | WMCC Address

## Get tx by addresses

```shell--cURL
address0='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';
address1='wc1qp5mqu3axakk7rnv3egpacnh4a4pm9mm33p0pag';

 curl $url/tx/address \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "addresses":[ "'$address0'", "'$address1'" ]}'
```

```shell--CLI
No CLI Option.
```

```javascript
const address0 = 'wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';
const address1 = 'wc1qp5mqu3axakk7rnv3egpacnh4a4pm9mm33p0pag';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();

  const txs = await client.getTXByAddress([address0, address1]);

  console.log(txs);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  ...,
  {
    "hash": "98c2faba6ad99ada7dca6f5fafed6cc52e6a63d63695015bd89d4b35a6b6e7e0",
    "witnessHash": "b7fe2d49e1e05b04929ecbbb444b5410dbea62f62f828f18ce68bf47e7ece6b6",
    "fee": 14000,
    "rate": 99290,
    "mtime": 1516128887,
    "height": 11218,
    "block": "00000011d493899de55b981f67151964cdf6486a92fc6b22b22384191447a0cb",
    "time": 1515382539,
    "index": 1,
    "version": 1,
    "inputs": [
      {
        "prevout": {
          "hash": "1134b445ebe98a890284ece292a8b63b8fc7cbb577fa086a05e2e09b2d64d23d",
          "index": 0
        },
        "script": "",
        "witness": "02473044022017187b9bdc387a65bae66bf5961e8acb6c514853654e694c734b9f761ed10c3802205b4f41524e5b29a93b093e4deff4d2cc0846310f0361a429c67efedfc9c82a67012102db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd50443006",
        "sequence": 4294967295,
        "coin": {
          "version": 1,
          "height": 1254,
          "value": 5000000000,
          "script": "00148dca4b88efee49e6756ba2ed09e1e27e994a679e",
          "address": "wc1q3h9yhz80aey7vatt5tksnc0z06v55eu78dqwxt",
          "coinbase": true
        }
      }
    ],
    "outputs": [
      {
        "value": 100000000,
        "script": "00140469e2609ea55b89369b916ba740d8f394bd5c88",
        "address": "wc1qq357ycy754dcjd5mj946wsxc7w2t6hygxfg9ft"
      },
      {
        "value": 4899986000,
        "script": "00140d360e47a6edade1cd91ca03dc4ef5ed43b2ef71",
        "address": "wc1qp5mqu3axakk7rnv3egpacnh4a4pm9mm33p0pag"
      }
    ],
    "locktime": 0,
    "hex": "010000000001013dd2642d9be0e2056a08fa77b5cbc78f3bb6a892e2ec8402898ae9eb45b434110000000000ffffffff0200e1f505000000001600140469e2609ea55b89369b916ba740d8f394bd5c8850da0f24010000001600140d360e47a6edade1cd91ca03dc4ef5ed43b2ef7102473044022017187b9bdc387a65bae66bf5961e8acb6c514853654e694c734b9f761ed10c3802205b4f41524e5b29a93b093e4deff4d2cc0846310f0361a429c67efedfc9c82a67012102db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd5044300600000000"
  },
  ...
]
```

Returns transaction objects array by addresses.

### HTTP Request

`POST /tx/address`

### POST Parameters (JSON)

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | addresses | Array of WMCC Addresses
