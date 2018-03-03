# Wallet Transactions

## Get Wallet TX Details

```shell--cURL
id="my_wallet";
hash="later";

curl $url/wallet/$id/tx/$hash
```

```shell--CLI
id="my_wallet";
hash="later";

wmcc cli wallet --id=$id tx $hash
```

```javascript
const id = "my_wallet";
const hash = "later";

const httpWallet = new Core.http.Wallet({
  id: id
});

(async () => {
  const res = await httpWallet.getTX(hash);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Get wallet transaction details.

### HTTP Request

`GET /wallet/:id/tx/:hash`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet that handled the transaction
| 2 | hash | string | Hash of the transaction to retrieve

## Delete Transaction

```shell--cURL
id="my_wallet";
hash="later";
passphrase="later";

curl $url/wallet/$id/tx/$hash \
  -X DELETE \
  --data '{"passphrase": "'$passphrase'"}'
```

```shell--CLI
# Not available in CLI
```

```javascript
// Not available in javascript wallet client.
```

Abandon single pending transaction. Confirmed transactions will throw an error. `"TX not eligible"`

### HTTP Request

`DEL /wallet/:id/tx/:hash`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet where the transaction is that you want to remove
| 2 | hash | string | Hash of transaction you would like to remove

## Get Wallet TX History

```shell--cURL
id="my_wallet";

curl $url/wallet/$id/tx/history
```

```shell--CLI
id="my_wallet";

wmcc cli wallet --id=$id history
```

```javascript
const id = "my_wallet";
const account = 'default';

const httpWallet = new Core.http.Wallet({
  id: id
});

(async () => {
  const res = await httpWallet.getHistory(account);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Get wallet TX history. Returns array of tx details.

### HTTP Request

`GET /wallet/:id/tx/history`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet to get history of

## Get Pending Transactions

```shell--cURL
id="my_wallet";

curl $url/wallet/$id/tx/unconfirmed
```

```shell--CLI
id="my_wallet";

wmcc cli wallet --id=$id pending
```

```javascript
const id = "my_wallet";
const account = 'default';

const httpWallet = new Core.http.Wallet({
  id: id
});

(async () => {
  const res = await httpWallet.getPending(account);

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Get pending wallet transactions. Returns array of tx details.

### HTTP Request

`GET /wallet/:id/tx/unconfirmed`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet to get pending/unconfirmed txs

## Get Range of Transactions

```shell--cURL
id="my_wallet";
account="default";
start=later;
end=later;

curl $url/wallet/$id/tx/range?account=$account&start=$start&end=$end
```

```shell--CLI
# Range not available in CLI yet
```

```javascript
const id = "my_wallet";
const account = "default";
const start = later;
const end = later;

const httpWallet = new Core.http.Wallet({
  id: id
});

(async () => {
  const res = await httpWallet.getRange(account, {start: start, end: end});

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

<aside class="notice">
There are other options documented that <code>getRange</code> accepts in the options body, <code>limit</code> and <code>reverse</code>
</aside>

### HTTP Request

`GET /wallet/:id/tx/range`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet to get history from

### Body Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | account | string | Account to get the tx history from
| 2 | start | int | Start time to get range from
| 3 | end | int | End time to get range from
