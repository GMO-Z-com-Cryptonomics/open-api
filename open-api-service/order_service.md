# Place Order Service  <span style="font-size: 0.8em;">[🚀](../Readme.md#software-development-api-documents)</span>

## Overview

Place order service providing about create order and get order delete order.

## Table of contents

* [Place Order Service](#placeorderservice)
* [Get Order Service](#getorderservice)
* [Cancel Order Service](#cancelorderservice)
* [Cancel All Order Service](#cancelAllOrderService)
* [Get All Order Service](#getAllOrderService)
* [Open Order Service](#openOrderService)

## PlaceOrderService
  - To create new order by symbol side quanity price and clientId. 

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `Authorization` | `Basic authenticate`     |
| `Url` | `/api/v1/order`     |
| `Method` | `POST`     |

### Request body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol` | `String`     | `Currency for exchange` |
| `side` | `String`     | `Side for action` |
| `quantity` | `BigDecimal`     | `Quanity currency` |
| `price` | `BigDecimal`     | `Price` |
| `clientId` | `String`     | ` - ` |

#### Example

``` java
  curl --location 'http://localhost/api/v1/order'
  --header 'Content-Type: application/json'
  --header 'Authorization: Basic {"basic authenticate"}' 
  --data '{
      "symbol" : "BTC_THB",
      "side" : "BUY",
      "quantity" : 0.2,
      "price" : 1188000,
      "cliendId" : ""
  }'
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `orderId` | `String`     | `ID of order` |
| `clientId` | `String`     | `ID od client` |
| `symbol` | `String`     | `Symbol` |
| `side` | `String`     | `Side` |
| `type` | `String`     | `Type of currency` |
| `quantity` | `BigDecimal`     | `Quanity` |
| `price` | `BigDecimal`     | `Price` |
| `status` | `String`     | `Status` |
| `timestamp` | `Date`     | `TimeStamp` |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `clientId must be unique.` |
| `400`     | `Trade functionality is blocked!`   |
| `400`     | `Ttrading is not enabled on this pair` |
| `400`     | `We temporary stop market order. Sorry for inconvenience!` |
| `400`     | `You have placed order more than 10 at the same location` |
| `500`     | `Internal Error`           |

##### Example

```json
  {
    "orderId": "USDT",
    "clientId": "test",
    "symbol": 123.32,
    "side": 213,
    "type": "21232",
    "quantity": "21232",
    "price": "21232",
    "status": "21232",
    "timestamp": "21232",
  }
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "This order is being processed.",
    "path": "/api/v1/cancelOrder"
  }
```

## GetOrderService
- This service to providing about order data it will return all of order follow symbol.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `Authorization` | `Basic authenticate`     |
| `Url` | `/api/v1/order`     |
| `Method` | `GET`     |

### Request parameter

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol` | `String`     | `Symbol` |
| `orderId` | `String`     | `Order Id` |
| `clientId` | `BigDecimal`     | `Client Id` |

#### Example Curl

``` java
  curl --location 'http://localhost/api/v1/openOrder?symbols=BTC_THB%2C%20XRP_THB&symbols=XRP_THB' 
  --header 'Authorization: Basic {basic authenticate}' 
  --data ''
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol` | `String`     | `ID of order` |
| `orderId` | `String`     | `ID od client` |
| `clientId` | `String`     | `Symbol` |
| `price` | `String`     | `Side` |
| `origQty` | `String`     | `Type of currency` |
| `executedQty` | `BigDecimal`     | `Quanity` |
| `price` | `BigDecimal`     | `Price` |
| `side` | `String`     | `Status` |
| `status` | `Date`     | `TimeStamp` |
| `time` | `Date`     | `TimeStamp` |
| `isWorking` | `Date`     | `TimeStamp` |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `clientId must be unique.` |
| `400`     | `Trade functionality is blocked!`   |
| `400`     | `Ttrading is not enabled on this pair` |
| `400`     | `We temporary stop market order. Sorry for inconvenience!` |
| `400`     | `You have placed order more than 10 at the same location` |
| `500`     | `Internal Error`           |

##### Example Success

```json
  {
    "orderId": "USDT",
    "clientId": "test",
    "symbol": 123.32,
    "side": 213,
    "type": "21232",
    "quantity": "21232",
    "price": "21232",
    "status": "21232",
    "timestamp": "21232",
  }
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "This order is being processed.",
    "path": "/api/v1/cancelOrder"
  }
```

## CancelOrderService

* This API to cancel order by symbol.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type`   | `Content-Type: application/json`     |
| `Authorization`      | `Basic authenticate`     |
| `Url`                | `/api/v1/cancelOrder`     |
| `Method` | `POST`    |

### Request body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `orderId` | `Long`     | `Symbol` |
| `clientId` | `String`     | `Client Id` |
| `symbol` | `String`     | `Symbol` |

#### Example Curl

``` java
    curl --location 'http://localhost/api/v1/cancelOrder' \
    --header 'Content-Type: application/json' \
    --header 'Authorization: Basic {basic authenticate}' \
    --data '{
        "orderId" : "426265402",
        "clientId" : "",
        "symbol" : "BTC_THB"
    }'
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `orderId` | `String`     | `order Id` |
| `clientId` | `String`     | `client Id` |
| `symbol` | `String`     | `Symbol` |
| `side` | `String`     | `Side` |
| `type` | `String`     | `Type` |
| `quantity` | `BigDecimal`     | `Quanity` |
| `price` | `BigDecimal`     | `Price` |
| `status` | `String`     | `Status` |
| `timestamp` | `Date`     | `TimeStamp` |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `Not found.`               |
| `400`     | `no order to remove`       |
| `400`     | `This order is in processing.`       |
| `400`     | `This order is being processed.`       |
| `500`     | `Internal Error`           |

##### Example Success

```json
  {
    "orderId": "USDT",
    "clientId": "test",
    "symbol": 123.32,
    "side": 213,
    "type": "21232",
    "quantity": "21232",
    "price": "21232",
    "status": "21232",
    "timestamp": "21232",
  }
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "This order is being processed.",
    "path": "/api/v1/cancelOrder"
  }
```

## CancelAllOrderService

* This API to cancel all order.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `Authorization` | `Basic authenticate`     |
| `Url` | `/api/v1/cancelAllOrders`     |
| `Method` | `POST`     |

### Request body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `orderId` | `Long`     | `Symbol` |
| `clientId` | `String`     | `Client Id` |

#### Example Curl

``` java
    curl --location 'http://localhost/api/v1/cancelAllOrders' \
    --header 'Content-Type: application/json' \
    --header 'Authorization: Basic {basic authenticate}' \
    --data '{
        "orderId" : "426265402",
        "clientId" : "",
        "symbol" : "BTC_THB"
    }'
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `orderId` | `String`     | `order Id` |
| `clientId` | `String`     | `client Id` |
| `symbol` | `String`     | `Symbol` |
| `side` | `String`     | `Side` |
| `type` | `String`     | `Type` |
| `quantity` | `BigDecimal`     | `Quanity` |
| `price` | `BigDecimal`     | `Price` |
| `status` | `String`     | `Status` |
| `timestamp` | `Date`     | `TimeStamp` |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `Not found.`               |
| `400`     | `no order to remove`       |
| `400`     | `This order is in processing.`       |
| `400`     | `This order is being processed.`       |
| `500`     | `Internal Error`           |

##### Example Success

```json
  [
    {
        "orderId": "USDT",
        "clientId": "test",
        "symbol": 123.32,
        "side": 213,
        "type": "21232",
        "quantity": "21232",
        "price": "21232",
        "status": "21232",
        "timestamp": "21232"
    }, {
        "orderId": "USDT",
        "clientId": "test",
        "symbol": 123.32,
        "side": 213,
        "type": "21232",
        "quantity": "21232",
        "price": "21232",
        "status": "21232",
        "timestamp": "21232"
    }
  ]
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "This order is being processed.",
    "path": "/api/v1/cancelAllOrders"
  }
```

## GetAllOrderService

* This API to list all order.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `Authorization` | `Basic authenticate`     |
| `Url` | `/api/v1/allOrders`     |
| `Method` | `GET`     |

### Request body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `startTime` | `String`   | `stsrt time` |
| `endTime` | `String`     | `end time` |
| `symbols` | `String`     | `sysbol` |
| `limit`   | `Integer`    | `Limit` |

#### Example Curl

``` java
    curl --location 'http://localhost/api/v1/allOrders?startTime=1668916414000&endTime=1899916414000&symbols=XLM_THB%2C%20BTC_THB' \
    --header 'Authorization: Basic {basic authenticate}' \
    --data ''
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol`    | `String`      | `order Id`    |
| `orderId`   | `Long`        | `client Id`   |
| `clientId`  | `String`      | `Symbol`      |
| `price`     | `BigDecimal`  | `Side`        |
| `origQty`   | `BigDecimal`  | `Type`        |
| `executedQty` | `BigDecimal`| `Quanity`     |
| `side`      | `String`      | `Price`       |
| `status`    | `String`      | `Status`      |
| `time`      | `Date`        | `TimeStamp`   |
| `isWorking` | `Boolean`     | `TimeStamp`   |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `Not found.`               |
| `400`     | `no order to remove`       |
| `400`     | `This order is in processing.`       |
| `400`     | `This order is being processed.`       |
| `500`     | `Internal Error`           |

##### Example Success

```json
  [
    {
        "symbol": "USDT",
        "orderId": "test",
        "clientId": 123.32,
        "price": 213,
        "origQty": "21232",
        "executedQty": "21232",
        "side": "21232",
        "status": "21232",
        "time": "21232",
        "isWorking": "21232"
    },{
        "symbol": "USDT",
        "orderId": "test",
        "clientId": 123.32,
        "price": 213,
        "origQty": "21232",
        "executedQty": "21232",
        "side": "21232",
        "status": "21232",
        "time": "21232",
        "isWorking": "21232"
    }
  ]
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "This order is being processed.",
    "path": "/api/v1/cancelAllOrders"
  }
```

## OpenOrderService

* This API for open order.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `Authorization` | `Basic authenticate`     |
| `Url` | `/api/v1/allOrders`     |
| `Method` | `GET`     |

### Request body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbols` | `String`   | `symbols` |

#### Example Curl

``` java
  curl --location 'http://localhost/api/v1/openOrder?symbols=XRP_THB' \
  --header 'Authorization: Basic ={basic authenticate}' \
  --data ''
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol`    | `String`      | `order Id`    |
| `orderId`   | `Long`        | `client Id`   |
| `clientId`  | `String`      | `Symbol`      |
| `price`     | `BigDecimal`  | `Side`        |
| `origQty`   | `BigDecimal`  | `Type`        |
| `executedQty` | `BigDecimal`| `Quanity`     |
| `side`      | `String`      | `Price`       |
| `status`    | `String`      | `Status`      |
| `time`      | `Date`        | `TimeStamp`   |
| `isWorking` | `Boolean`     | `TimeStamp`   |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `Not found.`               |
| `400`     | `no order to remove`       |
| `400`     | `This order is in processing.`       |
| `400`     | `This order is being processed.`       |
| `500`     | `Internal Error`           |

##### Example Success

```json
  [
    {
        "symbol": "USDT",
        "orderId": "test",
        "clientId": 123.32,
        "price": 213,
        "origQty": "21232",
        "executedQty": "21232",
        "side": "21232",
        "status": "21232",
        "time": "21232",
        "isWorking": "21232"
    },{
        "symbol": "USDT",
        "orderId": "test",
        "clientId": 123.32,
        "price": 213,
        "origQty": "21232",
        "executedQty": "21232",
        "side": "21232",
        "status": "21232",
        "time": "21232",
        "isWorking": "21232"
    }
  ]
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "This order is being processed.",
    "path": "/api/v1/cancelAllOrders"
  }
```
