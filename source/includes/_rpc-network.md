# RPC Calls - Network

## getconnectioncount

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getconnectioncount",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getconnectioncount
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getconnectioncount');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
16
```

Returns connection count.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## ping

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "ping",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc ping
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('ping');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Will send ping request to every connected peer.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getpeerinfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getpeerinfo",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getpeerinfo
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getpeerinfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  {
    "id": 55852,
    "addr": "172.245.190.73:8880",
    "addrlocal": "115.164.177.220:2334",
    "services": "00000009",
    "relaytxes": true,
    "lastsend": 1520053635,
    "lastrecv": 1520053635,
    "bytessent": 25016,
    "bytesrecv": 34335,
    "conntime": 401,
    "timeoffset": 51,
    "pingtime": 0.234,
    "minping": 0.234,
    "version": 70015,
    "subver": "/wmcc:v1.0.0-beta.1/",
    "inbound": false,
    "startingheight": 40406,
    "besthash": "00000000000d53383bf2c2e8eaeaf79a73a3cd51b7b0ea36f6839c2e86ed89d2",
    "bestheight": 40407,
    "banscore": 0,
    "inflight": [],
    "whitelisted": false
  },
  ...
]
```

Returns information about all connected peers.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## addnode

```shell--cURL
nodeAddr='172.245.190.68:8880';
cmd='add';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "addnode",
    "params": [ "'$nodeAddr'", "'$cmd'" ]
  }'
```

```shell--CLI
nodeAddr='172.245.190.68:8880';
cmd='add';

wmcc cli rpc addnode $nodeAddr $cmd
```

```javascript
const nodeAddr = '172.245.190.68:8880';
const cmd = 'add';

const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('addnode', [ nodeAddr, cmd ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Adds or removes peers in Host List.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | addr | Required | IP Address (port) of the Node
| 2 | cmd | Required | Command

### Commands

| \# | Command | Description
| :: | ---- | -------
| 1 | add | Adds node to Host List and connects to it
| 2 | onetry | Tries to connect to the given node
| 3 | remove | Removes node from host list

## disconnectnode

```shell--cURL
nodeAddr='172.245.190.68:8880';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "disconnectnode",
    "params": [ "'$nodeAddr'" ]
  }'
```

```shell--CLI
nodeAddr='172.245.190.68:8880';

wmcc cli rpc disconnectnode $nodeAddr
```

```javascript
const nodeAddr = '172.245.190.68:8880';

const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('disconnectnode', [ nodeAddr ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Disconnects node.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | addr | Required | IP Address of the Node

## getaddednodeinfo

```shell--cURL
nodeAddr='172.245.190.68:8880';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getaddednodeinfo",
    "params": [ "'$nodeAddr'" ]
  }'
```

```shell--CLI
nodeAddr='172.245.190.68:8880';

wmcc cli rpc getaddednodeinfo $nodeAddr
```

```javascript
const nodeAddr = '172.245.190.68:8880';

const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getaddednodeinfo', [ nodeAddr ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  {
    "addednode": "172.245.190.68:8880",
    "connected": true,
    "addresses": [
      {
        "address": "172.245.190.68:8880",
        "connected": "outbound"
      }
    ]
  }
]
```

Returns node information from host list.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | addr | Required | IP Address (port) of the Node

## getnettotals

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getnettotals",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getnettotals
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getnettotals');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "totalbytesrecv": 94851,
  "totalbytessent": 56241,
  "timemillis": 1520054570343
}
```

Returns information about used network resources.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## getnetworkinfo

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "getnetworkinfo",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc getnetworkinfo
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('getnetworkinfo');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "version": "v1.0.0-beta.1",
  "subversion": "/wmcc:v1.0.0-beta.1/",
  "protocolversion": 70015,
  "localservices": "00000009",
  "localrelay": true,
  "timeoffset": 0,
  "networkactive": true,
  "connections": 32,
  "networks": [],
  "relayfee": 0.00001,
  "incrementalfee": 0,
  "localaddresses": [
    {
      "address": "115.164.177.220",
      "port": 8880,
      "score": 3
    }
  ],
  "warnings": ""
}
```

Returns local node's network information.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## setban

```shell--cURL
nodeAddr='172.245.190.68:8880';
cmd='add';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "setban",
    "params": [ "'$nodeAddr'", "'$cmd'" ]
  }'
```

```shell--CLI
nodeAddr='172.245.190.68:8880';
cmd='add';

wmcc cli rpc setban $nodeAddr $cmd
```

```javascript
const nodeAddr = '172.245.190.68:8880';
const cmd = 'add';

const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('setban', [ nodeAddr, cmd ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Adds or removes nodes from banlist.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | addr | Required | IP Address (port) of the Node
| 2 | cmd | Required | Command

### Commands

| \# | Command | Description
| :: | ---- | -------
| 1 | add | Adds node to ban list, removes from host list, disconnects
| 2 | remove | Removes node from ban list

## listbanned

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "listbanned",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc listbanned
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('listbanned');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
[
  {
    "address": "172.245.190.68",
    "banned_until": 1520141477,
    "ban_created": 1520055077,
    "ban_reason": ""
  },
  ...
]
```

Lists all banned peers.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## clearbanned

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "clearbanned",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc clearbanned
```

```javascript
const rpc = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('clearbanned');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
null
```

Removes all banned peers.

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None
