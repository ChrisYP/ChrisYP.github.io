------
[`Back to Home`](../README.md)    [`Previous`](discord_join_channel.md)    [`English Version`](../en-US/unlocker.md)

## SiteUnlocker

### Description
* `SiteUnlocker Definition`: A full-process implementation for specific businesses on specific websites. It completely eliminates the need to consider the integration and invocation of various shields. You only need to pass parameters according to our defined action and params to get the response data from the target business interface.
* Many websites use shields (e.g., `akamai`, `kasada`, `datadome`, `shape`, `perimeterx`, etc.) whose integration and invocation are complex, coupled with other protective measures (e.g., `ja3`, `http2` fingerprint detection). Simply obtaining the parameters returned by our interface does not guarantee successful verification. It's possible to get the parameters from our interface but still receive a verification failure when actually calling the target interface, resulting in charges without obtaining the desired data. The Unlocker perfectly solves this problem. Users don't need to worry about which shields are bypassed, how to integrate these shields, or how the business process should be written, etc. They only need to integrate the Unlocker interface effortlessly. Charges are only incurred if the correct target interface response is obtained; otherwise, no charges are applied (e.g., if parameters are unusable).
* Site Unlockers for dozens of websites are currently supported. Contact the administrator for specific details.
* This interface supports usage packages (the more uses, the cheaper the price). Prices vary slightly depending on the difficulty of the website. Contact the administrator for specific details.

### Request URL（POST）:

| Version               | Endpoint URL                                                   |
|------------------|---------------------------------------------------------|
| `v1` | `http://api.nocaptcha.io/api/wanda/site/unlocker` |

### Request Headers:

| Parameter Name            | Description                                                                         | Required  |
|----------------|----------------------------------------------------------------------------|-----|
| `User-Token`   | `User secret, get from homepage`                                                               | `Yes` |
| `Content-Type` | `application/json`                                                         | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)` | `No` |

### POST Data（JSON）:

| Parameter Name | Description                                                                                                                          | Required |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `Target business website URL: e.g., https://www.starbucks.com/`    | `Yes` |
| `action`        | `String`  | `The defined action for the current website on the interface`    | `Yes` |
| `params`        | `Object`  | `	Parameters for the target interface. Consult the administrator for specifics`    | `Yes` |
| `user_agent` | `String`  | `Custom user_agent. Please use Chrome UA from version 115 to the latest`       | `No` |
| `proxy`    | `String`  | `Format: ip:port or usr:pwd@ip:port (Contact the administrator if there are issues)` | `No` |

#### JSON Example

```
{
    "href": "https://www.att.com/",
    "action": "order_flow",
    "params": {
        'imei': 'xxxx'
    }
}
```

### Response Data（JSON）:

#### Successful Response

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data`   | `String`  | `Target business interface response`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```
{
    "status": 1,
    "msg": "验证成功",
    "en_msg": "Verify success",
    "id": "b4f3e37c-78d1-4993-873c-9a0cbe2e48d8",
    "cost": "12860.88ms",
    "data": {
        "error": {
            "errorId": "UNLOCK406",
            "errorMessage": "Order Flow Validation Failed",
            "details": [
                {
                    "code": "ULS_8023"
                }
            ]
        }
    },
    "extra": {}
}
```

### Usage Example

#### Python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python

import re

# get the User-Token from www.nocaptcha.io
from utils import USER_TOKEN

from pynocaptcha import run_unlocker
result = run_unlocker(user_token=USER_TOKEN, site='www.att.com', action='order_flow', params={
    'imei': 'xxx'
})
print(result)

from pynocaptcha import Unlocker, LululemonCheckBalanceParams
unlocker = Unlocker(user_token=USER_TOKEN, timeout=120)
result = unlocker.lululemon_checkbalance(LululemonCheckBalanceParams(
    cardNumber='xxxx',
    pin='xxxx'
))
print(result)

import random
from pynocaptcha import Unlocker, PrizepicksLoginParams

unlocker = Unlocker(user_token=USER_TOKEN, timeout=120)
result = unlocker.prizepicks_login(PrizepicksLoginParams(
    email=f'jkutz21{random.randint(100, 10000)}@gmail.com',
    password=f'Jake8{random.randint(100, 10000)}!'
))
print(result)

from pynocaptcha import Unlocker, WizzairSearchParams, FlightSegment

unlocker = Unlocker(user_token=USER_TOKEN)
result = unlocker.wizzair_search_flights(WizzairSearchParams(
    adultCount=1,
    childCount=0,
    flightList=[
        FlightSegment(
            arrivalStation="LCA",
            departureStation="EVN",
            departureDate="2025-10-25T00:00:00",
        ), FlightSegment(
            arrivalStation="EVN",
            departureDate="2025-10-27T00:00:00",
            departureStation="LCA"
        )
    ],
    infantCount=0,
    isFlightChange=False,
    wdc=True
))
print(result)

# etc.
```
