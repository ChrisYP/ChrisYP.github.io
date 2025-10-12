------

[`返回首页`](../README.md)    [`上一页`](kasada.md)    [`下一页`](shape.md)    [`English Version`](../en-US/datadome.md)

## Datadome

### 说明
* 参数调用非常复杂，强烈建议直接使用 `pynocaptcha`，详情看下面 python 示例！！！

* 当看到 `cookies` 中有 `datadome`, 代表存在 `datadome` 验证, 有以下三种情况, 举个例子:
  * 当你要访问 `https://www.vinted.com/`, 挂代理请求 `https://www.vinted.com/`:
    * 状态码不是 `403` (`无感模式`): 
      * 打开 f12 查看是否有 `/js/` 结尾并且接口响应如下类似:
      ```
      {
        "status": 200,
        "cookie": "datadome=66wPBABk21P4x28BLuVse__8_z141EPJEjbgi1HBvNGBcHmX91OT1Z9Z63G4x_suPlRPQ_tgwljYmI5mWxpmkMJ3pKrcnAVKHZs2ymS_2O4nM5wEblvP~~nK3orSol0W; Max-Age=31536000; Domain=.soundcloud.com; Path=/; Secure; SameSite=Lax"
      }
      ```
      `无感` 验证类型, 必须要传 `js_url` (该 `/js` 结尾的 url), 该种模式会在我们的接口响应的 `extra` 参数中返回一个 `did` 参数, 该参数对于该页面后续的 `datadome` 验证非常重要！！！
      * 如果首页是 `无感模式`, 则后续的关键数据接口（如 `登录`、`查询`等）中携带有 `datadome` cookie, 并且会返回以下类似响应:
      ```
      {
        "url": "https://geo.captcha-delivery.com/captcha/?initialCid=AHrlqAAAAAMAqpOrr0GfIWgAudQ9Vg==&cid=w9vlJ4Xaf117hm82ORPnno7AnVvPPCoZ2gCDLj~Nch09ENObNXSzDWFekvMpp8ScynMSrB3~jsXcFtU9Y8mhOUscfnu1k_a~4_GMyGRE29_Gy~skFDqfX8tQJv1Va5Fv&referer=http%3A%2F%2Fapi-auth.soundcloud.com%2Fweb-auth%2Fidentifier%3Fq%3Desbiya1%2540gmail.com%26client_id%3D1q3v4x1lu3DpcWb4fAz0urivByipMEMK&hash=7FC6D561817844F25B65CDD97F28A1&t=fe&s=48134&e=faa8c1fb03676ac05d3bbe1d876a2d60168a7a2bab3adb5366483fc829465498"
      }
      ```
      则过掉该验证码需要传 `href` (当前浏览器页面的地址), `captcha_url`(响应中的 url `https://geo.captcha-delivery.com/captcha/?initialCid=AHrlqAAAAAMAqpOrr0GfIWgAudQ9Vg==&cid=w9vlJ4Xaf117hm82ORPnno7AnVvPPCoZ2gCDLj~Nch09ENObNXSzDWFekvMpp8ScynMSrB3~jsXcFtU9Y8mhOUscfnu1k_a~4_GMyGRE29_Gy~skFDqfX8tQJv1Va5Fv&referer=http%3A%2F%2Fapi-auth.soundcloud.com%2Fweb-auth%2Fidentifier%3Fq%3Desbiya1%2540gmail.com%26client_id%3D1q3v4x1lu3DpcWb4fAz0urivByipMEMK&hash=7FC6D561817844F25B65CDD97F28A1&t=fe&s=48134&e=faa8c1fb03676ac05d3bbe1d876a2d60168a7a2bab3adb5366483fc829465498` )
      以及上面所说的 `无感` 模式返回的 `did` 参数必须携带
      还有 `cookies: {"datadome": '无感模式返回的 datadome'}`
      也就是使用无感模式返回的 `datadome` cookie 访问你的目标数据接口又继续返回了滑块验证码或者设备验证码模式的话, 则需要携带 `href`、`captcha_url`、`did`、`cookies`
    ![无感验证码样例](/images/datadome/js.png)
    * 状态码 `403` (`设备验证模式`): 
      * 如果进入目标页面直接跳转至下面这样验证的页面或者是过掉滑块验证之后又跳转到这个验证了, 则是 `interstitial` 设备验证模式, 请传参数 `interstitial: true`
    ![无感验证码样例](/images/datadome/interstitial.png)
    * 状态码 `403` (`滑块验证码`):
      * 如果进入目标页面直接跳转至下面这样验证的页面, 则是 `captcha` 滑块验证码模式
    ![滑块验证码样例](/images/datadome/captcha.png)

  * 简单说就是先请求你目标页面地址, 状态码 `200` 就走无感模式, `403` 就走验证码模式, 类似以下伪代码流程:

  ```
  # 请求目标页面 href
  resp = session.get(href, headers=headers)
  
  # 状态码 200 为无感验证模式, 
  if resp.status_code == 200:
      res = DatadomeCracker(
          user_token=USER_TOKEN
          href=href,
          user_agent=user_agent,
          js_url="https://dd.vinted.lt/js",
          js_key=js_key,
          proxy=proxy,
      ).crack()
  # 状态码 403, 指定 interstitial 为 true, 保证过掉遇到的所有 datadome 验证码模式, 获取最终有效 datadome
  elif resp.status_code == 403:
      res = DatadomeCracker(
        user_token=USER_TOKEN,
          href=href,
          user_agent=user_agent,
          interstitial=True,
          proxy=proxy,
      ).crack()
  ```

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `通用版（universal）` | `http://api.nocaptcha.io/api/wanda/datadome/universal` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `触发 datadome 验证的页面地址`    | `是` |
| `proxy`    | `String`  | `无需保持代理一致, 若传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `是` |
| `js_url`    | `String`  | `js 模式下需要传该参数, /js/ 结尾的返回 datadome cookie 的接口, 如: https://dwt.soundcloud.com/js/`    | `否` |
| `js_key`    | `String`  | `js 模式下需要传该参数, f12 搜索 ddjskey 值, 如: E6EAF460AA2A8322D66B42C85B62F9`    | `否` |
| `captcha_url`    | `String`  | `post(xhr) 接口触发的 "url": "/captcha?initCid=xxx"`    | `否` |
| `interstitial`    | `Boolean`  | `是否会触发 interstitial 设备验证模式, 默认 false`    | `否` |
| `user_agent` | `String`  | `自定义 user_agent, 必须保持 user-agent 一致`       | `否` |
| `did` | `String`  | `js 模式返回的指纹 id（存在 extra 属性中）, 后续 xhr 接口出现的滑块验证码请传该参数`       | `否` |
| `cookies` | `String`  | `当前页面的 cookies`       | `否` |
| `timeout` | `Integer`  | `验证超时时间`       | `否` |

### Response Data（JSON）:

#### 提交验证（submit=true）

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.datadome`   | `String`  | `验证通过返回的可用的 datadome cookie, 可用于后续验证接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "4635.12ms",
  "data": {
    "datadome": "HYvnTVSxppxMMrSk_Z_MOHoSKkQRd2ppQr~pOeo2nDlL7Lg7QBwb2ew5OYQxSSSH1CR9NzO78A25KHM7kLV6OydtvwvJZ773Jil1mPC7ZoFSQQDrDYVeHZtjq_BWUai6"
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
from utils import USER_TOKEN, get_idea_proxy
from pynocaptcha import magneto, crack_datadome


def checkbalance(session: magneto.Session, extra):
    """
    后续需要进行的目标接口请求
    """
    data = {
        'language': 'en-ca',
        'csrfmiddlewaretoken': extra['csrfmiddlewaretoken'],
        'card_number': '98082560015032626594919',
        'pin': '4632',
        'g-recaptcha-response': 'true',
    }
    
    headers = {
        'accept': 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7',
        'accept-language': extra['accept-language'],
        'content-type': 'application/x-www-form-urlencoded',
        'origin': 'https://homedepot-ca.cashstar.com',
        'priority': 'u=0, i',
        'referer': 'https://homedepot-ca.cashstar.com/reload/',
        'sec-ch-ua': extra['sec-ch-ua'],
        'sec-ch-ua-mobile': '?0',
        'sec-ch-ua-platform': extra['sec-ch-ua-platform'],
        'sec-fetch-dest': 'document',
        'sec-fetch-mode': 'navigate',
        'sec-fetch-site': 'same-origin',
        'sec-fetch-user': '?1',
        'upgrade-insecure-requests': '1',
        'user-agent': extra['user-agent']
    }
    return session.post(
        'https://homedepot-ca.cashstar.com/reload/',
        headers=headers,
        data=data, 
    )


def parse_index(resp, extra):
    """
    需要解析 href 首页响应源码中获取的数据
    """
    token = re.search(r'name="csrfmiddlewaretoken" value="(.*?)"', resp.text)[1]
    extra['csrfmiddlewaretoken'] = token


session, resp, extra = crack_datadome(
    user_token=USER_TOKEN,
    href='https://homedepot-ca.cashstar.com/reload/',
    verifiers=[
        checkbalance
    ],
    parse_index=parse_index,
    proxy=get_idea_proxy("hk"),
    debug=True
)

print(resp.text)
```
