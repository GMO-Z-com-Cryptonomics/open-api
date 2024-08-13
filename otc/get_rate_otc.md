# OTC Rate Service  <span style="font-size: 0.8em;">[🚀](../Readme.md#software-development-api-documents)</span>

## Overview
This api to provide information rate of side buy and sell of otc.

##### Note
 Please contact admin to generate x-api-key to use this API.

#### GET RATE SIDE SELL
```
curl --location '{{domian}}/api/v1/rate?side=SELL' \
--header 'x-api-key: {{x-api-key}}'
```

#### GET RATE SIDE BUY
```
curl --location '{{x-api-key}}/api/v1/rate?side=BUY' \
--header 'x-api-key: {{x-api-key}}'
```

##### Example
``` json
    {
        "otcPriceId": 3651411,
        "symbol": "USDT_THB",
        "side": "BUY",
        "price": 36.71,
        "spread": 0.01,
        "createdAt": "2024-08-13T04:44:57.000+00:00"
    }
```

``` json
    {
        "otcPriceId": 3651430,
        "symbol": "USDT_THB",
        "side": "SELL",
        "price": 36.14,
        "spread": 0.01,
        "createdAt": "2024-08-13T04:45:54.000+00:00"
    }
```

##### Example bad request
``` json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "{\"message\":\"Unknown side: SEL\",\"timestamp\":\"2024-08-13T13:53:41.99352743\"}",
    "instance": "/api/v1/rate"
}
```

#### Http Response code
| code | Description |
| :------ | :------- |
| 200   |   Success |
| 401 | Unauthorize |
| 400 | Bad request |