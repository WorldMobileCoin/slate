# Coin

Getting `coin` information via API.

<aside class="notice2">
Coin stands for UTXO*
</aside>

<aside class="notice3">
You need to enable <code>index-address</code> in order to lookup coins by address(es).
</aside>

## Get coin by Outpoint

<aside class="notice">
This API call is always available regardless indexing options.
</aside>

```shell--cURL
hash='93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';
index=0;

curl $url/coin/$hash/$index
```

```shell--CLI
hash='93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';
index=0;

wmcc cli coin $hash $index
```

```javascript
const hash = '93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';
const index = 0;

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();

  const coin = await client.getCoin(hash, index);

  console.log(coin);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "version": 1,
  "height": 3000,
  "value": 5000000000,
  "script": "00141e8adf6f166aceec5fc65080aa1f88a3a260dd10",
  "address": "wc1qr69d7mckdt8wch7x2zq258ug5w3xphgs2sxpwg",
  "coinbase": true,
  "hash": "93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385",
  "index": 0
}
```

Get coin by outpoint (hash and index). Returns coin in wmcc coin json format.

### HTTP Request

`GET /coin/:hash/:index`

### URL Parameters

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | hash | Hash of tx
| 2 | index | Output's index in tx

## Get coins by address

```shell--cURL
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

curl $url/coin/address/$address
```

```shell--CLI
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

wmcc cli coin $address
```

```javascript
const address = 'wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();

  const coins = await client.getCoinsByAddress(address);

  console.log(coins);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  {
    "version": 1,
    "height": 11508,
    "value": 4532376000,
    "script": "001443e2aa012ff6c90ca3940679c0a6821c4e41e203",
    "address": "wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav",
    "coinbase": false,
    "hash": "1f99f3ea4e8f97428520436d63fc1f2f9a46e052d6cf798ba70881c76f016473",
    "index": 1
  },
  ...
]
```

Get coin objects array by address.

### HTTP Request

`GET /coin/address/:address`

### URL Parameters

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | address | WMCC Address

## Get coins by addresses

```shell--cURL
address0='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';
address1='wc1qp5mqu3axakk7rnv3egpacnh4a4pm9mm33p0pag';

curl $url/coin/address \
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

  const coins = await client.getCoinsByAddresses([address0, address1]);

  console.log(coins);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  {
    "version": 1,
    "height": 11508,
    "value": 4532376000,
    "script": "001443e2aa012ff6c90ca3940679c0a6821c4e41e203",
    "address": "wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav",
    "coinbase": false,
    "hash": "1f99f3ea4e8f97428520436d63fc1f2f9a46e052d6cf798ba70881c76f016473",
    "index": 1
  },
  {
    "version": 1,
    "height": 11218,
    "value": 4899986000,
    "script": "00140d360e47a6edade1cd91ca03dc4ef5ed43b2ef71",
    "address": "wc1qp5mqu3axakk7rnv3egpacnh4a4pm9mm33p0pag",
    "coinbase": false,
    "hash": "98c2faba6ad99ada7dca6f5fafed6cc52e6a63d63695015bd89d4b35a6b6e7e0",
    "index": 1
  }
]
```

Get coins by addresses, returns array of coin objects.

### HTTP Request

`POST /coin/address`

### POST Parameters (JSON)

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | addresses | Array of WMCC Addresses
