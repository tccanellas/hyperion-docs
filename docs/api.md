# API Reference

***

### /v1/history/get_actions

#### POST
##### Summary

get actions

##### Description

legacy get actions query

##### Request Body
```
{
  "account_name": "string",
  "pos": 0,
  "offset": 0,
  "filter": "string",
  "sort": "desc",
  "after": "2020-01-17T19:51:03.618Z",
  "before": "2020-01-17T19:51:03.618Z",
  "parent": 0
}
```

##### Schema

|   variable	|  type 	|   description 	|
|:-:	|---	|---	|
| account_name  	|  string  <br>minLength: 1 maxLength: 12</br>	|   notified account	|
| pos	|  integer	|  action position (pagination) 	|
| offset  	|  integer 	|  limit of [n] actions per page 	|
| filter  | string <br>minLength: 3</br>     | code:name filter 
| sort    | string  | sort direction <br>Enum: [ desc, asc, 1, -1 ] | 
| after   | string($date-time)   |  filter after specified date (ISO8601)
| before  | string($date-time)   |  filter before specified date (ISO8601)
| parent  | integer <br>minimum: 0</br>  |  filter by parent global sequence

##### Responses

| Code | Description |
| ---- | ----------- |
| 200  |             |       

##### Example
```
curl -X POST "https://eos.hyperion.eosrio.io/v1/history/get_actions"
```

### /v1/history/get_controlled_accounts

#### POST
##### Summary

get controlled accounts by controlling accounts

##### Description

get controlled accounts by controlling accounts

##### Request Body <font size="0" color="red">Required</font>
```
{
  "controlling_account": "string"
}
```

##### Schema
|   variable	|  type 	|   description 	|
|:-:	|---	|---	|
| controlling_account  	|  string  |   controlling account	|

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Example
```
curl -X POST "https://eos.hyperion.eosrio.io/v1/history/get_controlled_accounts" -d '{"controlling_account":"eosio"}'
```

### /v1/history/get_key_accounts

#### POST
##### Summary

get accounts by public key

##### Description

get accounts by public key

##### Request Body <font size="0" color="red">Required</font>
```
{
  "public_key": "string"
}
```

##### Schema
|   variable	|  type 	|   description 	|
|:-:	|---	|---	|
| public_key  	|  public key  |   public key	|

##### Responses
| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Example
```
curl -X POST "https://eos.hyperion.eosrio.io/v1/history/get_key_accounts" -d '{"public_key":"EOS8fDDZm7ommT5XBf9MPYkRioXX6GeCUeSNkTpimdwKon5bNAVm7"}'
```

| Code | Description |
| ---- | ----------- |
| 200 |  |

### /v1/history/get_transaction

#### POST
##### Summary

get transaction by id

##### Description

get all actions belonging to the same transaction

##### Request Body <font size="0" color="red">Required</font>
```
{
  "id": "string"
}
```

##### Schema
|   variable	|  type 	|   description 	|
|:-:	|---	|---	|
| id  	|  string  |   transaction id	|

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Example
```
curl -X POST "https://eos.hyperion.eosrio.io/v1/history/get_transaction"
```

### /v1/chain/get_block

#### POST
##### Summary

Returns an object containing various details about a specific block on the blockchain.

##### Description

Returns an object containing various details about a specific block on the blockchain.

##### Request Body
```
{
  "block_num_or_id": "string"
}
```

##### Schema

block_num_or_id* -> string -> Provide a block number or a block id

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Example
```
curl -X POST "https://eos.hyperion.eosrio.io/v1/chain/get_block" -d '{"block_num_or_id": "1000"}'
```

### /v2/history/get_abi_snapshot

#### GET
##### Summary

fetch abi at specific block

##### Description

fetch contract abi at specific block

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| contract | query | contract account | Yes | string |
| block | query | target block | No | integer |
| fetch | query | should fetch the ABI | No | boolean |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

### /v2/history/get_actions

#### GET
##### Summary

get root actions

##### Description

get actions based on notified account. this endpoint also accepts generic filters based on indexed fields (e.g. act.authorization.actor=eosio or act.name=delegatebw), if included they will be combined with a AND operator

##### Request Body
N/A

##### Schema
N/A 

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| account | query | notified account | No | string |
| track | query | total results to track (count) [number or true] | No | string |
| filter | query | code:name filter | No | string |
| skip | query | skip [n] actions (pagination) | No | integer |
| limit | query | limit of [n] actions per page | No | integer |
| sort | query | sort direction | No | string |
| after | query | filter after specified date (ISO8601) | No | string |
| before | query | filter before specified date (ISO8601) | No | string |
| simple | query | simplified output mode | No | boolean |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

### /v2/history/get_blocks

#### GET
##### Summary

get block range

##### Description

get block range

##### Request Body
N/A

##### Schema
N/A 

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| from | query | starting block | No | integer |
| to | query | last block | No | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Examples
Get all blocks
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_blocks"
```
Get all blocks starting from block 1000
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_blocks?from=1000"
```
Get blocks from 10 to 15
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_blocks?from=10&to=15"
```

### /v2/history/get_created_accounts

#### GET
##### Summary

get created accounts

##### Description

get all accounts created by one creator

##### Request Body
N/A

##### Schema
N/A 

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| account | query | creator account | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Examples
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_created_accounts?account=eosio"
```

### /v2/history/get_creator

#### GET
##### Summary

get account creator

##### Description

get account creator

##### Request Body
N/A

##### Schema
N/A 

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| account | query | created account | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Example
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_creator?account=eosriobrazil"
```

### /v2/history/get_deltas

#### GET
##### Summary

get state deltas

##### Description

get state deltas

##### Request Body
N/A

##### Schema
N/A 

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| code | query | contract account | No | string |
| scope | query | table scope | No | string |
| table | query | table name | No | string |
| payer | query | payer account | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Examples
Get all deltas from `eosio.token` contract 
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_deltas?code=eosio.token"
```

Get all deltas from the table `accounts` of the `eosio.token` contract 
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_deltas?code=eosio.token&&table=accounts"
```

### /v2/history/get_transacted_accounts

#### GET
##### Summary

get interactions based on transfers

##### Description

get all account that interacted with the source account provided

##### Request Body
N/A

##### Schema
N/A 

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| account | query | source account | Yes | string |
| symbol | query | token symbol | No | string |
| contract | query | token contract | No | string |
| direction | query | search direction | Yes | string |
| min | query | minimum value | No | number |
| max | query | maximum value | No | number |
| limit | query | query limit | No | number |
| after | query | filter after specified date (ISO8601) or block number | No | string |
| before | query | filter before specified date (ISO8601) or block number | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Example

### /v2/history/get_transaction

#### GET
##### Summary

get transaction by id

##### Description

get all actions belonging to the same transaction

##### Request Body
N/A

##### Schema
N/A

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| id | query | transaction id | Yes | string |

##### Example
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_transaction?id=eec44c2ab2c2330e88fdacd3cd4c63838adb60da679ff12f299a4341fd036658"
```

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

### /v2/history/get_transfers

#### GET
##### Summary

get token transfers

##### Description

get token transfers utilizing the eosio.token standard

##### Request Body
N/A

##### Schema
N/A

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| from | query | source account | No | string |
| to | query | destination account | No | string |
| symbol | query | token symbol | No | string |
| contract | query | token contract | No | string |
| skip | query | skip [n] actions (pagination) | No | integer |
| limit | query | limit of [n] actions per page | No | integer |
| after | query | filter after specified date (ISO8601) | No | dateTime |
| before | query | filter before specified date (ISO8601) | No | dateTime |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Example
Get all transfers from eosriobrazil account
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_transfers?from=eosriobrazil"
```

Get all transfer from `eosriobrazil` account to `eosio.ramfee` account
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_transfers?from=eosriobrazil&to=eosio.ramfee"
```

Get all transfer from `eosriobrazil` account to `eosio.ramfee` account after November 2019
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/history/get_transfers?from=eosriobrazil&to=eosio.ramfee&after=2019-11-01T00:00:00.000Z"
```

### /v2/state/get_account

#### GET
##### Summary

get account summary

##### Description

get account data

##### Request Body
N/A

##### Schema
N/A

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| account | query | account name | No | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Example
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/state/get_account?account=eosio"
```

### /v2/state/get_key_accounts

#### GET
##### Summary

get accounts by public key

##### Description

get accounts by public key

##### Request Body
N/A

##### Schema
N/A

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| public_key | query | public key | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Example
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/state/get_key_accounts?public_key=EOS8fDDZm7ommT5XBf9MPYkRioXX6GeCUeSNkTpimdwKon5bNAVm7"
```

### /v2/state/get_key_accounts
#### POST
##### Summary

get accounts by public key

##### Description

get accounts by public key

##### Request Body
```
{
  "public_key": "string"
}
```

##### Schema
|   variable	|  type 	|   description 	|
|:-:	|---	|---	|
| public_key  	|  public key  |   public key	|

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Example
```
curl -X POST "https://eos.hyperion.eosrio.io/v2/state/get_key_accounts" -d '{"public_key":"EOS8fDDZm7ommT5XBf9MPYkRioXX6GeCUeSNkTpimdwKon5bNAVm7"}'
```

### /v2/state/get_proposals

#### GET
##### Summary

get proposals

##### Description

get proposals

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| proposer | query | filter by proposer | No | string |
| proposal | query | filter by proposal name | No | string |
| account | query | filter by either requested or provided account | No | string |
| requested | query | filter by requested account | No | string |
| provided | query | filter by provided account | No | string |
| executed | query | filter by execution status | No | boolean |
| track | query | total results to track (count) [number or true] | No | string |
| skip | query | skip [n] actions (pagination) | No | integer |
| limit | query | limit of [n] actions per page | No | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

### /v2/state/get_tokens

#### GET
##### Summary

get tokens from account

##### Description

get tokens from account

##### Request Body
N/A

##### Schema
N/A

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| account | query | account | Yes | string |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 |  |

##### Example
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/state/get_tokens?account=eosriobrazil"
```

### /v2/state/get_voters

#### GET
##### Summary

get voters

##### Description

get voters

##### Request Body
N/A

##### Schema
N/A

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| producer | query | filter by voted producer (comma separated) | No | string |
| skip | query | skip [n] actions (pagination) | No | integer |
| limit | query | limit of [n] actions per page | No | integer |

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

##### Example
Get all `eosriobrazil` voters
```
curl -X GET "https://eos.hyperion.eosrio.io/v2/state/get_voters?producer=eosriobrazil"
```
Get only the first 3 responses
```
curl -X GET https://eos.hyperion.eosrio.io/v2/state/get_voters?producer=eosriobrazil&limit=3
```

### /v2/health

#### GET
##### Summary:

API Service Health Report

##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | Default Response |

### /stream-client.js

#### GET
##### Responses

| Code | Description |
| ---- | ----------- |
| 200 | default response |
