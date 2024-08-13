# Wokring Capital Service  <span style="font-size: 0.8em;">[🚀](../Readme.md#software-development-api-documents)</span>

## Overview
This API to provide information of the working capital.

##### Note :
    Please contact admin to generate x-api-key.

##### Working Capital Coin
Request body
``` curl
curl --location 'https://open-api.exchange-staging.z.com/api/v1/working-capital?symbol=USDT' \
--header 'x-api-key: user2'
```

##### Working Capital Amount balance
Request body
``` curl
curl --location 'https://open-api.exchange-staging.z.com/api/v1/working-capital?symbol=THB' \
--header 'x-api-key: user2'
```

##### Example success
``` json
    {
        "availableBalance": 155781697.759302685923120000,
        "withdrawBankAccounts": null
    }
```

##### Example Bad request
``` json
{
    "type": "about:blank",
    "title": "Bad Request",
    "status": 400,
    "detail": "symbol not support : TH",
    "instance": "/api/v1/working-capital"
}
```

##### Http Response code
| code | Description |
| :------ | :------- |
| 200   |   Sucess |
| 401 | Unauthorize |
| 400 | Bad Request |