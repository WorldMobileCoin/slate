# RPC Calls - Transactions

## gettxout

```shell--cURL
txhash='2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158';
index=0;
includemempool=1;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "gettxout",
    "params": [ "'$txhash'", "'$index'", "'$includemempool'" ]
  }'
```

```shell--CLI
txhash='2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158';
index=0;
includemempool=1;

wmcc cli rpc gettxout $txhash $index $includemempool
```

```javascript
const txhash = '2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158';
const index = 0;
const includemempool = 1;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('gettxout', [ txhash, index, includemempool ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "bestblock": "00000000005dd7dc561adf5a45b424522ddb5d5d097cf786e3765d131c45d541",
  "confirmations": 27102,
  "value": 4.6761,
  "scriptPubKey": {
    "asm": "OP_0 fabd5c4234e13f6afcf5bb88d31778bd4a7501ef",
    "hex": "0014fabd5c4234e13f6afcf5bb88d31778bd4a7501ef",
    "type": "WITNESSPUBKEYHASH",
    "reqSigs": 1,
    "addresses": [
      "wc1ql274cs35uylk4l84hwydx9mch4982q006z9a6r"
    ]
  },
  "version": 1,
  "coinbase": false
}
```

Validates address.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | address | Required | Address to validate

## gettxoutsetinfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "gettxoutsetinfo",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc gettxoutsetinfo
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('gettxoutsetinfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "height": 38515,
  "bestblock": "0000000000302782c0835cad1da86e8c98c92cb05a0304d3b6b4ca62199f6a28",
  "transactions": 38670,
  "txouts": 71313,
  "bytes_serialized": 0,
  "hash_serialized": 0,
  "total_amount": 22118325
}
```

Returns information about UTXO's from Chain.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getrawtransaction

```shell--cURL
txhash='2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158';
verbose=0;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getrawtransaction",
    "params": [ "'$txhash'", "'$verbose'" ]
  }'
```

```shell--CLI
txhash='2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158';
verbose=0;

wmcc cli rpc getrawtransaction $txhash $verbose
```

```javascript
const txhash = '2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158';
const verbose = 0;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getrawtransaction', [ txhash, verbose ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
"010000000001013e1ac1713e83b89067f97b2b583dc88afc6dbd391dd9782a363be2d108bb62290000000000ffffffff029029df1b00000000160014fabd5c4234e13f6afcf5bb88d31778bd4a7501efc091260e010000001600145ead51bc8f6ba3536a2ac99a2f28c8ab9bbec383024730440220669783ecaffb8da8f9d2b09faa33240486570a1ca5091f9feb1d2f451e125a9602206c63013c292f2eb9a2a363b13f73f2f8d8035b81f4d3c83a51f1c171d693a17c012102db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd5044300600000000"
```

Returns raw transaction.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | txhash | Required | Transaction hash
| 2 | verbose | false | Returns json formatted if true

## decoderawtransaction

```shell--cURL
rawtx='010000000001013e1ac1713e83b89067f97b2b583dc88afc6dbd391dd9782a363be2d108bb62290000000000ffffffff029029df1b00000000160014fabd5c4234e13f6afcf5bb88d31778bd4a7501efc091260e010000001600145ead51bc8f6ba3536a2ac99a2f28c8ab9bbec383024730440220669783ecaffb8da8f9d2b09faa33240486570a1ca5091f9feb1d2f451e125a9602206c63013c292f2eb9a2a363b13f73f2f8d8035b81f4d3c83a51f1c171d693a17c012102db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd5044300600000000';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "decoderawtransaction",
    "params": [ "'$rawtx'" ]
  }'
```

```shell--CLI
rawtx='010000000001013e1ac1713e83b89067f97b2b583dc88afc6dbd391dd9782a363be2d108bb62290000000000ffffffff029029df1b00000000160014fabd5c4234e13f6afcf5bb88d31778bd4a7501efc091260e010000001600145ead51bc8f6ba3536a2ac99a2f28c8ab9bbec383024730440220669783ecaffb8da8f9d2b09faa33240486570a1ca5091f9feb1d2f451e125a9602206c63013c292f2eb9a2a363b13f73f2f8d8035b81f4d3c83a51f1c171d693a17c012102db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd5044300600000000';

wmcc cli rpc decoderawtransaction $rawtx
```

```javascript
const rawtx = '010000000001013e1ac1713e83b89067f97b2b583dc88afc6dbd391dd9782a363be2d108bb62290000000000ffffffff029029df1b00000000160014fabd5c4234e13f6afcf5bb88d31778bd4a7501efc091260e010000001600145ead51bc8f6ba3536a2ac99a2f28c8ab9bbec383024730440220669783ecaffb8da8f9d2b09faa33240486570a1ca5091f9feb1d2f451e125a9602206c63013c292f2eb9a2a363b13f73f2f8d8035b81f4d3c83a51f1c171d693a17c012102db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd5044300600000000';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('decoderawtransaction', [ rawtx ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "txid": "2784c844f46d162157244a39463df5ffb13fedf82cae601306afbad45a6aa158",
  "hash": "ec3f8bffc219ba76205567bdae14b352e292a90895b1ac131ac1129f94276dbf",
  "size": 222,
  "vsize": 141,
  "version": 1,
  "locktime": 0,
  "vin": [
    {
      "txid": "2962bb08d1e23b362a78d91d39bd6dfc8ac83d582b7bf96790b8833e71c11a3e",
      "scriptSig": {
        "asm": "",
        "hex": ""
      },
      "txinwitness": [
        "30440220669783ecaffb8da8f9d2b09faa33240486570a1ca5091f9feb1d2f451e125a9602206c63013c292f2eb9a2a363b13f73f2f8d8035b81f4d3c83a51f1c171d693a17c01",
        "02db24f4484b429ee9de01bc0e2d7a8d5945fafca8c8c986dd61eb49bd50443006"
      ],
      "sequence": 4294967295,
      "vout": 0
    }
  ],
  "vout": [
    {
      "value": 4.6761,
      "n": 0,
      "scriptPubKey": {
        "asm": "OP_0 fabd5c4234e13f6afcf5bb88d31778bd4a7501ef",
        "hex": "0014fabd5c4234e13f6afcf5bb88d31778bd4a7501ef",
        "type": "WITNESSPUBKEYHASH",
        "reqSigs": 1,
        "addresses": [
          "wc1ql274cs35uylk4l84hwydx9mch4982q006z9a6r"
        ]
      }
    },
    {
      "value": 45.32376,
      "n": 1,
      "scriptPubKey": {
        "asm": "OP_0 5ead51bc8f6ba3536a2ac99a2f28c8ab9bbec383",
        "hex": "00145ead51bc8f6ba3536a2ac99a2f28c8ab9bbec383",
        "type": "WITNESSPUBKEYHASH",
        "reqSigs": 1,
        "addresses": [
          "wc1qt6k4r0y0dw34x632exdz72xg4wdmasurll7j7u"
        ]
      }
    }
  ],
  "coinbase": false,
  "blockhash": null,
  "confirmations": 0,
  "time": 0,
  "blocktime": 0
}
```

Decodes raw transaction and provide chain info.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | rawtx | Required | Raw transaction hex

## decodescript

```shell--cURL
script='483045022100a00ee7b3f66cb730b1dcac558871add61fdd0b6505d074ff8750bf776893025002202091022864a5b9f1104c31f399e1855def6ac03cd1e981abe06b3bf5e7ec2143012102e054848255c88553a04cfae49c0bba95bf23243e61aa15e5a8c01cc918b19687';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "decodescript",
    "params": [ "'$script'" ]
  }'
```

```shell--CLI
script='483045022100a00ee7b3f66cb730b1dcac558871add61fdd0b6505d074ff8750bf776893025002202091022864a5b9f1104c31f399e1855def6ac03cd1e981abe06b3bf5e7ec2143012102e054848255c88553a04cfae49c0bba95bf23243e61aa15e5a8c01cc918b19687';

wmcc cli rpc decodescript $script
```

```javascript
const script='483045022100a00ee7b3f66cb730b1dcac558871add61fdd0b6505d074ff8750bf776893025002202091022864a5b9f1104c31f399e1855def6ac03cd1e981abe06b3bf5e7ec2143012102e054848255c88553a04cfae49c0bba95bf23243e61aa15e5a8c01cc918b19687';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('decodescript', [ script ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "asm": "3045022100a00ee7b3f66cb730b1dcac558871add61fdd0b6505d074ff8750bf776893025002202091022864a5b9f1104c31f399e1855def6ac03cd1e981abe06b3bf5e7ec214301 02e054848255c88553a04cfae49c0bba95bf23243e61aa15e5a8c01cc918b19687",
  "type": "NONSTANDARD",
  "reqSigs": 1,
  "addresses": [],
  "p2sh": "XCYUwwFSNj76UmQd2Hyrt1wTE499Q5xqv7"
}
```

Decodes raw transaction and provide chain info.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | script | Required | Script hex

## sendrawtransaction

```shell--cURL
rawtx='later';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "sendrawtransaction",
    "params": [ "'$rawtx'" ]
  }'
```

```shell--CLI
rawtx='later';

wmcc cli rpc sendrawtransaction $rawtx
```

```javascript
const rawtx = 'later';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('sendrawtransaction', [ rawtx ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Sends raw transaction without verification.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | rawtx | Required | Raw transaction hex

## createrawtransaction

```shell--cURL
txhash='later';
txindex=1;
amount=1;
address='later';
data='';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "createrawtransaction",
    "params": [
      [{ "txid": "'$txhash'", "vout": "'$txindex'" }],
      { "'$address'": "'$amount'", "data": "'$data'" }
    ]
  }'
```

```shell--CLI
txhash='later';
txindex=1;
amount=1;
address='later';
data='';

wmcc cli rpc createrawtransaction \
  '[{ "txid": "'$txhash'", "vout": "'$txindex'" }]' \
  '{ "'$address'": "'$amount'", "data": "'$data'" }'
```

```javascript
const txhash = 'later';
const txindex = 1;
const amount = 1;
const address = 'later';
const data = '';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const sendTo = {
    data: data
  };
  sendTo[address] = amount;
  const res = await rpc.execute('createrawtransaction', [ [{ txid: txhash, vout: txindex }], sendTo]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Creates raw, unsigned transaction without any formal verification.

<aside class="notice">
Transaction in example doesn't specify change output, you can do it by specifying another address: amount pair.
</aside>

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | outpoints | Required | Outpoint list
| *1.1* | *txid* |  | *Transaction Hash*
| *1.2* | *vout* |  | *Transaction Outpoint Index*
| *1.3* | *sequence* |  | *Sequence number for input*
| 2 | sendto | Required | List of addresses with amounts that we are sending to
| *2.1* | *address* | *0* | *`address: amount` key pairs*
| *2.2* | *data* | *nullData* | *Data output*
| 3 | locktime |  | Earliest time a transaction can be added

## signrawtransaction

```shell--cURL
rawtx='later';
txhash='later';
txindex=1;
scriptPubKey='later';
amount=1;
privkey='later';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "signrawtransaction",
    "params": [
      "'$rawtx'",
      [{
        "txid": "'$txhash'",
        "vout": "'$txindex'",
        "scriptPubKey": "'$scriptPubKey'",
        "amount": "'$amount'"
      }],
      [ "'$privkey'" ]
    ]
  }'
```

```shell--CLI
rawtx='later';
txhash='later';
txindex=1;
scriptPubKey='later';
amount=1;
privkey='later';

wmcc cli rpc signrawtransaction $rawtx \
  '[{ "txid": "'$txhash'", "vout": "'$txindex'", "scriptPubKey": "'$scriptPubKey'", "amount": "'$amount'" }]' \
  '[ "'$privkey'" ]'
```

```javascript
const rawtx = 'later';
const txhash = 'later';
const txindex = 1;
const scriptPubKey = 'later';
const amount = 1;
const privkey = 'later';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('signrawtransaction', [ rawtx,
    [{
      txid: txhash,
      vout: txindex,
      scriptPubKey: scriptPubKey,
      amount: amount
    }],
    [ privkey ]
  ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Signs raw transaction.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | rawtx | Required | Raw tx
| 2 | inputs | Required | Coins you're going to spend
| *2.1* | *txid* |  | *Transaction Hash*
| *2.2* | *vout* |  | *Transaction Outpoint Index*
| *2.3* | *scriptPubKey* |  | *Script with pubkey you are going to sign*
| *2.4* | *redeemScript* |  | *redeemScript if tx is P2SH*
| 3 | privkeylist |  | List of private keys
| 4 | sighashtype |  | Type of signature hash

## gettxoutproof

```shell--cURL
txhash='93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "gettxoutproof",
    "params": [ "'$txhash'" ]
  }'
```

```shell--CLI
txhash='93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';

wmcc cli rpc gettxoutproof $txhash
```

```javascript
const txhash = '93820db11708782c947fe2fe34830616bb6cec52f9a032cf18c7e0ae58e47385';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('gettxoutproof', [ txhash ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
"000000206235243ff1ef6c3dcfecb2654715256aa46cbe246513ee98d13c595bea0000008573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930c4e3f5afcff031ee6c7260001000000018573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930101"
```

Checks if transactions are within block. Returns raw block.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | txidlist | Required | Array of transaction hashes
| 2 | blockhash | Based on TX | Block hash

## verifytxoutproof

```shell--cURL
proof='000000206235243ff1ef6c3dcfecb2654715256aa46cbe246513ee98d13c595bea0000008573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930c4e3f5afcff031ee6c7260001000000018573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930101';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "verifytxoutproof",
    "params": [ "'$proof'" ]
  }'
```

```shell--CLI
proof='000000206235243ff1ef6c3dcfecb2654715256aa46cbe246513ee98d13c595bea0000008573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930c4e3f5afcff031ee6c7260001000000018573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930101';

wmcc cli rpc verifytxoutproof $proof
```

```javascript
const proof = '000000206235243ff1ef6c3dcfecb2654715256aa46cbe246513ee98d13c595bea0000008573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930c4e3f5afcff031ee6c7260001000000018573e458aee0c718cf32a0f952ec6cbb16068334fee27f942c780817b10d82930101';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('verifytxoutproof', [ proof ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[] later ** check this **
```

Checks the proof for transaction inclusion.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | proof | Required | Proof of transaction inclusion
