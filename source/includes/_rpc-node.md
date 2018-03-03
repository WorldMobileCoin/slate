# RPC Calls - Node

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "method": "methodname", "params": [...] "id": "some-id" }'
```

```shell--CLI
wmcc cli rpc params...
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('MethodName', [ ...params ]);
  // RES will return "result" part of the object, not the id or error

})().catch((err) => {
  // error will be thrown.
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
{"result": resultObject ,"error": errorObject, "id": passedID}
```

> `Further examples` will only include "result" part.

WMCC RPC calls mimic Bitcoin Core's RPC. This is documentation how to use it with `wmcc-core`.

RPC Calls are accepted at: `POST /`

<aside class="notice">
Note: wmcc cli rpc and javascript will return error OR result.
</aside>

### POST Parameters RPC

Parameter | Description
--------- | -----------
method | Name of the RPC call
params | Parameters accepted by method
id | Will be returned with the response (Shouldn't be object)

## stop

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{ "method": "stop" }'
```

```shell--CLI
wmcc cli rpc stop
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('stop');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
"Stopping."
```

Stops the running node.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getinfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getinfo",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getinfo
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getinfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "version": "v1.0.0-beta.1",
  "protocolversion": 70015,
  "walletversion": 0,
  "balance": 0,
  "blocks": 38432,
  "timeoffset": 0,
  "connections": 28,
  "proxy": "",
  "difficulty": 689.0484608679707,
  "testnet": false,
  "keypoololdest": 0,
  "keypoolsize": 0,
  "unlocked_until": 0,
  "paytxfee": 0.001,
  "relayfee": 0.00001,
  "errors": ""
}
```

Returns general info.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getmemoryinfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getmemoryinfo",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getmemoryinfo
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getmemoryinfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "total": 62,
  "jsHeap": 16,
  "jsHeapTotal": 19,
  "nativeHeap": 42,
  "external": 62
}
```

Returns Memory usage info.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## setloglevel

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "setloglevel",
    "params": [ "none" ]
  }'
```

```shell--CLI
wmcc cli rpc setloglevel none
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('setloglevel', [ 'none' ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Change Log level of the running node.

Levels are: `NONE`, `ERROR`, `WARNING`, `INFO`, `DEBUG`, `SPAM`

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | level | Required | Level for the logger

## validateaddress

```shell--cURL
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "validateaddress",
    "params": [ "'$address'" ]
  }'
```

```shell--CLI
address='wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

wmcc cli rpc validateaddress $address
```

```javascript
const address = 'wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('validateaddress', [ address ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "isvalid": true,
  "address": "wc1qg0325qf07mysegu5qeuupf5zr38yrcsrkqhnav",
  "scriptPubKey": "001443e2aa012ff6c90ca3940679c0a6821c4e41e203",
  "ismine": false,
  "iswatchonly": false
}
```

Validates address.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | address | Required | Address to validate

## createmultisig

```shell--cURL
later
```

```shell--CLI
later
```

```javascript
later
```

> The above command returns JSON "result" like this:

```json
later
```

Create multisig address.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | nrequired | Required | Required number of approvals for spending
| 2 | keyArray | Required | Array of public keys

## createwitnessaddress

```shell--cURL
later
```

```shell--CLI
later
```

```javascript
later
```

> The above command returns JSON "result" like this:

```json
later
```

Creates witness address.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | script | Required | WMCC script.

## signmessagewithprivkey

```shell--cURL
later
```

```shell--CLI
later
```

```javascript
later
```

> The above command returns JSON "result" like this:

```json
later
```

Signs message with private key.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | privkey | Required | Private key
| 2 | message | Required | Message you want to sign.

## verifymessage

```shell--cURL
later
```

```shell--CLI
later
```

```javascript
later
```

> The above command returns JSON "result" like this:

```json
later
```

Verify a message.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | address | Required | Address of the signer
| 2 | signature | Required | Signature of signed message
| 3 | message | Required | Message that was signed

## setmocktime

```shell--cURL
timestamp=1519880400;

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "setmocktime",
    "params": [ '$timestamp' ]
  }'
```

```shell--CLI
timestamp=1519880400;

wmcc cli rpc setmocktime $timestamp
```

```javascript

const timestamp = 1519880400;

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('setmocktime', [ timestamp ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Changes network time (This is consensus-critical).

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | timestamp | Required | timestamp to change to
