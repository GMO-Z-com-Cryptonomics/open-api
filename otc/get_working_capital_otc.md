# Working Capital Service  <span style="font-size: 0.8em;">[🚀](../Readme.md#software-development-api-documents)</span>

## Overview
This API to provide information of the working capital.

##### Note :
    Please contact admin to generate x-api-key.

#### Available USDT working Capital

##### Request Header
| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `x-api-key`     |
| `Method` | `GET`     |
| `Domain` | `https://open-api.ex.z.com` |
| `Url` | `/api/v1/working-capital?symbol=USDT`     |
| `Param` | `Symbol : USDT`     |


##### Request Body
``` curl
curl --location 'https://open-api.ex.z.com/api/v1/working-capital?symbol=USDT' \
--header 'x-api-key: {x-api-key}'
```

##### Example success
``` json
    {
        "availableBalance": 155781697.759302685923120000,
        "withdrawBankAccounts": null
    }
```

##### Example fail bad request
``` json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "symbol not support : TH",
    "instance": "/api/v1/working-capital"
}
```

##### Response code
| code | Message |
| :------ | :------- |
| `200`   |   `Success` |
| `401` | `Unauthorize` |
| `400` | `Bad Request` |

#### Available THB working Capital

##### Request Header
| Parameter | Type     |
| :-------- | :------- |
| `Application Type` | `Content-Type: application/json`     |
| `x-api-key` | `x-api-key`     |
| `Method` | `GET`     |
| `Domain` | `https://open-api.ex.z.com` |
| `Url` | `/api/v1/working-capital?symbol=THB`     |
| `Param` | `Symbol : THB`     |

##### Request body
``` curl

curl --location 'https://open-api.ex.z.com/api/v1/working-capital?symbol=THB' \
--header 'x-api-key: {x-api-key}'
```

##### Example success
``` json
    {
        "availableBalance": 155781697.759302685923120000,
        "withdrawBankAccounts": null
    }
```

##### Example bad request
``` json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "symbol not support : TH",
    "instance": "/api/v1/working-capital"
}
```

##### Response code
| code | Message |
| :------ | :------- |
| `200`   |   `Success` |
| `401` | `Unauthorize` |
| `400` | `Bad Request` |