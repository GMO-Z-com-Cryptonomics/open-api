# Wallet Service  <span style="font-size: 0.8em;">[🚀](../Readme.md#software-development-api-documents)</span>

## Overview
Detailed documentation to present the Open-api Wallet-service features.

## Table of contents

* [Deposit History](#deposithistory)

## DepositHistory

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `x-api-key`     |
| `Url` | `/api/v1/deposit/hisrec`     |
| `Method` | `GET`     |

### Request body

| Parameter | Type     | Mandatory | Description                |
| :-------- | :------- | :--------   | :------------------------- |
| `startTime` | `String` |  `Oprional`  | `startTime format unixTime milisecond` |
| `endTime` | `String`  | `Optional`  | `endTime format unixTime milisecond` |

#### Example

``` java
  curl --location '{url_domain}/api/v1/deposit/hisrec?startTime=1706150442000&endTime=1706150442000' 
    --header 'x-api-key: {x-api}'
    --data ''
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `id` | `Long`     | `ID of order` |
| `amount` | `BigDecimal`     | `amount` |
| `fees` | `String`     | `fee` |
| `currency` | `String`     | `currency` |
| `network` | `String`     | `network` |
| `status` | `String`     | `status` |
| `address` | `String`     | `address` |
| `addressTag` | `String`     | `addressTag` |
| `txId` | `String`     | `txId` |
| `transactionTime` | `Date`     | `transactionTime` |
| `transferType` | `StringBuilder`     | `transferType` |

#### Status code

| Http Code | Message                |  Descritpions  |
| :-------- | :------------------------- |  :---------------------  |
| `200`     | `Success`                  |  Success     |
| `400`     | `startTime must value must be in unix time stamp milliseconds.` | startTime format should be unix time in milisec. | 
| `400`     | `endTime must value must be in unix time stamp milliseconds`   |  endTime format should be unix time in milisec.  |
| `400`     | `startTime must be before endTime`   |  startTime can't more than endTime  |

##### Example Response

```json
  [{
    "id": "1",
    "amount": 0.09000000,
    "fees": "0.00000000",
    "currency": "THB",
    "network": "BTC",
    "status": "PENDING",
    "address": "0x072bebb8280d842b0984a686c80a06c1d3d471f9",
    "addressTag": "834112167",
    "txId": "0xbfb69f96020bec2e5f7414b6165af17c4a554a0f1d528af1e7528e05fff53321",
    "transactionTime": "2021-09-01 17:00:05",
    "transferType": "WITHDRAW"
  },{
    "id": "2",
    "amount": 0.09000000,
    "fees": "0.00000000",
    "currency": "THB",
    "network": "BTC",
    "status": "PENDING",
    "address": "0x072bebb8280d842b0984a686c80a06c1d3d471f9",
    "addressTag": "834112167",
    "txId": "0xbfb69f96020bec2e5f7414b6165af17c4a554a0f1d528af1e7528e05fff53321",
    "transactionTime": "2021-09-01 17:00:05",
    "transferType": "WITHDRAW"
  }]
    
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "startTime must be before endTime",
    "path": "/api/v1/deposit/hisrec"
  }
```