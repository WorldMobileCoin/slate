# Wallet Accounts

## Account Object

> An account object looks like this:

```json
later

```

Account belonging to a Wallet.

<aside class="notice">
This object does not enforce locks. Any method that does a write is internal API only and will lead to race conditions if used elsewhere.
</aside>

## Get Wallet Account List

```shell--cURL
id='my_wallet';

curl $url/wallet/$id/account
```

```shell--CLI
id='my_wallet';

wmcc cli wallet account list --id=$id
```

```javascript
const id = 'my_wallet';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();
  const info = await client.getAccounts(id);

  console.log(info);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

List all account names (array indices map directly to bip44 account indices) associated with a specific wallet id.

<aside class="notice">
Command defaults to primary (default) wallet if no wallet id is passed
</aside>

### HTTP Request

`GET /wallet/:id/account`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet you would like to retrieve the account list for

## Get Account Information

```shell--cURL
id='my_wallet';
account='default';

curl $url/wallet/$id/account/$account
```

```shell--CLI
id='my_wallet';

wmcc cli wallet --id=$id account get $account
```

```javascript
const id = 'my_wallet';
const account = 'default';

const client = new Core.http.Client({
  network: 'mainnet'
});

(async () => {
  await client.open();
  const info = await client.getAccount(id, account);

  console.log(info);

  await client.close();
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Get account info.

### HTTP Request

`GET /wallet/:id/account/:account`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet you would like to query
| 2 | account | string | Id of account you would to retrieve information for

## Create new wallet account

```shell--cURL
id='my_wallet';
account='new_account';
type='multisig';

curl $url/wallet/$id/account/$name \
  -X PUT \
  --data '{"type": "'$type"}'
```

```shell--CLI
id='my_wallet';
account='new_account';
type='multisig';

wmcc cli wallet --id=$id account create $name --type=$type --key=$accountKey
```

```javascript
const id = 'my_wallet';
const account = 'default';
const type = 'multisig';

const httpWallet = new Core.http.Wallet({
  id: id
});

const options = {type: type};

(async () => {
  const acc = await httpWallet.createAccount(account, options);

  console.log(acc);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
later
```

Create account with specified account name.

### HTTP Request

`PUT /wallet/:id/account/:name`

### Request Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | id | string | Id of wallet you would like to query
| 2 | account | string | Name of account you would to create

### Options Parameters

| \# | Parameter | Type | Description
| :: | --------- | ---- | -----------
| 1 | witness | bool | Whether or not to act as segregated witness wallet account
| 2 | accountKey | string | The extended public key for the account. This is ignored for non watch only wallets. Watch only accounts can't accept private keys for import (or sign transactions)
| 3 | type | string | Type of key for that account ('multisig', 'pubkeyhash')
| 4 | m | int | For multisig accounts, the `m` value in m-of-n
| 5 | n | int | For multisig accounts, the `n` value in in m-of-n
