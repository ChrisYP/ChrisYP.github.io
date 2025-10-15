------

[`返回首页`](../README.md)    [`上一页`](aws.md)   [`下一页`](kasada.md)    [`English Version`](../en-US/perimeterx.md)

## PerimeterX

### 价格说明
* 按压模式消耗 `1000` 点, 需要传入 `app_id`、`href`、`captcha`

### 说明

* 参数调用非常复杂，强烈建议直接使用 `pynocaptcha`，详情看下面 python 示例！！！

* 当看到 `cookies` 中有 `_px2`、`_px3` 时, 代表存在 `perimeterx` 验证, 有以下三种情况
    * `仅无感模式（*/api/v2/colletor）`: 打开目标页面, 没有出现任何验证, f12 中不停发送 `*/api/v2/colletor` 接口, 该模式必须传 `app_id`、`href`、`proxy`
    ![验证接口](/images/perimeterx/1.png)
    * `首页无感＋按压模式（*/assets/js/bundle）`: 打开目标页面, 直接出现按压验证码, 该模式必须传 `tag`、`href`、`proxy` 接口
    ![验证接口](/images/perimeterx/1.png)
    * `xhr 按压验证模式（*/assets/js/bundle）`: 打开目标页面, 未直接出现按压验证码, 在点击登录、注册或者搜索等关键接口出现按压验证码, 该模式必须传 `app_id`、`href`、`captcha`、`proxy`
    ![验证接口](/images/perimeterx/3.png)
    ![按压验证码样例](/images/perimeterx/2.png)

ps: 
    * 无感模式跟首页按压模式通常取决于你的代理质量, 如果你直接使用`无感模式`, 可能拿到的 `_px2`、`_px3` cookie 还是会继续触发 `首页按压验证模式`, 若继续出现 `首页按压模式`, 则说明你的代理不能直接使用 `无感模式`, 请转而使用 `首页按压模式`
    * 按压模式返回的 `_px2`、`_px3` 通常需要过个几秒才能正常使用, 马上用可能还是 403
    * 建议先挂代理请求你的目标页面判断状态码是不是 `403`, 如果是 `403`, 说明你当前代理会触发按压模式, 按 `首页无感＋按压模式（*/assets/js/bundle）` 模式传参, 如果不是 `403`（正常进入当前页面, 状态码 `200` 或者 `302` 之类的）, 那么说明你的代理请求当前页面触发的是 `无感模式`, 按 `无感模式` 传参即可

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `通用版（universal）` | `http://api.nocaptcha.io/api/wanda/perimeterx/universal` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `触发 perimeterx 验证的页面地址`    | `是` |
| `tag`        | `String`  | `版本号, */api/v2/colletor 或者 */assets/js/bundle 中的 tag 参数（不传 tag 就必须传 app_id）`    | `否` |
| `app_id`        | `String`  | `*/api/v2/colletor 或者 */assets/js/bundle 中的 appId 参数（PX开头的, 不传 app_id 就必须传 tag`    | `否` |
| `captcha`    | `Object`  | `验证码参数, xhr 接口返回的按压验证码必传`    | `否` |
| `captcha_html`    | `String`  | `验证码参数, 请求 href 返回的按压验证码的响应源码`    | `否` |
| `uuid`    | `String`  | `window._pxUuid`    | `否` |
| `vid`    | `String`  | `window._pxVid`    | `否` |
| `proxy`    | `String`  | `无需保持代理一致, 若传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `否` |
| `did` | `String`  | `无感模式返回的指纹 id（存在 extra 属性中）, 后续 xhr 接口出现的按压验证码请传该参数`       | `否` |
| `country`    | `String`  | `业务流程使用的代理所属地区国家 code, 如美国（us）、英国（uk）, 详情可咨询管理`    | `否` |
| `ip`    | `String`  | `业务流程使用的代理流程的 ip 地址（例: 56.214.78.94）, 详情可咨询管理`    | `否` |
| `user_agent` | `String`  | `自定义 user_agent, 请传最新版 windows ua`       | `否` |
| `cookies` | `String`  | `按压验证码模式下, 当前页面的 cookies`       | `否` |
| `actions` | `Integer`  | `随机行为次数, 越大耗时越久, 风控高的站点可以设置大一点, 默认 1`       | `否` |
| `timeout` | `Integer`  | `验证超时时间`       | `否` |

#### json 示例

##### 仅无感模式
```
{
    "app_id": "PXu6b0qd2S",
    "href": "https://www.walmart.com/",
    "proxy": "user:pass@ip:port",
}
```

##### 无感＋按压模式（打开目标页面直接弹按压验证码）
```
{
    "tag": "v8.6.6",
    "href": "https://www.walmart.com/",
    "proxy": "user:pass@ip:port",
}
```

##### xhr 接口返回的纯按压验证码

`captcha`: 如果触发接口直接返回 `json` 数据格式, 直接将返回的 `json` 数据传递成 `captcha` 参数即可, 如下图所示:

![xhr 按压验证码](/images/perimeterx/4.png)

```
{
    "app_id": "PXaOtQIWNf",
    "href": "https://www.chegg.com/auth?action=login&redirect=https%3A%2F%2Fwww.chegg.com%2Ftextbooks%2Fstudent-solutions-manual-chapters-1-11-for-stewart-s-single-variable-calculus-8th-edition-9781305271814-1305271815%3Ftrackid%3D74b04883b359%26strackid%3Db48a54386409%26searchid%3Db06489ae-fb76-4dc5-8d8e-dae3ce250966",
    "captcha": {
        "appId": "PXaOtQIWNf",
        "jsClientSrc": "/aOtQIWNf/init.js", 
        "firstPartyEnabled": true, 
        "uuid": "bd2deef7-0b95-11ef-8c49-cb4c98cbe205", 
        "hostUrl": "/aOtQIWNf/xhr", 
        "blockScript": "/aOtQIWNf/captcha/captcha.js?a=c&u=bd2deef7-0b95-11ef-8c49-cb4c98cbe205&v=&m=0", 
        "altBlockScript": "https://captcha.px-cloud.net/PXaOtQIWNf/captcha.js?a=c&u=bd2deef7-0b95-11ef-8c49-cb4c98cbe205&v=&m=0", 
        "customLogo": "https://chegg-mobile-promotions.cheggcdn.com/px/Chegg-logo-79X22.png"
    },
    "did": "无感模式返回的 did",
    "proxy": "user:pass@ip:port",
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
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "2635.12ms",
  "data": {
    "cookies": {
        "_px3": "eb9fb4aab8cbd8d9c7018d0928bdccd972ef2a879383dec6b8999bca90ef4fdd:0r5KU/5t6VOMgwq7DnwmGd246hJVZbhPeI72OXfd8QSyRuK1hBRSBog3nrfQah8dLHd5X7cJZJnydq09AginIw==:1000:7eMdz1/BzkA4xQ8/rxujv5jsju6W1PbCAAp+gNDX8fox23jXH2mvzBzg0IwYLDX576aAHr3TeWqHFWvutnqxAKgTSIyR8cutzM7CG6zHQSV0N8piaWjjXlozbaWh77V3BGC7EZ/e3Rj3cbhl9Z4bufg6/87I91c7vv3Ka4ewGi+9EkKABRSCjAs4wEJYu6SneH1ZiiQAWVRW/EAULvFKJpxC07/qpxYuCblvaPljf14=", 
        "_pxde": "9a14782e5832ac4ba515c98e3e9f6b6e7b2e3d8ecb36320e659f85bb4f7359ac:eyJ0aW1lc3RhbXAiOjE3MTE2ODA3MDcyNzd9", 
        "pxcts": "48247186-ed77-11ee-8c23-8bccbc7b0e91"
        "_pxvid": "bcc357c3-ed78-11ee-aaf0-a24906ed7b54",
        "_pxde": "370c1218665b160f442e1e2b63603a15b046b7831b83de27de7c5211bf102f77:eyJ0aW1lc3RhbXAiOjE3MTE2ODI5NTE5MzZ9"
    }
  }
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
from utils import USER_TOKEN, get_idea_proxy
from pynocaptcha import magneto, crack_perimeterx


def parse_index(resp, extra):
    extra["csrf_token"] = re.search(
        r'name="csrf_token" value="(.*?)"', resp.text
    )[1]


def checkbalance(session: magneto.Session, extra):
    headers = {
        'sec-ch-ua-platform': extra['sec-ch-ua-platform'], 
        'x-requested-with': 'XMLHttpRequest',
        'user-agent': extra['user-agent'],
        'accept': 'application/json, text/javascript, */*; q=0.01',
        'sec-ch-ua': extra['sec-ch-ua'],
        'content-type': 'application/x-www-form-urlencoded; charset=UTF-8',
        'sec-ch-ua-mobile': '?0',
        'Origin': 'https://www.columbia.com', 
        'Sec-Fetch-Site': 'same-origin', 
        'Sec-Fetch-Mode': 'cors',
        'Sec-Fetch-Dest': 'empty', 
        'Referer': 'https://www.columbia.com/giftcards/', 
        'Accept-Encoding': 'gzip, deflate, br, zstd',
        'Accept-Language': extra['accept-language'], 
        'priority': 'u=1, i'
    }

    data = {
        'giftCertID': '8554515151515155454',
        'giftCertPin': '1541',
        'csrf_token': extra["csrf_token"]
    }

    return session.post(
        'https://www.columbia.com/on/demandware.store/Sites-Columbia_US-Site/en_US/GiftCard-CheckBalance',
        headers=headers,
        data=data,
    )


session, resp, extra = crack_perimeterx(
    USER_TOKEN,
    href='https://www.columbia.com/giftcards/',
    app_id='PXLkXIE7Oj',
    proxy=get_idea_proxy("hk"),
    parse_index=parse_index,
    verifiers=[
        checkbalance
    ]
)
print(resp.status_code, resp.text)
```
