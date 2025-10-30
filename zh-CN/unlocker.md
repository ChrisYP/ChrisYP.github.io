------
[`返回首页`](../README.md)    [`上一页`](discord_join_channel.md)    [`English Version`](../en-US/unlocker.md)

## SiteUnlocker

### 说明
* 解锁器定义：针对具体网站具体业务的全流程实现，，完全不需要考虑各种盾的接入调用，只需要按照我们定义的 `action` 跟 `params` 传参即可获取目标业务的接口响应数据
* 很多网站使用的盾（比方说 `akamai`、`kasada`、`datadome`、`shape`、`perimeterx` 等）接入调用较为复杂，而且还有其他的一些防护措施（比方说 `ja3`、`http2` 指纹检测），并不是拿到我们接口返回的参数就能成功通过验证，有可能获取到了我们接口返回的参数，但是实际用到目标接口时却返回验证失败，扣了钱却没有获取到想要的数据，解锁器就可以完美解决这个问题，用户不需要管过哪些盾、应该如何接入这些盾、业务流程应该如何写等等，只需要无脑接入解锁器接口，只有获取到了正确的目标接口响应才会扣钱，否则不会扣钱（比方说参数不可用）
* 目前已支持几十个网站的业务解锁器，具体联系管理员了解详情
* 该接口支持次数包（次数越多越便宜），不同网站根据难度不同价格也有细微差别，具体联系管理员了解详情

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `v1` | `http://api.nocaptcha.io/api/wanda/site/unlocker` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `目标业务网站地址：如 https://www.starbucks.com/`    | `是` |
| `action`        | `String`  | `接口定义的当前网站的 action`    | `是` |
| `params`        | `Object`  | `目标接口的传参, 具体咨询管理员`    | `是` |
| `user_agent` | `String`  | `自定义 user_agent, 请传 115 ~ 最新版本的 chrome ua`       | `否` |
| `proxy`    | `String`  | `无需保持代理一致, 若传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `否` |

#### json 示例

```
{
    "href": "https://www.att.com/",
    "action": "order_flow",
    "params": {
        'imei': 'xxx'
    }
}
```

### Response Data（JSON）:

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.cookies`   | `String`  | `验证通过返回的可用的 _px2、_px3 cookie, 可用于后续验证接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

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

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python

import re

# 访问 www.nocaptcha.io 官网获取 User-Token
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
    cardNumber='xxxxx',
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
