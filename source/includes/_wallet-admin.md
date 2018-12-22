# Wallet Admin

The \_admin namespace exists to differentiate administrative level tasks on the wallet API that you probably don't want to expose to individual wallets.

`/wallet/_admin/[TARGET_ACTION]`

<aside class="notice3">
Replace <code>[TARGET_ACTION]</code> with one of the available actions listed below.
</aside>

## Wallet Rescan

```shell--cURL
height = 40000;

curl $url/wallet/_admin/rescan \
  -X POST \
  --data '{"height": '$height'}'
```

```shell--CLI
height = 40000;

wmcc cli rescan $height
```

```javascript
const height = 40000;

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.rescan(height);
})().catch((err) => {
  console.error(err.stack);
});
```

> Response Body:

```text
Rescanning...
```

Initiates a blockchain rescan for the walletdb. Wallets will be rolled back to the specified height (transactions above this height will be unconfirmed).

### HTTP Request

`POST /wallet/_admin/rescan`

### POST Parameters (JSON)

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | height | Height of block to start rescan

## Wallet Resend

```shell--cURL
curl $url/wallet/_admin/resend \
  -X POST
```

```shell--CLI
wmcc cli resend
```

```javascript
const height = 40000;

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.resend();
})().catch((err) => {
  console.error(err.stack);
});
```

> Response Body:

```text
Resending...
```

Rebroadcast all pending transactions in all wallets.

### HTTP Request

`POST /wallet/_admin/resend`

### POST Parameters (JSON)

| \# | Parameter | Description
| -- | --------- | -----------
| | None

## Wallet Backup

```shell--cURL
path='./backup/my_wallet.ldb';

curl $url/wallet/_admin/backup \
  -X POST \
  --data '{"path": "'$path'"}'
```

```shell--CLI
path='./backup/my_wallet.ldb';

wmcc cli backup $path
```

```javascript
const path = './backup/my_wallet.ldb';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.backup(path);
})().catch((err) => {
  console.error(err.stack);
});
```

> Response Body:

```text
Backup complete.
```

Safely backup the wallet database to specified path (creates a clone of the database).

### HTTP Request

`POST /wallet/_admin/backup`

### POST Parameters (JSON)

| \# | Parameter | Description
| :: | --------- | -----------
| 1 | path | Path to backup wallet database

## List all Wallets

```shell--cURL
curl $url/wallet/_admin/wallets
```

```shell--CLI
wmcc cli wallets
```

```javascript
const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  const wallets = await client.getWallets();

  console.log(wallets);
})().catch((err) => {
  console.error(err.stack);
});
```

> Response Body:

```json
[
  "my_wallet"
]
```

List all wallet IDs. Returns an array of strings.

### HTTP Request

`GET /wallet/_admin/wallets`