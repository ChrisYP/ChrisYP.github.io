------
[`返回首页`](../README.md)    [`上一页`](hcaptcha.md)       [`下一页`](incapsula_utmvc.md)   [`English Version`](../en-US/incapsula.md)

## Incapsula ( reese84 )

### 有问必答

* 接口中提交的 href 在哪里?(有多个 src 的情况下, 选择有 async 关键字的那个链接)
    * ![incapsula](/images/incapsula/incapsula.png)
* href 返回样例(响应中会包含类似 ob 混淆一样的代码)
    * ![incapsula](/images/incapsula/incapsula2.png)

### 为什么选择我们

* 通用性: 目前已知网站均能通过验证。
* 极致的速度: 接口使用`纯算法`计算参数，`协议提交`，`同步返回`。
* 稳定性: 更新及时（不会超过两小时），更好地支撑您的业务。

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|-------------------|---------------------------------------------------------|
| `reese84（universal）` | `http://api.nocaptcha.io/api/wanda/incapsula/reese84` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| `href`       | `String`  | `触发 incapsula 验证的获取 incapsula js 的地址`                                                                                                                           | `是` |
| `user_agent` | `String`  | `请求流程使用 ua, 后续请求校验 ua 是否一致, 所以请传你后续请求将使用的 ua`                                                                                                      | `是` |
| `cookies` | `Object`  | `提示需要包含 rbzid、rbzsessionid 的 cookies 时使用`                                                                                                      | `否` |

#### json 示例

```
{
  "href": "https://www.priceline.com.au/Cawdor-asse-my-Nightning-we-from-Dealell-Come-Ty",
  "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36",
}
```

### Response Data（JSON）:

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.solution` | `String`  | `验证通过返回的 solution, 可用于后续请求获取resee84接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
  'status': 1,
  'msg': '验证成功',
  'id': '4a8019cc-321b-467f-9273-2698fb14288b',
  'cost': '2575.75ms',
  'data': {
    'solution': {
      'interrogation': {
        'p': 'A long string',
        'st': 1691455449,
        'sr': 1259062184,
        'cr': 352269128,
        'og': 1
      },
      'version': 'beta'
    },
    'old_token': None,
    'error': None,
    'performance': {
      'interrogation': 643
    }
  },
  'extra': {}
}
```

<!--#### 不提交验证, 仅计算（submit=false）

| 参数名      | 类型        | 说明                            |
|----------|-----------|-------------------------------|
| `status` | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`    | `String`  | `调用结果中文说明`                    |
| `id`     | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data`   | `Object`  | `直接用作验证接口 post json 参数提交即可`   |
| `cost`   | `String`  | `验证耗时（毫秒）`                    |

```
{
  "cost": "279.66ms",
  "data": {
    "error": null,
    "old_token": null,
    "performance": {
      "interrogation": 319
    },
    "solution": {
      "interrogation": {
        "cr": 661732465,
        "og": 1,
        "p": "A long string",
        "sr": 981077036,
        "st": 1679134739
      },
      "version": "beta"
    }
  },
  "id": "b41526e4-60b9-4005-8967-0124d328f386",
  "msg": "验证成功",
  "status": 1
}
```-->


### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import IncapsulaReee84Cracker

cracker = IncapsulaReee84Cracker(
    user_token="xxx",
    href="https://www.priceline.com.au/Cawdor-asse-my-Nightning-we-from-Dealell-Come-Ty",
    user_agent="Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36",
    debug=True
)
ret = cracker.crack()
print(ret)
```
