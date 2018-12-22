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
{
  "wid": 1,
  "id": "my_wallet",
  "hash": "1a39a3727f12f89ec19cdd1504782b702e3127c5087567a66b6f352099b5304f",
  "height": 40698,
  "block": "0000000000079a5d7594d319ed5f0a038804f52c54bc2cc40d25bda08468d8a0",
  "time": 1520198647,
  "mtime": 1520198716,
  "date": "2018-03-04T21:24:07Z",
  "size": 236,
  "virtualSize": 209,
  "fee": 0,
  "rate": 0,
  "confirmations": 17,
  "inputs": [
    {
      "value": 0,
      "address": null,
      "path": null
    }
  ],
  "outputs": [
    {
      "value": 5000000000,
      "address": "wc1qsxwp9qgggez5p7t033t8kmm42gud0a7n5g8e7k",
      "path": {
        "name": "default",
        "account": 0,
        "change": false,
        "derivation": "m/0'/0/13"
      }
    },
    {
      "value": 500000000,
      "address": "WV17cxcpPmNNJYuFp7nkNoXJ75uZj11zTC",
      "path": null
    },
    {
      "value": 0,
      "address": null,
      "path": null
    }
  ],
  "tx": "010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2503fa9e00126d696e656420627920776d63635f7573657204dafae1af080000058aecd20400ffffffff0300f2052a01000000160014819c128108464540f96f8c567b6f755238d7f7d30065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000"
}
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
[
  ...
  {
    "wid": 1,
    "id": "my_wallet",
    "hash": "1a39a3727f12f89ec19cdd1504782b702e3127c5087567a66b6f352099b5304f",
    "height": 40698,
    "block": "0000000000079a5d7594d319ed5f0a038804f52c54bc2cc40d25bda08468d8a0",
    "time": 1520198647,
    "mtime": 1520198716,
    "date": "2018-03-04T21:24:07Z",
    "size": 236,
    "virtualSize": 209,
    "fee": 0,
    "rate": 0,
    "confirmations": 16,
    "inputs": [
      {
        "value": 0,
        "address": null,
        "path": null
      }
    ],
    "outputs": [
      {
        "value": 5000000000,
        "address": "wc1qsxwp9qgggez5p7t033t8kmm42gud0a7n5g8e7k",
        "path": {
          "name": "default",
          "account": 0,
          "change": false,
          "derivation": "m/0'/0/13"
        }
      },
      {
        "value": 500000000,
        "address": "WV17cxcpPmNNJYuFp7nkNoXJ75uZj11zTC",
        "path": null
      },
      {
        "value": 0,
        "address": null,
        "path": null
      }
    ],
    "tx": "010000000001010000000000000000000000000000000000000000000000000000000000000000ffffffff2503fa9e00126d696e656420627920776d63635f7573657204dafae1af080000058aecd20400ffffffff0300f2052a01000000160014819c128108464540f96f8c567b6f755238d7f7d30065cd1d000000001976a914456c9dc895ca8bc6e6bae8ca8f2a8a29018ca57d88ac0000000000000000266a24aa21a9ede2f61c3f71d1defd3fa999dfa36953755c690689799962b48bebd836974e8cf90120000000000000000000000000000000000000000000000000000000000000000000000000"
  },
  ...
]
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
<!--
> The above command returns JSON "result" like this:

```json
later
```
-->

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

Get range of wallet transactions by timestamp. Returns array of tx details.

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
