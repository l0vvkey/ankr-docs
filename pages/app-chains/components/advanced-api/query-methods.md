import { Tabs, Tab } from "nextra-theme-docs";
import { Callout } from "components";

# Query API

<Callout>
_Query API_ is a part of Advanced APIs' collection of methods that can be added as the add-on premium feature to the AppChains package.
</Callout>

_Query API_ is an access-ready solution that enables your projects to interact with multiple blockchains in a single request. By indexing blockchain data from all eight currently supported chains, searching through large amounts of data is easier and faster than ever before. Query API can boast almost instantaneous processing speeds (due to the key-value filtering supported) for the searches that might ordinarily take hours to process. 

Query API serves to request info on the ranges of blocks (max range is 100) for a full list of block metadata.

Query API implements the [JSON-RPC 2.0 specification](https://www.jsonrpc.org/specification) for interaction.

## Query API Methods

_Query API_ consists of the following methods to request info on the ranges of blocks (max range is 100) for a full list of block metadata:

  * [`ankr_getBlocks`](/app-chains/components/advanced-api/query-methods/#ankr_getblocks) — retrieves full info of a particular block.
  * [`ankr_getLogs`](/app-chains/components/advanced-api/query-methods/#ankr_getlogs) — retrieves history data of a particular block range.
  * [`ankr_getTransactionsByHash`](/app-chains/components/advanced-api/query-methods/#ankr_gettransactionsbyhash) — retrieves the details of a transaction specified by hash.
  * [`ankr_getTransactionsByAddress`](/app-chains/components/advanced-api/query-methods/#ankr_gettransactionsbyaddress) — retrieves the details of a transaction specified by address.
  * [`ankr_getBlockchainStats`](/app-chains/components/advanced-api/query-methods/#ankr_getblockchainstats) — retrieves blockchain statistics.
  * [`ankr_getInteractions`](/app-chains/components/advanced-api/query-methods/#ankr_getinteractions) — retrieves blockchains interacted with a particular wallet.

---

## `ankr_getBlocks`

> **Retrieves the blocks' data.**

Retrieves complete information for the block specified.

### Request

Build your request using the parameters below.

#### Parameters

* `id` (int64; required): a request ID (example: 1).
* `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0). 
* `method` (string; required): a method used for the request.
* `params` (object; required): the data object containing request body parameters:

  * `blockchain` (string; required): either of the supported chains (`bas_bombchain`, `bas_bombchain_testnet`, `bas_metaapes`, `bas_metaapes_testnet`).
  * `decodeLogs` (boolean): set to `true` to decode logs, or to `false` if you don't need this kind of info.
  * `decodeTxData` (boolean): set to `true` to decode transaction data, or to `false` if not interested in it.
  * `descOrder` (boolean): choose data order, either descending (if `true`) or ascending (if `false`).
  * `fromBlock` (uint64): the first block of the range.
  * `toBlock` (uint64): the last block included in the range.
  * `includeLogs` (boolean): set to `true` to include logs, or to `false` to exclude them. Note that logs are stored inside transactions, so make sure the following parameter is also set to `true` if you'd like to include logs.
  * `includeTxs` (boolean): set to `true` to include transactions, or to `false` to exclude them.

<Tabs
  items={[
    "Body",
    "Headers",
  ]}
>   
  <Tab>

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ankr_getBlocks",
  "params": {
    "blockchain": "string",
    "decodeLogs": true,
    "decodeTxData": true,
    "descOrder": true,
    "fromBlock": 0,
    "includeLogs": true,
    "includeTxs": true,
    "toBlock": 0
  }
}
```
  </Tab>
  <Tab>

```shell
Content-Type: application/json
```
  </Tab>
</Tabs>

### Response

Returns complete information for the block specified by request parameters.

### Code Examples

#### Request

```shell
curl --location --request POST 'https://rpc.chainscanner.xyz/multichain' \
--header 'Content-Type: application/json' \
--data-raw '{
    "jsonrpc": "2.0",
    "method": "ankr_getBlocks",
    "params": {
        "blockchain": "bas_bombchain",
        "fromBlock": 14500000,
        "toBlock": 14500000,
        "decodeLogs": false,
        "decodeTxData": true,
        "includeLogs": true,
        "includeTxs": true
    },
    "id": 1
}'
```

#### Response

Code: 200 OK

<Tabs
  items={[
    "Schema",
    "Example",
  ]}
>
  <Tab>

```json
{
  "error": {},
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "blocks": [
      {
        "blockHash": "string",
        "blockHeight": "string",
        "blockchainLogo": "string",
        "blockchainName": "string",
        "details": {
          "ethBlock": {
            "difficulty": "string",
            "extraData": "string",
            "gasLimit": 0,
            "gasUsed": 0,
            "miner": "string",
            "nonce": "string",
            "sha3Uncles": "string",
            "size": "string",
            "stateRoot": "string",
            "totalDifficulty": "string"
          }
        },
        "parentHash": "string",
        "timestamp": "string",
        "transactionsCount": 0
      }
    ]
  }
}
```
  </Tab>
  <Tab>

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "blocks": [
            {
                "blockchain": "bas_bombchain",
                "number": "0xdd40a0",
                "hash": "0xfeed3e175e482268db83d4fd87a43c708f40983343f4b039e582c6f6a95e0e78",
                "parentHash": "0xe311161a7462068919abe2ac2cd42e5806898b3f42ec597699ce764c067c416a",
                "nonce": "0xc5f9ce09d63baf71",
                "mixHash": "0xbd7063d27079586ab3fdae7de0472f93f96f81a0f6c5b3abe903a9c6f62cab06",
                "sha3Uncles": "0x1dcc4de8dec75d7aab85b567b6ccd41ad312451b948a7413f0a142fd40d49347",
                "logsBloom": "0x00000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000",
                "stateRoot": "0xbbf4fe65498447568abe945ea8f926791e491873a367c82ae847aeadf0c7e17f",
                "miner": "0xea674fdde714fd979de3edf0f56aa9716b898ec8",
                "difficulty": "0x2e032d1caff8d9",
                "extraData": "0x617369612d65617374312d34",
                "size": "0x219",
                "gasLimit": "0x1ca35d2",
                "gasUsed": "0x0",
                "timestamp": "0x6246dd9c",
                "transactionsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
                "receiptsRoot": "0x56e81f171bcc55a6ff8345e692c0f86e5b48e01b996cadc001622fb5e363b421",
                "totalDifficulty": "0x994af3a04b379bb8b42",
                "transactions": [],
                "uncles": []
            }
        ]
    }
}
```
  </Tab>
</Tabs>

---

## `ankr_getLogs`

> **Retrieves the blocks' history data.**

Retrieves history data for the blocks specified.

### Request

Build your request using the parameters below.

#### Parameters

* `id` (int64; required): a request ID (example: 1).
* `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0). 
* `method` (string; required): a method used for the request.
* `params` (object; required): the data object containing request body parameters:

  * `address` (uint8): an address of the contract created the logs. Supported value formats: hex or array of hexes.
  * `blockchain` (string): a chain or a combination of chains to query:
    * Single chain: `bas_bombchain`, `bas_bombchain_testnet`, `bas_metaapes`, `bas_metaapes_testnet`.
    * Chains combination: `[bas_bombchain, bas_metaapes, bas_bombchain_testnet]`.
    * All chains: leave the value empty to query all the chains available.
  * `decodeLogs` (boolean): set to `true` to decode logs, or to `false` if you don't need this kind of info.
  * `descOrder` (boolean): choose data order, either descending (if `true`) or ascending (if `false`).
  * `fromBlock` (string): the first block of the range. Supported value formats: hex, decimal, "earliest", "latest". 
  * `fromTimestamp` (uint64): the first timestamp of the range.
  * `pageSize` (string): a number of result pages you'd like to get.
  * `pageToken` (string): a token is provided at the end of the response body and can be referenced in the request to fetch the next page.
  * `toBlock` (string): the last block included in the range.
  * `toTimestamp` (uint64): the last timestamp of the range.
  * `topics` (uint8): the data the log contains.

<Tabs
  items={[
    "Body",
    "Headers",
  ]}
>
  <Tab>

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ankr_getLogs",
  "params": {
    "address": [
      [
        0
      ]
    ],
    "blockchain": [
      "string"
    ],
    "decodeLogs": true,
    "descOrder": true,
    "fromBlock": 0,
    "fromTimestamp": 0,
    "pageSize": 0,
    "pageToken": "string",
    "toBlock": 0,
    "toTimestamp": 0,
    "topics": [
      [
        [
          0
        ]
      ]
    ]
  }
}
```
  </Tab>
  <Tab>

```shell
Content-Type: application/json
```
  </Tab>
</Tabs>

### Response

Returns history data for the blocks specified by request body parameters.

### Code Examples

#### Request

```shell
curl --location --request POST 'https://rpc.chainscanner.xyz/multichain' \
--header 'Content-Type: application/json' \
--data-raw '{
    "jsonrpc": "2.0",
    "method": "ankr_getLogs",
    "params": {
        "blockchain": "bas_bombchain",
        "fromBlock": "0xdaf6b1", // hex, decimal, "earliest", "latest" are supported
        "toBlock": 14350010, // hex, decimal, "earliest", "latest" are supported
        "address": ["0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2"], // hex or array of hexes are supported
        "topics": [
            [],
            [
                "0x000000000000000000000000def1c0ded9bec7f1a1670819833240f027b25eff"
            ]
        ]
    },
    "id": 1
}'
```

#### Response

Code: 200 OK

<Tabs
  items={[
    "Schema",
    "Example",
  ]}
>
  <Tab>

```json
{
  "error": {},
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "logs": [
      {
        "address": "string",
        "blockHash": "string",
        "blockNumber": "string",
        "data": "string",
        "event": {
          "anonymous": true,
          "id": "string",
          "inputs": [
            {
              "indexed": true,
              "name": "string",
              "size": 0,
              "type": "string",
              "valueDecoded": "string"
            }
          ],
          "name": "string",
          "signature": "string",
          "string": "string",
          "verified": true
        },
        "logIndex": "string",
        "removed": true,
        "topics": [
          "string"
        ],
        "transactionHash": "string",
        "transactionIndex": "string"
      }
    ],
    "nextPageToken": "string"
  }
}
```
  </Tab>
  <Tab>

```json
{
  "jsonrpc": "2.0",
  "id": 1,
  "result": {
    "logs": [
      {
        "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "topics": [
          "0xe1fffcc4923d04b559f4d29a8bfc6cda04eb5b0d3c460751c2402c5c5cc9109c",
          "0x000000000000000000000000def1c0ded9bec7f1a1670819833240f027b25eff"
        ],
        "data": "0x00000000000000000000000000000000000000000000000006ce16d63d3e98d5",
        "blockNumber": "0xdaf6b1",
        "transactionHash": "0xa00481485db1092529a3502bd8027e0a85a7eff1ecc17d4adae5b38a2ba33ba1",
        "transactionIndex": "0x1",
        "blockHash": "0xdd6a92a8d1436f97e6d3c33154805156b92b59f2cfef3f3fa390ba49643f09e8",
        "logIndex": "0x0",
        "removed": false
      },
      {
        "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "topics": [
          "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
          "0x000000000000000000000000def1c0ded9bec7f1a1670819833240f027b25eff",
          "0x00000000000000000000000092f0b57e3814e4bd74ef6a6fd6d825db522ccfe2"
        ],
        "data": "0x00000000000000000000000000000000000000000000000006ce16d63d3e98d5",
        "blockNumber": "0xdaf6b1",
        "transactionHash": "0xa00481485db1092529a3502bd8027e0a85a7eff1ecc17d4adae5b38a2ba33ba1",
        "transactionIndex": "0x1",
        "blockHash": "0xdd6a92a8d1436f97e6d3c33154805156b92b59f2cfef3f3fa390ba49643f09e8",
        "logIndex": "0x2",
        "removed": false
      },
      {
        "address": "0xc02aaa39b223fe8d0a0e5c4f27ead9083c756cc2",
        "topics": [
          "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
          "0x000000000000000000000000def1c0ded9bec7f1a1670819833240f027b25eff",
          "0x000000000000000000000000d42bd36302f33d77cbb080ad7e0434f6bedc9a44"
        ],
        "data": "0x000000000000000000000000000000000000000000000000081e9d8d247e8a1d",
        "blockNumber": "0xdaf6b3",
        "transactionHash": "0x9b196e7b81c1aeed1c2bbe3d65c411a6eaecc21ddf5bd7c34141e88577384d4d",
        "transactionIndex": "0x3",
        "blockHash": "0xa48f22823710329ad512e3ffc0378a2cc15abda153af23dd6361d58ab190cdb1",
        "logIndex": "0x22",
        "removed": false
      }
    ]
  }
}
```
  </Tab>
</Tabs>

---

## `ankr_getTransactionsByHash`

> **Retrieves data for the hash-specified transaction.**

Retrieves the details for a transaction specified by hash.

### Request

Build your request using the parameters below.

#### Parameters

* `id` (int64; required): a request ID (example: 1).
* `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0). 
* `method` (string; required): a method used for the request.
* `params` (object; required): the data object containing request body parameters:

  * `blockchain` (string): a chain or a combination of chains to query:
    * Single chain: `bas_bombchain`, `bas_bombchain_testnet`, `bas_metaapes`, `bas_metaapes_testnet`.
    * Chains combination: `[bas_bombchain, bas_metaapes, bas_bombchain_testnet]`.
    * All chains: leave the value empty to query all the chains available.
  * `transactionHash` (string): a hash of the transactions you'd like to request the details for.
  * `decodeLogs` (boolean): set to `true` to decode logs, or to `false` if you don't need this kind of info.
  * `decodeTxData` (boolean): set to `true` to decode transaction data, or to `false` if not interested in it.
  * `includeLogs` (boolean): set to `true` to include logs, or to `false` to exclude them.

<Tabs
  items={[
    "Body",
    "Headers",
  ]}
>
  <Tab>

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ankr_getTransactionsByHash",
  "params": {
    "blockchain": [
      "string"
    ],
    "decodeLogs": true,
    "decodeTxData": true,
    "includeLogs": true,
    "transactionHash": "string"
  }
}
```
  </Tab>
  <Tab>

```shell
Content-Type: application/json
```
  </Tab>
</Tabs>

### Response

Returns all transactions' metadata for the hash specified in request body parameters.

### Code Examples

#### Request

```shell
curl --location -g --request POST 'https://rpc.chainscanner.xyz/multichain' \
--header 'Content-Type: application/json' \
--data-raw '{
    "jsonrpc": "2.0",
    "method": "ankr_getTransactionsByHash",
    "params": {
        "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
        "decodeLogs": true,
        "decodeTxData": true
    },
    "id": 1
}'
```

#### Response

Code: 200 OK

<Tabs
  items={[
    "Schema",
    "Example",
  ]}
>
  <Tab>

```json
{
  "error": {},
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "transactions": [
      {
        "blockHash": "string",
        "blockNumber": "string",
        "blockchain": "string",
        "contractAddress": "string",
        "cumulativeGasUsed": "string",
        "from": "string",
        "gas": "string",
        "gasPrice": "string",
        "gasUsed": "string",
        "hash": "string",
        "input": "string",
        "logs": [
          {
            "address": "string",
            "blockHash": "string",
            "blockNumber": "string",
            "data": "string",
            "event": {
              "anonymous": true,
              "id": "string",
              "inputs": [
                {
                  "indexed": true,
                  "name": "string",
                  "size": 0,
                  "type": "string",
                  "valueDecoded": "string"
                }
              ],
              "name": "string",
              "signature": "string",
              "string": "string",
              "verified": true
            },
            "logIndex": "string",
            "removed": true,
            "topics": [
              "string"
            ],
            "transactionHash": "string",
            "transactionIndex": "string"
          }
        ],
        "logsBloom": "string",
        "method": {
          "id": "string",
          "inputs": [
            {
              "name": "string",
              "size": 0,
              "type": "string",
              "valueDecoded": "string"
            }
          ],
          "name": "string",
          "signature": "string",
          "string": "string",
          "verified": true
        },
        "nonce": "string",
        "r": "string",
        "s": "string",
        "status": "string",
        "timestamp": "string",
        "to": "string",
        "transactionHash": "string",
        "transactionIndex": "string",
        "type": "string",
        "v": "string",
        "value": "string"
      }
    ]
  }
}
```
  </Tab>
  <Tab>

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "transactions": [
            {
                "v": "0x94",
                "r": "0xc3adcd90cbf2ef2870c0b7b5497e3c8a5757aadcc152ec1156804082c3269451",
                "s": "0x1c12681bee4a75a7514f4251bcb4a0243bfc70de998f5c77d87aedc56bce85fc",
                "nonce": "0x1615d",
                "from": "0x64aa6f93e0e1f49ff4958990c40d4bf17dafc0eb",
                "gas": "0x5cc60",
                "gasPrice": "0x1c3802ec80",
                "input": "0x1d3ec0d600000000000000000000000000000000000000000000000000000000000000e000000000000000000000000000000000000000000052b2e13cc84f2c000000000000000000000000000000000000000000000000000000000000000000000001000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000052b7ce5e6080a4eaee3fd000000000000000000000000000000000000000000052aed9671d3df9df54b80000000000000000000000000010ed43c718714eb63d5aa57b78b54704e256024e0000000000000000000000000000000000000000000000000000000000000002000000000000000000000000000000000000000000000000000000002043c3f900000000000000000000000000000000000000000000000000000000310ff2d6",
                "blockNumber": "0xd02cf7",
                "to": "0x98767abab06e45a181ab73ae4cd0fecd0fbd0cd0",
                "transactionIndex": "0x0",
                "blockHash": "0x7c4b9b19b521795a0a99c925d4a03079aca26f14cb7bc1400d0183a5adf56ac1",
                "value": "0x0",
                "type": "0x0",
                "contractAddress": null,
                "cumulativeGasUsed": "0x176b2",
                "gasUsed": "0x176b2",
                "logs": [
                    {
                        "address": "0xbb4cdb9cbd36b01bd1cbaebf2de08d9173bc095c",
                        "topics": [
                            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                            "0x00000000000000000000000098767abab06e45a181ab73ae4cd0fecd0fbd0cd0",
                            "0x00000000000000000000000058f876857a02d6762e0101bb5c46a8c1ed44dc16"
                        ],
                        "data": "0x0000000000000000000000000000000000000000000000047e678c2df911bc30",
                        "blockNumber": "0xd02cf7",
                        "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                        "transactionIndex": "0x0",
                        "blockHash": "0x7c4b9b19b521795a0a99c925d4a03079aca26f14cb7bc1400d0183a5adf56ac1",
                        "logIndex": "0x0",
                        "removed": false,
                        "event": {
                            "name": "Transfer",
                            "inputs": [
                                {
                                    "name": "_from",
                                    "type": "address",
                                    "indexed": true,
                                    "size": 20,
                                    "valueDecoded": "0x98767abab06e45a181Ab73AE4cD0FeCd0FBD0cD0"
                                },
                                {
                                    "name": "_to",
                                    "type": "address",
                                    "indexed": true,
                                    "size": 20,
                                    "valueDecoded": "0x58F876857a02D6762E0101bb5C46A8c1ED44Dc16"
                                },
                                {
                                    "name": "_value",
                                    "type": "uint256",
                                    "indexed": false,
                                    "size": 256,
                                    "valueDecoded": "82895379195298430000"
                                }
                            ],
                            "anonymous": false,
                            "string": "event Transfer(address indexed _from, address indexed _to, uint256 _value)",
                            "signature": "Transfer(address,address,uint256)",
                            "id": "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                            "verified": false
                        }
                    },
                    {
                        "address": "0xe9e7cea3dedca5984780bafc599bd69add087d56",
                        "topics": [
                            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                            "0x00000000000000000000000058f876857a02d6762e0101bb5c46a8c1ed44dc16",
                            "0x00000000000000000000000098767abab06e45a181ab73ae4cd0fecd0fbd0cd0"
                        ],
                        "data": "0x0000000000000000000000000000000000000000000008fc40ca5d0026461ddc",
                        "blockNumber": "0xd02cf7",
                        "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                        "transactionIndex": "0x0",
                        "blockHash": "0x7c4b9b19b521795a0a99c925d4a03079aca26f14cb7bc1400d0183a5adf56ac1",
                        "logIndex": "0x1",
                        "removed": false,
                        "event": {
                            "name": "Transfer",
                            "inputs": [
                                {
                                    "name": "_from",
                                    "type": "address",
                                    "indexed": true,
                                    "size": 20,
                                    "valueDecoded": "0x58F876857a02D6762E0101bb5C46A8c1ED44Dc16"
                                },
                                {
                                    "name": "_to",
                                    "type": "address",
                                    "indexed": true,
                                    "size": 20,
                                    "valueDecoded": "0x98767abab06e45a181Ab73AE4cD0FeCd0FBD0cD0"
                                },
                                {
                                    "name": "_value",
                                    "type": "uint256",
                                    "indexed": false,
                                    "size": 256,
                                    "valueDecoded": "42432180015750915169756"
                                }
                            ],
                            "anonymous": false,
                            "string": "event Transfer(address indexed _from, address indexed _to, uint256 _value)",
                            "signature": "Transfer(address,address,uint256)",
                            "id": "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                            "verified": false
                        }
                    },
                    {
                        "address": "0x58f876857a02d6762e0101bb5c46a8c1ed44dc16",
                        "topics": [
                            "0x1c411e9a96e071241c2f21f7726b17ae89e3cab4c78be50e062b03a9fffbbad1"
                        ],
                        "data": "0x000000000000000000000000000000000000000000005f4272d9c342f8340191000000000000000000000000000000000000000000beea5069c8a189501d6059",
                        "blockNumber": "0xd02cf7",
                        "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                        "transactionIndex": "0x0",
                        "blockHash": "0x7c4b9b19b521795a0a99c925d4a03079aca26f14cb7bc1400d0183a5adf56ac1",
                        "logIndex": "0x2",
                        "removed": false,
                        "event": {
                            "name": "",
                            "inputs": [],
                            "anonymous": false,
                            "string": "",
                            "signature": "",
                            "id": "",
                            "verified": false
                        }
                    },
                    {
                        "address": "0x58f876857a02d6762e0101bb5c46a8c1ed44dc16",
                        "topics": [
                            "0xd78ad95fa46c994b6551d0da85fc275fe613ce37657fb8d5e3d130840159d822",
                            "0x00000000000000000000000010ed43c718714eb63d5aa57b78b54704e256024e",
                            "0x00000000000000000000000098767abab06e45a181ab73ae4cd0fecd0fbd0cd0"
                        ],
                        "data": "0x0000000000000000000000000000000000000000000000047e678c2df911bc30000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000008fc40ca5d0026461ddc",
                        "blockNumber": "0xd02cf7",
                        "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                        "transactionIndex": "0x0",
                        "blockHash": "0x7c4b9b19b521795a0a99c925d4a03079aca26f14cb7bc1400d0183a5adf56ac1",
                        "logIndex": "0x3",
                        "removed": false,
                        "event": {
                            "name": "",
                            "inputs": [],
                            "anonymous": false,
                            "string": "",
                            "signature": "",
                            "id": "",
                            "verified": false
                        }
                    },
                    {
                        "address": "0x0000000000004946c0e9f43f4dee607b0ef1fa1c",
                        "topics": [
                            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                            "0x00000000000000000000000098767abab06e45a181ab73ae4cd0fecd0fbd0cd0",
                            "0x0000000000000000000000000000000000000000000000000000000000000000"
                        ],
                        "data": "0x0000000000000000000000000000000000000000000000000000000000000003",
                        "blockNumber": "0xd02cf7",
                        "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                        "transactionIndex": "0x0",
                        "blockHash": "0x7c4b9b19b521795a0a99c925d4a03079aca26f14cb7bc1400d0183a5adf56ac1",
                        "logIndex": "0x4",
                        "removed": false,
                        "event": {
                            "name": "Transfer",
                            "inputs": [
                                {
                                    "name": "_from",
                                    "type": "address",
                                    "indexed": true,
                                    "size": 20,
                                    "valueDecoded": "0x98767abab06e45a181Ab73AE4cD0FeCd0FBD0cD0"
                                },
                                {
                                    "name": "_to",
                                    "type": "address",
                                    "indexed": true,
                                    "size": 20,
                                    "valueDecoded": "0x0000000000000000000000000000000000000000"
                                },
                                {
                                    "name": "_value",
                                    "type": "uint256",
                                    "indexed": false,
                                    "size": 256,
                                    "valueDecoded": "3"
                                }
                            ],
                            "anonymous": false,
                            "string": "event Transfer(address indexed _from, address indexed _to, uint256 _value)",
                            "signature": "Transfer(address,address,uint256)",
                            "id": "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                            "verified": false
                        }
                    }
                ],
                "logsBloom": "0x0",
                "transactionHash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                "hash": "0x82c13aaac6f0b6471afb94a3a64ae89d45baa3608ad397621dbb0d847f51196f",
                "status": "0x1",
                "blockchain": "bsc",
                "timestamp": "0x61c09887",
                "method": {
                    "name": "",
                    "inputs": [],
                    "string": "",
                    "signature": "",
                    "id": "",
                    "verified": false
                }
            }
        ]
    }
}
```
  </Tab>
</Tabs>

---

## `ankr_getTransactionsByAddress`

> **Retrieves transactions by address.**

Retrieves the details of transactions specified by address.

### Request

Build your request using the parameters below.

#### Parameters

* `id` (int64; required): a request ID (example: 1).
* `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0). 
* `method` (string; required): a method used for the request.
* `params` (object; required): the data object containing request body parameters:

    * `address` (string; required): an address to search for transactions.
    * `blockchain` (string): either of the supported chains (`bas_bombchain`, `bas_bombchain_testnet`, `bas_metaapes`, `bas_metaapes_testnet`).
    * `fromBlock` (integer): narrow your search indicating the block number to start from (inclusive; `>= 0`).
    * `toBlock` (integer): narrow your search indicating the block number to end with (inclusive; `>= 0`).
    * `fromTimestamp` (integer): narrow your search indicating the timestamp to start from (inclusive; `>= 0`).
    * `toTimestamp` (integer): narrow your search indicating the timestamp to end with (inclusive; `>=0`).
    * `includeLogs` (boolean): set to `true` to include logs, or to `false` to exclude them.
    * `descOrder` (boolean): choose data order, either descending (if `true`) or ascending (if `false`).
    * `pageSize` (int32): a number of result pages you'd like to get.
    * `pageToken` (string): a token is provided at the end of the response body and can be referenced in the request to fetch the next page.

<Tabs
  items={[
    "Body",
    "Headers",
  ]}
>
  <Tab>

```json
{
    "id": 1,
    "jsonrpc": "2.0",
    "method": "ankr_getTransactionsByAddress",
    "params": {
        "blockchain": "string",
        "includeLogs": true,
        "descOrder": true,
        "pageSize": 0,
        "pageToken": "string",
        "toTimestamp": 0,
        "address": "string"
    }
}
```
  </Tab>
  <Tab>

```shell
Content-Type: application/json
```
  </Tab>
</Tabs>

### Response

Returns the transactions specified by address.

### Code Examples

#### Request

```shell
curl --location -g --request POST 'https://rpc.chainscanner.xyz/multichain' \
--header 'Content-Type: application/json' \
--data-raw '{
    "id": 1,
    "jsonrpc": "2.0",
    "method": "ankr_getTransactionsByAddress",
    "params": {
        "address": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045"
    }
  }'
```

#### Response

Code: 200 OK

<Tabs
  items={[
    "Schema",
    "Example",
  ]}
>
  <Tab>

```json
{
    "id": 1,
    "jsonrpc": "2.0",
    "result": {
        "transactions": [
            {
                "blockHash": "string",
                "blockNumber": "string",
                "blockchain": "string",
                "cumulativeGasUsed": "string",
                "from": "string",
                "gas": "string",
                "gasPrice": "string",
                "gasUsed": "string",
                "hash": "string",
                "input": "string",
                "nonce": "string",
                "r": "string",
                "s": "string",
                "status": "string",
                "timestamp": "string",
                "to": "string",
                "transactionIndex": "string",
                "type": "string",
                "v": "string",
                "value": "string"
            }
        ]
    }
}
```
  </Tab>
  <Tab>

```json
{
    "id": 1,
    "jsonrpc": "2.0",
    "result": {
        "transactions": [
            {
                "blockHash": "0x8ffa5d490184c95c830bb4fb47b76e1fd69eb35d100f93d36d7db131837c938f",
                "blockNumber": "0xf823ad",
                "blockchain": "bas_bombchain",
                "cumulativeGasUsed": "0x68f589",
                "from": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
                "gas": "0xbe98",
                "gasPrice": "0x2babee650",
                "gasUsed": "0xbd8d",
                "hash": "0x9a70ccd1f8e0d5ddf8e78f68b477d4d5c15ddd17c66f05f820b4c67f5eb6f85a",
                "input": "0xa9059cbb000000000000000000000000fe97e32a873aa2f926fbfc560abeef01f753c1280000000000000000000000000000000000000000000000000000002e90edd000",
                "nonce": "0x3c4",
                "r": "0xe5c2731e3a85d048b4adb0cf9c06cb51013728627525ce80e96c4f1317007104",
                "s": "0x3a22f49130b59d832a6c9db79880b313e9ca2536a3fd5f10b8080e2e1c3bda97",
                "status": "0x1",
                "timestamp": "0x63a85033",
                "to": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
                "transactionIndex": "0x3c",
                "type": "0x2",
                "v": "0x0",
                "value": "0x0"
            }
        ]
    }
}
```
  </Tab>
</Tabs>

---

## `ankr_getBlockchainStats`

> **Retrieves blockchain statistics.**

### Request

Build your request using the parameters below.

#### Parameters

* `id` (int64; required): a request ID (example: 1).
* `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0). 
* `method` (string; required): a method used for the request.
* `params` (object; required): the data object containing request body parameters:

  * `blockchain` (string): a chain or a combination of chains to query:
    * Single chain: `bas_bombchain`, `bas_bombchain_testnet`, `bas_metaapes`, `bas_metaapes_testnet`.
    * Chains combination: `[bas_bombchain, bas_metaapes, bas_bombchain_testnet]`.
    * All chains: leave the value empty to query all the chains available.

<Tabs
  items={[
    "Body",
    "Headers",
  ]}
>
  <Tab>

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ankr_getInteractions",
  "params": {
    "address": "string"
  }
}
```
  </Tab>
  <Tab>

```shell
Content-Type: application/json
```
  </Tab>
</Tabs>

### Response

Returns statistics for the blockchains specified.

### Code Examples

#### Request

```shell
curl --location --request POST 'https://rpc.chainscanner.xyz/multichain' \
--header 'Content-Type: application/json' \
--data-raw '{
    "jsonrpc": "2.0",
    "method": "ankr_getBlockchainStats",
    "params": {},
    "id": 1
}'
```

#### Response

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "stats": [
      {
        "blockTimeMs": 3000,
        "blockchain": "bas_bombchain",
        "latestBlockNumber": 24274429,
        "nativeCoinUsdPrice": "245.153233940444766334",
        "totalEventsCount": 11643833187,
        "totalTransactionsCount": 3764960943
      },
      {
        "blockTimeMs": 4000,
        "blockchain": "bas_metaapes",
        "latestBlockNumber": 37350500,
        "nativeCoinUsdPrice": "0.803307052493372837",
        "totalEventsCount": 8710949888,
        "totalTransactionsCount": 2318753716
      }
    ]
  }
}
```

---

## `ankr_getInteractions`

> **Retrieves blockchains interacted with a particular address.**

Retrieves a list of blockchains on which the address interaction was registered and manifested by the info available for the address (tokens, NFTs, transactions).

### Request

Build your request using the parameters below.

#### Parameters

* `id` (int64; required): a request ID (example: 1).
* `jsonrpc` (string; required): a JSON RPC spec used (example: 2.0). 
* `method` (string; required): a method used for the request.
* `params` (object; required): the data object containing request body parameters:

  * `address` (string): an address of the contract created the logs.

<Tabs
  items={[
    "Body",
    "Headers",
  ]}
>
  <Tab>

```json
{
  "id": 1,
  "jsonrpc": "2.0",
  "method": "ankr_getInteractions",
  "params": {
    "address": "string"
  }
}
```
  </Tab>
  <Tab>

```shell
Content-Type: application/json
```
  </Tab>
</Tabs>

### Response

Returns the list of blockchains interacted with the address specified in request body parameters.

### Code Examples

#### Request

```shell
curl --location -g --request POST 'https://rpc.chainscanner.xyz/multichain' \
--header 'Content-Type: application/json' \
--data-raw '{
		"jsonrpc": "2.0",
		"method": "ankr_getInteractions",
		"params": {
			"address":"0xF977814e90dA44bFA03b6295A0616a897441aceC"
		},
		"id": "1"
	}'
```

#### Response

Code: 200 OK

<Tabs
  items={[
    "Schema",
    "Example",
  ]}
>
  <Tab>

```json
{
  "error": {},
  "id": 1,
  "jsonrpc": "2.0",
  "result": {
    "blockchains": [
      "string"
    ]
  }
}
```
  </Tab>
  <Tab>

```json
{
    "jsonrpc": "2.0",
    "id": "1",
    "result": {
        "blockchains": [
            "bas_bombchain",
            "bas_bombchain_testnet",
            "bas_metaapes",
            "bas_metaapes_testnet"
        ]
    }
}
```
  </Tab>
</Tabs>