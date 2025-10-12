[`Back to Home`](en.md)    [`Previous`](aws.md)   [`Next`](kasada.md)    [`中文文档`](../zh-CN/perimeterx.md)

## PerimeterX

### Pricing
* Press mode consumes `1000` points, requires `app_id`, `href`, `captcha`

### Description
* Parameter invocation is very complex, strongly recommend using `pynocaptcha` directly, see the python example below!!!
* When you see `_px2`, `_px3` in cookies, it means `perimeterx` verification exists, with three cases:
    * Sense-only mode (`*/api/v2/colletor`): Open the target page, no verification appears, f12 keeps sending `*/api/v2/colletor` requests, this mode must pass `app_id`, `href`, `proxy`
    ![Verification API](/images/perimeterx/1.png)
    * Homepage sense + press mode (`*/assets/js/bundle`): Open the target page, press captcha appears directly, this mode must pass `tag`, `href`, `proxy`
    ![Verification API](/images/perimeterx/1.png)
    * xhr press verification mode (`*/assets/js/bundle`): Open the target page, no press captcha appears directly, but appears on login, register, or search key APIs, this mode must pass `app_id`, `href`, `captcha`, `proxy`
    ![Verification API](/images/perimeterx/3.png)
    ![Press captcha sample](/images/perimeterx/2.png)

ps:
    * Sense-only mode and homepage press mode usually depend on your proxy quality. If you use sense-only mode directly, the `_px2`, `_px3` cookies you get may still trigger homepage press verification mode. If you keep seeing homepage press mode, your proxy cannot use sense-only mode, please switch to homepage press mode.
    * The `_px2`, `_px3` cookies returned by press mode usually need a few seconds before they can be used normally, using them immediately may still result in 403.
    * It is recommended to use a proxy to request your target page and check if the status code is `403`. If so, your proxy triggers press mode, use homepage sense + press mode parameters. If not (`200` or `302` etc.), your proxy triggers sense-only mode, use those parameters.

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `Universal` | `http://api.nocaptcha.io/api/wanda/perimeterx/universal` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `Page URL that triggers perimeterx verification`    | `Yes` |
| `tag`        | `String`  | `Version, tag parameter in */api/v2/colletor or */assets/js/bundle (if not passing tag, must pass app_id)`    | `No` |
| `app_id`        | `String`  | `appId parameter in */api/v2/colletor or */assets/js/bundle (starts with PX, if not passing app_id, must pass tag)`    | `No` |
| `captcha`    | `Object`  | `Captcha parameter, required for xhr API returned press captcha`    | `No` |
| `captcha_html`    | `String`  | `Captcha parameter, response source code of press captcha from href request`    | `No` |
| `uuid`    | `String`  | `window._pxUuid`    | `No` |
| `vid`    | `String`  | `window._pxVid`    | `No` |
| `proxy`    | `String`  | `No need to keep proxy consistent, if passing proxy please use overseas proxy, format: ip:port or usr:pwd@ip:port (contact admin if issues)` | `No` |
| `did` | `String`  | `Fingerprint ID returned by seamless mode (in extra property), pass this parameter for subsequent press captcha from xhr APIs`       | `No` |
| `country`    | `String`  | `Country code of proxy used in business process, e.g. US (us), UK (uk), consult admin for details`    | `No` |
| `ip`    | `String`  | `IP address of proxy used in business process (e.g. 56.214.78.94), consult admin for details`    | `No` |
| `user_agent` | `String`  | `Custom user_agent, please pass latest Windows UA`       | `No` |
| `cookies` | `String`  | `Current page cookies in press captcha mode`       | `No` |
| `actions` | `Integer`  | `Random behavior count, higher value takes longer, set higher for high risk control sites, default 1`       | `No` |
| `timeout` | `Integer`  | `Verification timeout`       | `No` |

#### json examples

##### Seamless mode only
```json
{
    "app_id": "PXu6b0qd2S",
    "href": "https://www.walmart.com/",
    "proxy": "user:pass@ip:port"
}
```

##### Seamless + press mode (press captcha appears directly when opening target page)
```json
{
    "tag": "v8.6.6",
    "href": "https://www.walmart.com/",
    "proxy": "user:pass@ip:port"
}
```

##### Pure press captcha returned by xhr API

`captcha`: If the triggered API directly returns `json` data format, directly pass the returned `json` data as the `captcha` parameter, as shown below:

![xhr press captcha](/images/perimeterx/4.png)

```json
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
    "did": "did returned by seamless mode",
    "proxy": "user:pass@ip:port"
}
```

### Response Data (JSON):

#### Successful Response

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data.cookies`   | `String`  | `The available _px2, _px3 cookies returned after successful verification, can be used for subsequent verification APIs`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "2635.12ms",
  "data": {
    "cookies": {
        "_px3": "eb9fb4aab8cbd8d9c7018d0928bdccd972ef2a879383dec6b8999bca90ef4fdd:0r5KU/5t6VOMgwq7DnwmGd246hJVZbhPeI72OXfd8QSyRuK1hBRSBog3nrfQah8dLHd5X7cJZJnydq09AginIw==:1000:7eMdz1/BzkA4xQ8/rxujv5jsju6W1PbCAAp+gNDX8fox23jXH2mvzBzg0IwYLDX576aAHr3TeWqHFWvutnqxAKgTSIyR8cutzM7CG6zHQSV0N8piaWjjXlozbaWh77V3BGC7EZ/e3Rj3cbhl9Z4bufg6/87I91c7vv3Ka4ewGi+9EkKABRSCjAs4wEJYu6SneH1ZiiQAWVRW/EAULvFKJpxC07/qpxYuCblvaPljf14=", 
        "_pxde": "9a14782e5832ac4ba515c98e3e9f6b6e7b2e3d8ecb36320e659f85bb4f7359ac:eyJ0aW1lc3RhbXAiOjE3MTE2ODA3MDcyNzd9", 
        "pxcts": "48247186-ed77-11ee-8c23-8bccbc7b0e91",
        "_pxvid": "bcc357c3-ed78-11ee-aaf0-a24906ed7b54",
        "_pxde": "370c1218665b160f442e1e2b63603a15b046b7831b83de27de7c5211bf102f77:eyJ0aW1lc3RhbXAiOjE3MTE2ODI5NTE5MzZ9"
    }
  }
}
```

### Call Example

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
    ],
    debug=True
)

print(resp.text)
```
