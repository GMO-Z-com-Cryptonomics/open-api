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
| `x-api-key` | `x-api-key`     |
| `x-api-signature` | `signature` |
| `Url` | `/api/v1/order`     |
| `Method` | `POST`     |

### Request body

| Parameter | Type     | Mandatory | Description                |
| :-------- | :------- | :-------- | :------------------------- |
| `symbol` | `String`  | Mandatory | `Symbol as such BTC_THB` |
| `side` | `String`    | Mandatory |`Side as such BUY, SELL` |
| `quantity` | `BigDecimal` | Mandatory  | `Quanity` |
| `price` | `BigDecimal`    | Mandatory  | `Price` |
| `clientId` | `String`     | Optional   | ` - ` |

#### Example

``` java
  curl --location '{domain_url}/api/v1/order' 
  --header 'x-api-key: {api-key}' 
  --header 'x-api-signature: {signature}' 
  --header 'Content-Type: application/json' 
  --data '{
      "symbol":"BTC_THB",
      "side": "BUY",
      "quantity": 0.01,
      "price": 16009.266,
      "clientId":"test_01"
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

| Http Code | Message                |  Descritpions  |
| :-------- | :------------------------- |  :---------------------  |
| `200`     | `Success`                  |  Place order success     |
| `400`     | `Not found symbol instant.` | Not found symbol in server. | 
| `400`     | `Incorrect side.` | Side should be BUY or SELL. | 
| `400`     | `Incorrect quantity`   |  Should be BigDecimal value ex : 0.01  | 
| `400`     | `Price must be positive number` | Should be BigDecimal value ex : 11213.003 |
| `400`     | `DUPLICATE_CLIENT_ORDER_ID` | User Id already place order. | 
| `400`     | `You have placed order more than 10 at the same location` | when you have placed order more than 10 at the same location |
| `400`     | `Price you have input has too much gap of the current price, please try again` | when Price you have input has too much gap of the current price, please try again |
| `400`     | `coin Pair trading status not fetched, feign client not called` | when coin Pair trading status not fetched, feign client not called | 
| `400`     | `Wallet not found` |  Not found user wallet. |
| `400`     | `Insufficient Wallet Balance` |  User balance not enough. |
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
    "message": "Insufficient Wallet Balance.",
    "path": "/api/v1/order"
  }
```

## GetOrderService
- This service to providing about order data it will return all of order follow symbol.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `api-key`     |
| `Url` | `/api/v1/order`     |
| `Method` | `GET`     |

### Request parameter

| Parameter | Type     | Mandatory | Description                |
| :-------- | :------- | :-------- | :------------------------- |
| `symbol` | `String`     |  `Mandatory` | Symbol |
| `orderId` | `String`     | `Mandatory` | OrderId can be null but clientId is not null |
| `clientId` | `BigDecimal`     | `Mandatory` | ClientId can be null but orderId is not null. |

#### Example Curl

``` java
  curl --location '{domain_url}/api/v1/order?symbol=BTC_THB&clientId=1231&orderId=2131' 
  --header 'x-api-key: {x-api-key}'
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

| Http Code | Message                |  Descriptions  |
| :-------- | :------------------------- | :-------- |
| `200`     | `Success`                  |  Success |
| `400`     | `Required parameter 'symbol' is not present.` |  Symbol is Null |
| `400`     | `orderId or clientId is required.` |  OrderId and ClientId some value not null. |
| `400`     | `Not found.`   |  Not found data in market data |

##### Example Success

```json
  {
    "symbol": "XLM_THB",
    "orderId": 510229768,
    "clientId": "test_02",
    "price": 4.200000000000000000,
    "origQty": 200000.000000000000000000,
    "executedQty": 0E-18,
    "side": "BUY",
    "status": "QUEUED",
    "time": "2024-01-29T06:41:09.000+00:00",
    "isWorking": true
  }
```

##### Example code 400, 500

``` Json
  {
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "Required parameter 'symbol' is not present.",
    "instance": "/api/v1/order"
  }
```

## CancelOrderService

* This API to cancel order by symbol.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type`   | `Content-Type: application/json`     |
| `x-api-key`      | `api-key`     |
| `x-api-signature`      | `signature-key`     |
| `Path`                | `/api/v1/cancelOrder`     |
| `Method` | `POST`    |

### Request body

| Parameter | Type     |  Mandatory  | Description                |
| :-------- | :------- |  :--------  | :------------------------- |
| `orderId` | `Long`     |  `Mandatory`  | `Symbol` |
| `clientId` | `String`   | `Optional`  | `Client Id` |
| `symbol` | `String`     | `Optional` | `Symbol` |

#### Example Curl

``` java
    curl --location '{domain_url}/api/v1/cancelOrder' 
    --header 'x-api-key: {api-key}' 
    --header 'x-api-signature: {signature-key}' 
    --header 'Content-Type: application/json' 
    --data '{
        "symbol":"BTC_THB",
        "orderId": "1234",
        "clientId":"test_1"
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

| Http Code | Message                |  Description  |
| :-------- | :------------------------- | :------   |
| `200`     | `Order Successfully removed` |  Success  |
| `400`     | `Not found symbol instant.`|  Not found symbol in server  |
| `400`     | `orderId or clientId is required.`|   OrderId and ClientId is null  |
| `400`     | `no order to remove`       |  Not found order to remove  |
| `400`     | `This order is in processing.`       |  Order is processing  |
| `400`     | `This order is being processed.`       |  This order is being processed.  |
| `400`     | `Failed to return balance after cancelling order.`  | Failed to return balance after cancelling order. |

##### Example Success

```json
  {
    "orderId": "1111",
    "clientId": "1234",
    "symbol": "BTC_THB",
    "side": "BUY",
    "type": "",
    "quantity": 0.01,
    "price": 16009.266,
    "status": "PENDING",
    "timestamp": "1706150442000",
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
| `x-api-key` | `{api_key}`     |
| `x-api-signature` | `{signature}`     |
| `Path` | `/api/v1/cancelAllOrders`     |
| `Method` | `POST`     |

### Request body

| Parameter | Type     | Mandatory | Description                |
| :-------- | :------- | :---------- | :------------------------- |
| `orderId` | `Long`   | `Mandatory`  | `Symbol` |
| `clientId` | `String` | `Optional`    | `Client Id` |

#### Example Curl

``` java
    curl --location '{domain_url}/api/v1/cancelAllOrders' \
    --header 'Content-Type: application/json' \
    --header 'x-api-key: {Api_key}' \
    --header 'x-api-signature: {Signature}' \
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

| Http Code | Message                |  Description |
| :-------- | :------------------------- | :------------- |
| `200`     | `Success`                  | Cancel success. |
| `400`     | `Not found symbol instant.`               | Not found symbol server. |
| `400`     | `no order to remove`       | Not found symbol for remove. |
| `400`     | `Could not cancel order. Order does not belong to the logged in user.`       |  Could not cancel order. Order does not belong to the logged in user.  |

##### Example Success

```json
  [
    {
        "orderId": "001",
        "clientId": "test_01",
        "symbol": "BTC_THB",
        "side": "BUY",
        "type": "",
        "quantity": 0.01,
        "price": 16543.001,
        "status": "PENDING",
        "timestamp": "21232"
    }, {
        "orderId": "002",
        "clientId": "test_02",
        "symbol": "BTC_THB",
        "side": "BUY",
        "type": "",
        "quantity": 0.01,
        "price": 165434.001,
        "status": "PENDING",
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
    "message": "Not found symbol for remove.",
    "path": "/api/v1/cancelAllOrders"
  }
```

## GetAllOrderService

* This API to list all order.

### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `zpi-key`     |
| `Path` | `/api/v1/allOrders`     |
| `Method` | `GET`     |

### Request body

| Parameter | Type     | Mandatory | Description                |
| :-------- | :------- | :-------- | :------------------------- |
| `startTime` | `String`  | `Optinal` | `stsrt time` |
| `endTime` | `String`    | `Optinal` | `end time` |
| `symbols` | `String`    | `Optinal` | `sysbol` |
| `limit`   | `Integer`   | `Optinal` | `Limit` |

#### Example Curl

``` java
    curl --location '{domain_url}/api/v1/allOrders?startTime=1668916414000&endTime=1899916414000&symbols=XLM_THB%2C%20BTC_THB' \
    --header 'x-api-key: api-key' \
    --data ''
```

### Response Body

| Parameter | Type     | Description                |
| :-------- | :------- | :------------------------- |
| `symbol`    | `String`      | `symbol`    |
| `orderId`   | `Long`        | `order Id`   |
| `clientId`  | `String`      | `client Id`      |
| `price`     | `BigDecimal`  | `price`        |
| `origQty`   | `BigDecimal`  | `original quanity`        |
| `executedQty` | `BigDecimal`| `execute quanity`     |
| `side`      | `String`      | `BUY or SELL`       |
| `status`    | `String`      | `status`      |
| `time`      | `Date`        | `TimeStamp`   |
| `isWorking` | `Boolean`     | `woring flag`   |

#### Status code

| Http Code | Description                |
| :-------- | :------------------------- |
| `200`     | `Success`                  |
| `400`     | `Not found.`               |
| `400`     | `StartTime must value must be in unix time stamp milliseconds`       |
| `400`     | `EndTime must value must be in unix time stamp milliseconds`       |
| `400`     | `startTime must be before endTime`       |

##### Example Success

```json
  [
    {
        "symbol": "BTC_THB",
        "orderId": "001",
        "clientId": "test_01",
        "price": 165473.012,
        "origQty": 0.01,
        "executedQty": 0.01,
        "side": "SELL",
        "status": "PENDING",
        "time": "212322123",
        "isWorking": "true"
    },{
        "symbol": "BTC_THB",
        "orderId": "002",
        "clientId": "test_02",
        "price": 165473.012,
        "origQty": 0.01,
        "executedQty": 0.01,
        "side": "SELL",
        "status": "PENDING",
        "time": "212322123",
        "isWorking": "true"
    }
  ]
```

##### Example code 400, 500

``` Json
  {
    "timestamp": "2023-12-05T14:18:15.076+00:00",
    "status": 400,
    "error": "Bad Request",
    "message": "startTime must be before endTime.",
    "path": "/api/v1/allOrders"
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
