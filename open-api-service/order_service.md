# Place Order Service

## Overview

This API is provide information of trading.  

## Table of contents

* [Place Order Service](#placeorderservice)
* [Get Order Service](#getorderservice)
* [Cancel Order Service](#cancelorderservice)
* [Cancel All Order Service](#web-socket-api-documentation)
* [Get All Order Service](#stream-demo)
* [Open Order Service](#live-order-book)

## PlaceOrderService

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

* This API to cancel order.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `Authorization` | `Basic authenticate`     |
| `Url` | `/api/v1/cancelOrder`     |
| `Method` | `POST`     |

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
