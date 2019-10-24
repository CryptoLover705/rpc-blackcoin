# rpc-bitcoin [![Build Status](https://travis-ci.com/vansergen/rpc-bitcoin.svg?token=cg5dVMovG8Db6p5Qzzps&branch=master)](https://travis-ci.com/vansergen/rpc-bitcoin)

A [TypeScript](https://www.typescriptlang.org) library to make RPC and HTTP REST requests to [Bitcoin Core](https://bitcoin.org/en/bitcoin-core/).

## Installation

```bash
npm install rpc-bitcoin
```

## [RPC](https://bitcoin.org/en/developer-reference#remote-procedure-calls-rpcs)

```javascript
const { RPCClient } = require("rpc-bitcoin");
const url = "http://192.168.0.10";
const user = "rpcuser";
const pass = "rpcpassword";
const port = 18832;
const timeout = 10000;
const client = new RPCClient({ url, port, timeout, user, pass });
```

- batch

```javascript
const response = await client.batch([
  { method: "getbestblockhash", id: 1 },
  { method: "help", params: { command: "help" }, id: "custom-id" },
  { method: "getzmqnotifications", params: {}, id: 2 }
]);
```

### Blockchain

- [`getbestblockhash`](https://bitcoin.org/en/developer-reference#getbestblockhash)

```javascript
const hex = await client.getbestblockhash();
```

- [`getblock`](https://bitcoin.org/en/developer-reference#getblock)

```javascript
const blockhash =
  "000000004182034f427d463b92162d35d0accef9ea0c5354a87e870ca1815b4c";
const verbosity = 2;
const block = await client.getblock({ blockhash, verbosity });
```

- [`getblockchaininfo`](https://bitcoin.org/en/developer-reference#getblockchaininfo)

```javascript
const info = await client.getblockchaininfo();
```

- [`getblockcount`](https://bitcoin.org/en/developer-reference#getblockcount)

```javascript
const count = await client.getblockcount();
```

- [`getblockhash`](https://bitcoin.org/en/developer-reference#getblockhash)

```javascript
const height = 1583782;
const hash = await client.getblockhash({ height });
```

- [`getblockheader`](https://bitcoin.org/en/developer-reference#getblockheader)

```javascript
const blockhash =
  "000000004182034f427d463b92162d35d0accef9ea0c5354a87e870ca1815b4c";
const verbose = false;
const header = await client.getblockheader({ blockhash, verbose });
```

- [`getblockstats`](https://bitcoin.org/en/developer-reference#getblockstats)

```javascript
const hash_or_height =
  "000000004182034f427d463b92162d35d0accef9ea0c5354a87e870ca1815b4c";
const stats = ["txs", "time"];
const info = await client.getblockstats({ hash_or_height, stats });
```

- [`getchaintips`](https://bitcoin.org/en/developer-reference#getchaintips)

```javascript
const tips = await client.getchaintips();
```

- [`getchaintxstats`](https://bitcoin.org/en/developer-reference#getchaintxstats)

```javascript
const nblocks = 2016;
const blockhash =
  "000000004182034f427d463b92162d35d0accef9ea0c5354a87e870ca1815b4c";
const result = await client.getchaintxstats({ nblocks, blockhash });
```

- [`getdifficulty`](https://bitcoin.org/en/developer-reference#getdifficulty)

```javascript
const difficulty = await client.getdifficulty();
```

- [`getmempoolancestors`](https://bitcoin.org/en/developer-reference#getmempoolancestors)

```javascript
const verbose = true;
const txid = "3e128c38f35520d4121d582f15998b7f74b44f17aa650b4d60decf975e642b9a";
const result = await client.getmempoolancestors({ txid, verbose });
```

- [`getmempooldescendants`](https://bitcoin.org/en/developer-reference#getmempooldescendants)

```javascript
const verbose = true;
const txid = "ff758ffd73729be8afae0d683547f7840bdaee75ad5e5c464fb621b2509c366b";
const result = await client.getmempooldescendants({ txid, verbose });
```

- [`getmempoolentry`](https://bitcoin.org/en/developer-reference#getmempoolentry)

```javascript
const txid = "0629e01f05088728b089715f247de82a160428c06d6c85484adab2aa66574ace";
const result = await client.getmempoolentry({ txid });
```

- [`getmempoolinfo`](https://bitcoin.org/en/developer-reference#getmempoolinfo)

```javascript
const info = await client.getmempoolinfo();
```

- [`getrawmempool`](https://bitcoin.org/en/developer-reference#getrawmempool)

```javascript
const verbose = true;
const result = await client.getrawmempool({ verbose });
```

- [`gettxout`](https://bitcoin.org/en/developer-reference#gettxout)

```javascript
const txid = "d2f6b1d1844e483ce350a4a22fbaef36c31ebe88730415b7408c1f34b834fab5";
const n = 1;
const include_mempool = true;
const result = await client.gettxout({ txid, n, include_mempool });
```

- [`gettxoutproof`](https://bitcoin.org/en/developer-reference#gettxoutproof)

```javascript
const txids = [
  "42e75d074cf5b836170d20fc09593245c65a3f07283a497c3350c4d109b38bb6"
];
const blockhash =
  "000000000000000000055bc30b762904ab996430603cafe846cc6adc82c4af1e";
const result = await client.gettxoutproof({ txids, blockhash });
```

- [`gettxoutsetinfo`](https://bitcoin.org/en/developer-reference#gettxoutsetinfo)

```javascript
const info = await client.gettxoutsetinfo();
```

- [`preciousblock`](https://bitcoin.org/en/developer-reference#preciousblock)

```javascript
const blockhash =
  "00000000000000261a35cf378bf8fa1bf6ac87800d798ce2a11f581f562e92ba";
const result = await client.preciousblock({ blockhash });
```

- [`pruneblockchain`](https://bitcoin.org/en/developer-reference#pruneblockchain)

```javascript
const height = 1000;
const result = await client.pruneblockchain({ height });
```

- [`savemempool`](https://bitcoin.org/en/developer-reference#savemempool)

```javascript
const result = await client.savemempool();
```

- [`scantxoutset`](https://bitcoin.org/en/developer-reference#scantxoutset)

```javascript
const action = "start";
const scanobjects = [
  "addr(mxosQ4CvQR8ipfWdRktyB3u16tauEdamGc)",
  {
    desc:
      "wpkh([d34db33f/84'/0'/0']tpubD6NzVbkrYhZ4YTN7usjEzYmfu4JKqnfp9RCbDmdKH78vTyuwgQat8vRw5cX1YaZZvFfQrkHrM2XsyfA8cZE1thA3guTBfTkKqbhCDpcKFLG/0/*)#8gfuh6ex",
    range: [1, 3]
  }
];
const result = await client.scantxoutset({ action, scanobjects });
```

- [`verifychain`](https://bitcoin.org/en/developer-reference#verifychain)

```javascript
const checklevel = 1;
const nblocks = 10;
const result = await client.verifychain({ checklevel, nblocks });
```

- [`verifytxoutproof`](https://bitcoin.org/en/developer-reference#verifytxoutproof)

```javascript
const proof =
  "00000020ed07b12f0398e45fd403db11dbe894dc3301ce1a7725424e0b5e460c0000000066fca14db436f305aea37b3ae0f8b188cbf112dff3854c3d419f3ff3ebbc821f6c0c975dffff001d8fd5a7d2eb00000009e7acd3f605d1b957d684d9eeca9c472d803d90c0d17e29e5606f9b080b177a4abcd854622ad3900b5bc1ae71e99699a05eb972d46bd439c08eb7fbd20bba6494542222b2d1388f52c6d23ac12b32245ca47b02fc2f0a283a88aabca1f4db43ca8a4da8ffd7d9ae403b0c34ccbf14d2318c34fabb713c48f6d6490c6095250b6f08f26f020275d448dfb9967c62bedefaf29260021671a191f620f7783252788549b1e033dc815e2cd36ff204b398046f834643859f881a4d93b3fc5b91413a009c5069be274e1dcc675183ea2a989ef598422c0ed02e407aade8eaa6ef7ec1120ca4ffdef21b5fd26c4525a27c78cc38026b257f9d23f0d796603b1d3cbf539bdf87ccf9e81954f58e072d67eff2891339f203cbdec68bbbabbbbc0c070cceea03bf0a00";
const result = await client.verifytxoutproof({ proof });
```

### Control

- [`getmemoryinfo`](https://bitcoin.org/en/developer-reference#getmemoryinfo)

```javascript
const mode = "mallocinfo";
const result = await client.getmemoryinfo({ mode });
```

- [`getrpcinfo`](https://bitcoin.org/en/developer-reference#getrpcinfo)

```javascript
const result = await client.getrpcinfo();
```

- [`help`](https://bitcoin.org/en/developer-reference#help)

```javascript
const command = "getzmqnotifications";
const result = await client.help({ command });
```

- [`logging`](https://bitcoin.org/en/developer-reference#logging)

```javascript
const include = ["net", "rpc"];
const exclude = ["mempoolrej", "estimatefee"];
const result = await client.logging({ include, exclude });
```

- [`stop`](https://bitcoin.org/en/developer-reference#stop)

```javascript
const result = await client.stop();
```

- [`uptime`](https://bitcoin.org/en/developer-reference#uptime)

```javascript
const result = await client.uptime();
```

### ZMQ

- [`getzmqnotifications`](https://bitcoincore.org/en/doc/0.17.0/rpc/zmq/getzmqnotifications/)

```javascript
const result = await client.getzmqnotifications();
```

## [HTTP REST](https://bitcoin.org/en/developer-reference#http-rest)

```javascript
const { RESTClient } = require("rpc-bitcoin");
const url = "http://192.168.0.101";
const port = 17230;
const timeout = 20000;
const restClient = new RESTClient({ url, port, timeout });
```

- [getBlock](https://bitcoin.org/en/developer-reference#get-block)

```javascript
const hash = "00000000099de420b319c7804c4bfee5357d3f5ddbfd3c71c15b3625347792bf";
const format = "hex";
await restClient.getBlock({ hash, format });
```

- [getBlockNoTxDetails](https://bitcoin.org/en/developer-reference#get-blocknotxdetails)

```javascript
const hash = "00000000099de420b319c7804c4bfee5357d3f5ddbfd3c71c15b3625347792bf";
const format = "hex";
await restClient.getBlockNoTxDetails({ hash, format });
```

- [getBlockHashByHeight](https://bitcoin.org/en/developer-reference#get-blockhashbyheight)

```javascript
const height = 1;
const format = "hex";
await restClient.getBlockHashByHeight({ height, format });
```

- [getChainInfo](https://bitcoin.org/en/developer-reference#get-chaininfo)

```javascript
await restClient.getChainInfo();
```

- [getUtxos](https://bitcoin.org/en/developer-reference#get-getutxos)

```javascript
const checkmempool = true;
const outpoints = [
  {
    txid: "e346be6c1ef4d24f3a26ea8e1b45a2645d339fbee9da8b9dc03aeef1c4179716",
    n: 0
  },
  {
    txid: "e346be6c1ef4d24f3a26ea8e1b45a2645d339fbee9da8b9dc03aeef1c4179716",
    n: 1
  }
];
const format = "hex";
await restClient.getUtxos({ checkmempool, outpoints, format });
```

- [getHeaders](https://bitcoin.org/en/developer-reference#get-headers)

```javascript
const count = 5;
const hash = "00000000000001f0be142e57e99d3528212e1204157209c6c10bd11326cc5b35";
const format = "hex";
await restClient.getHeaders({ count, hash, format });
```

- [getMemPoolContents](https://bitcoin.org/en/developer-reference#get-mempoolcontents)

```javascript
await restClient.getMemPoolContents();
```

- [getMemPoolInfo](https://bitcoin.org/en/developer-reference#get-mempoolinfo)

```javascript
await restClient.getMemPoolInfo();
```

- [getTx](https://bitcoin.org/en/developer-reference#get-tx)

```javascript
const txid = "93520a51cc6c694e79913f1daf0288cb10e0d7946723c06b4e7b6c2e5b057933";
const format = "hex";
await restClient.getTx({ txid, format });
```
