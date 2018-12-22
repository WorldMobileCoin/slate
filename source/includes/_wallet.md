# Wallet

```shell--cURL
id='my_wallet';
url="http://localhost:7880";

curl $url/wallet/$id/
```

```shell--CLI
id='my_wallet';

wmcc cli wallet get --id=$id
```

```javascript
const id = 'my_wallet';

const httpWallet = new Core.http.Wallet({
  id: id
});

(async () => {
  const res = await httpWallet.getInfo();

  console.log(res);
})().catch((err) => {
  console.error(err.stack);
});
```

> The above command returns JSON "result" like this:

```json
{
  "network": "mainnet",
  "wid": 1,
  "id": "my_wallet",
  "initialized": true,
  "watchOnly": false,
  "accountDepth": 1,
  "token": "42b117673f5022b89965e93fe0269402e7282eed330f413f22ca2b75db4b7d7d",
  "tokenDepth": 0,
  "lock": "1a497f236d54507a4d757431205f3d6c04231a4e1c11697d7d6e367c0b261d1969",
  "chksum": "37021e7e",
  "state": {
    "tx": 1,
    "coin": 1,
    "unconfirmed": 5000000000,
    "confirmed": 5000000000
  },
  "master": {
    "encrypted": true,
    "until": 0,
    "iv": "f43d54bcb946bbe0a37eadf85a2918db",
    "algorithm": "pbkdf2",
    "N": 50000,
    "r": 0,
    "p": 0
  },
  "account": {
    "name": "default",
    "initialized": true,
    "witness": true,
    "watchOnly": false,
    "type": "pubkeyhash",
    "m": 1,
    "n": 1,
    "accountIndex": 0,
    "receiveDepth": 15,
    "changeDepth": 1,
    "nestedDepth": 1,
    "lookahead": 0,
    "receiveAddress": "wc1qxd72nvknaumlrux8nzsqhm2zgxx5u9w0uamxur",
    "nestedAddress": "XHkZVbxqfvjHkh7DqUC537Kp3xE5LYzjex",
    "changeAddress": "wc1qgc3ear4vddvjypcupympm2s2rcupxk8c4wqemf",
    "accountKey": "xpub6CB49PLkxvx8iL8YK3a5NrL8H5LQvPxoPXyoTvEy2aWfw3XquUgcDjhXs4mXrxZNgMevdaY3xMkPXDd2fgX3Nw6uyGXxamyFdazJ565xJ76",
    "keys": []
  }
}
```

`wmcc-core` maintains a wallet database which contains every wallet. Wallets are not usable without also using a wallet database. Wallets are uniquely identified by an id and the walletdb is created with a default id of primary. (See [Create a Wallet](#create-a-wallet) below for more details.)

Wallets in wmcc use bip44. They also originally supported bip45 for multisig, but support was removed to reduce code complexity, and also because bip45 doesn't seem to add any benefit in practice.

The wallet database can contain many different wallets, with many different accounts, with many different addresses for each account. WMCC should theoretically be able to scale to hundreds of thousands of wallets/accounts/addresses.

Each account can be of a different type. You could have a pubkeyhash account, as well as a multisig account, a witness pubkeyhash account, etc.

Note that accounts should not be accessed directly from the public API. They do not have locks which can lead to race conditions during writes.

## Wallet Options

> Wallet options object will look something like this:

```json
{
  "id": "walletId",
  "witness": true,
  "watchOnly": false,
  "accountKey": "tpubDDRH1rj7ut9ZjcGakR9VGgXU8zYSZypLtMr7Aq6CZaBVBrCaMEHPzye6ZZbUpS8YmroLfVp2pPmCdaKtRdCuTCK2HXzwqWX3bMRj3viPMZo",
  "accountIndex": 1,
  "type": "pubkeyhash"
  "m": 1,
  "n": 1,
  "keys": [],
  "mnemonic": 'differ fantasy trigger priso remove sun undo arm fine sheriff sight mountainn'
}
```

Options are used for wallet creation. None are required.

### Options Object

| \# | Name | Type | Default | Description
| :: | ---- | ---- | ------- | -----------
| 1 | id | String |  | Wallet ID (used for storage)
| 2 | master | HDPrivateKey |  | Master HD key. If not present, it will be generated
| 3 | witness | Boolean | false | Whether to use witness programs
| 4 | watchOnly | Boolean | false | Watch only wallet
| 5 | accountKey | String |  | The extended public key for the primary account in the new wallet. This value is ignored if watchOnly is false
| 6 | accountIndex | Number | 0 | The BIP44 account index
| 7 | receiveDepth | Number |  | The index of the next receiving address
| 8 | changeDepth | Number |  | The index of the next change address
| 9 | type | String | 'pubkeyhash' | Type of wallet (pubkeyhash, multisig)
| 10 | compressed | Boolean | true | Whether to use compressed public keys
| 11 | m | Number | 1 | m value for multisig (m-of-n)
| 12 | n | Number | 1 | n value for multisig (m-of-n)
| 13 | mnemonic | String |  | A mnemonic phrase to use to instantiate an hd private key. One will be generated if none provided