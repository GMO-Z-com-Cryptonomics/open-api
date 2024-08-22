# OTC Rate Service  <span style="font-size: 0.8em;">[🚀](../Readme.md#software-development-api-documents)</span>

## Overview
This api to provide information rate of side buy and sell of otc.

##### Note
```
    Please contact admin to generate x-api-key to use this API.
```

### GET RATE SIDE SELL

##### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `x-api-key`     |
| `Method` | `GET`     |
| `Domain` | `https://open-api.ex.z.com` |
| `Url` | `/api/v1/rate?side=SELL`     |
| `Param` | `Side = SELL`     |

##### Request Body
```
curl --location 'https://open-api.ex.z.com/api/v1/rate?side=SELL' \
--header 'x-api-key: {{x-api-key}}'
```

##### Example response SELL side
``` json
    {
        "otcPriceId": 3651430,
        "symbol": "USDT_THB",
        "side": "SELL",
        "price": 36.14,
        "createdAt": "2024-08-13T04:45:54.000+00:00"
    }
```

##### Example resposne fail Bad Request
``` json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "{\"message\":\"Unknown side: SEL\",\"timestamp\":\"2024-08-13T13:53:41.99352743\"}",
    "instance": "/api/v1/rate"
}
```
##### Response Body
| Field | Description     |
| :-------- | :------- |
| `otcPriceId` | `Id of otc price`     |
| `symbol` | `symbol`     |
| `side` | `side of rate`     |
| `price` | `price otc rate` |
| `createdAt` | `date of otc price`     |

##### Response Code
| `Code` | `Message`     |
| :-------- | :------- |
| `200`   |   `Success` |
| `401` | `Unauthorize` |
| `400` | `Bad request` |

### GET RATE SIDE BUY

##### Request header

| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `x-api-key`     |
| `Method` | `GET`     |
| `Domain` | `https://open-api.ex.z.com` |
| `Url` | `/api/v1/rate?side=BUY`     |
| `Param` | `Side = BUY`     |

##### Request Body
```
curl --location 'https://open-api.ex.z.com/api/v1/rate?side=BUY' \
--header 'x-api-key: {{x-api-key}}'
```

##### Example response BUY side
``` json
    {
        "otcPriceId": 3651411,
        "symbol": "USDT_THB",
        "side": "BUY",
        "price": 36.71,
        "createdAt": "2024-08-13T04:44:57.000+00:00"
    }
```

##### Example resposne Bad Request
``` json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "{\"message\":\"Unknown side: BU\",\"timestamp\":\"2024-08-13T13:53:41.99352743\"}",
    "instance": "/api/v1/rate"
}
```

##### Response Body
| Field | Description     |
| :-------- | :------- |
| `otcPriceId` | `Id of otc price`     |
| `symbol` | `symbol`     |
| `side` | `side of rate`     |
| `price` | `price otc rate` |
| `createdAt` | `date of otc price`     |

##### Response code

| `Code` | `Message`     |
| :-------- | :------- |
| `200`   |   `Success` |
| `401` | `Unauthorize` |
| `400` | `Bad request` |