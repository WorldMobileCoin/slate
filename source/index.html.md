---
title: WMCC API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell--cURL: CURL
  - shell--CLI: CLI
  - javascript: Javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - node
  - rpc-node
  - rpc-chain
  - rpc-block
  - rpc-mempool
  - rpc-txn
  - rpc-mining
  - rpc-network
  - coin
  - transaction
  - wallet-admin
  - wallet
  - wallet-txn
  - wallet-account
  - wallet-event
  - error

search: true
history: true
---

# Introduction

Welcome to the WMCC API!

The default WMCC HTTP server listens on the standard RPC port `7880`.
It exposes a REST json api, as well as a JSON-RPC api.

# Authentication

## Auth

> To authorize, use this code:

```shell--cURL
curl http://x:[api-key]@127.0.0.1:7880/
```

```shell--CLI
export WMCC_API_KEY=[api-key]
wmcc cli info
```

```javascript
const Core = require('wmcc-core');
// http client
const client = new Core.http.Client({
  apiKey: [api-key],
  //...
});
// Or wallet
const wallet = new Core.http.Wallet({
  apiKey: [api-key],
  //...
});
```

> Make sure to replace `[api-key]` with your API key.

Auth is accomplished via HTTP Basic Auth, using your node's API key (passed via --api-key).

<aside class="notice">
You must replace `[api-key]` with your personal API key.
</aside>

<aside class="notice2">
If you intend to use API via network and setup `api-key`, make sure to setup `ssl` too.
</aside>

# Configuring Clients

## Default Listeners

```shell
# With curl you just send HTTP Requests based on further docs
# Only thing to have in mind is Authentication, which is described in Auth section.

curl http://127.0.0.1:7880/ # will get info from mainnet
```

By default API listens on this address:

Network | API Port
------- | --------
mainnet | 7880

You can interact with wmcc with REST Api as well as RPC, there are couple of ways you can use API.  

* `cURL` - You can use direct HTTP calls for invoking REST/RPC API calls.
* `CLI` - wmcc cli has almost all methods described to be used.
* `Javascript` - Clients used by `wmcc cli` can be used directly from javascript.

## Configuring WMCC CLI

```shell
# You can use config file
wmcc cli --config /full/path/to/wmcc.conf

# Or with prefix (which will later load wmcc.conf file from the directory)
wmcc cli --prefix /full/path/to/wmcc/dir

# You can configure it by passing arguments:
wmcc cli --network=mainnet info
wmcc cli info --network=mainnet

# Or use ENV variables (Starting with WMCC_)
export WMCC_NETWORK=mainnet
export WMCC_API_KEY=yoursecret
wmcc cli info
```

`wmcc cli` can be configured with many params:

### General configurations are:

Config | Options | Description
------ | ------- | -----------
prefix | dir path | This accepts directory where DBs and `wmcc.conf` are located.
network | `mainnet` | This will configure which network to load, also where to look for config file
uri, url | Base HTTP URI | This can be used for custom port
api-key | secret | Secret used by RPC for auth.

### Wallet Specific

Config | Options | Description
------ | ------- | -----------
id | primary, custom | specify which account to use by default
token | token str | Token specific wallet

<aside class="notice">
Some commands might accept additional parameters.
</aside>

## Using Javascript Client

```javascript--
const Core = require('wmcc-core');
const Client = Core.http.Client;
const Wallet = Core.http.Wallet;

const client = new Client({
  network: 'mainnet',
  uri: 'http://localhost:7880'
});

const wallet = new Wallet({
  network: 'mainnet',
  uri: 'http://localhost:7880',
  id: 'primary'
});
```

You can also use api with Javascript Library (used by `wmcc cli`). There are two objects: `Core.http.Client` for general API and `Core.http.Wallet` for wallet API.

`Core.http.Client` options:

Config | Type | Description
------ | ---- | -----------
network | mainnet | Network to use (doesn't lookup configs by itself)
uri | String | URI of the service
apiKey | String | api secret

`Core.http.Wallet` options:

Config | Type | Description
------ | ---- | -----------
network | mainnet | Network to use (doesn't lookup configs by itself)
uri | String | URI of the service
apiKey | String | api secret
id | primary, custom | specify which account to use by default
token | token str | Token specific wallet