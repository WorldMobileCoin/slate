# RPC Calls - Chain

## pruneblockchain

```shell--cURL
curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "pruneblockchain",
    "params": []
  }'
```

```shell--CLI
wmcc cli rpc pruneblockchain
```

```javascript
const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('pruneblockchain');

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
null
```

Prunes the blockchain, it will keep blocks specified in Network Configurations.

### Default Prune Options

Network | keepBlocks | pruneAfter
------- | ---------- | ----------
main | 288 | 1000

### Params

| \# | Name | Default | Description
| -- | ---- | ------- | -----------
| | | None

## invalidateblock

```shell--cURL
blockhash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "invalidateblock",
    "params": [ "'$blockhash'" ]
  }'
```

```shell--CLI
blockhash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';

wmcc cli rpc invalidateblock $blockhash
```

```javascript
const blockhash = '00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('invalidateblock', [ blockhash ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
null
```

Invalidates the block in the chain. It will rewind network to blockhash and invalidate it.

It won't accept that block as valid *Invalidation will work while running, restarting node will remove invalid block from list.*

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockhash | Required | Block's hash

## reconsiderblock

```shell--cURL
blockhash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';

curl $url/ \
  -H 'Content-Type: application/json' \
  -X POST \
  --data '{
    "method": "reconsiderblock",
    "params": [ "'$blockhash'" ]
  }'
```

```shell--CLI
blockhash='00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';

wmcc cli rpc reconsiderblock $blockhash
```

```javascript
const blockhash = '00000f010aabd27b067361a8d8bde8dc320ccb237c17797028eb41b00e7dca38';

const rpc = new Core.http.RPCClient({
  network: 'mainnet'
});

(async () => {
  const res = await rpc.execute('reconsiderblock', [ blockhash ]);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON structured like this:

```json
null
```

This rpc command will remove block from invalid block set.

### Params

| \# | Name | Default | Description
| :: | ---- | ------- | -----------
| 1 | blockhash | Required | Block's hash
