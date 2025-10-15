------
[`返回首页`](../README.md)    [`上一页`](incapsula_rbzid.md)  [`下一页`](tls.md)	[`English Version`](../en-US/akamai.md)

## Akamai

### 说明
* akamai 还有其他很多因素影响，强烈建议直接使用 `pynocaptcha`，详情看下面 python 示例！！！
* v2/v3 通用

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `v2（universal）` | `http://api.nocaptcha.io/api/wanda/akamai/v2` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| `href`       | `String`  | `触发 akamai 验证的页面地址`                                                                                                                          | `是` |
| `api`        | `String`  | `akamai 提交 sensor_data 验证接口地址, 该地址过段时间会换`       | `否` |
| `telemetry`  | `Boolean` | `是否 headers 中的 telemetry 参数验证形式（如 https://api.maersk.com/ 接口的 akamai-bm-telemetry）, 默认 false`   | `否` |
| `cookies`  | `Object`  | `cookies 的值, 可以是字符串格式, 也可以是键值对, 必须包含 _abck、bm_sz 两个参数`   | `否` |
| `proxy`    | `String`  | `无需保持代理一致, 若传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `否` |

#### json 示例

```
{
    "href": "https://www.jetstar.com/",
}
```

```
{
    "href": "https://www.jetstar.com/",
    "cookies": {
        "value": "_abck=D719B7C0C6B1EBE8FC8F5C1B804B2265~-1~YAAQJescuEJsVzWIAQAAnwAZQQkN297mPe+Q48Xd0/10jSvgz/y69qQbPEwxUuQZhIhisL+GFAMfvabHtQPRUbiIqzDD6vA9iN9lvjzaAbKaL+aNXF/3EhpYYYUsBa0q92JUxusD8F09nFXy3mfZ8p8GzDk+/ikw4Y8QVQcchjC/s6XYbG+I2RSHl+lDOSvR2biGLFZ1dW2PsFZQ6Fs4M1/ccWfaXg6IRvzjlWaF0vH8GIoljDVRvZxwCeUO71QJORFxeVEEO43BiC3LczJhMomt8pnTbnJcMbMbi1zFcYUKUZjYvB7+kJ1JsMHfVdzbrwTB2I3bePGPgX06RvzCReVCETYpJB7H+XEeJgQQDzKiYZhCONfnae3BQUll~-1~-1~1684722838; bm_sz=751A827227D797408E66A3559D978757~YAAQpVcyuNsPVjCIAQAAMTCrRhNw86NLVNcBypYZvOkbMMnc+ef6EeDWu9UtvPw3OfyfpKLmEFQeDw99mddahdMlOj3VxzPz8eV9mfMSWDLxup33fIKAvsMvnUjvAJV0gpZvTTwdk0atKXCg1DXvs+U+VOvPPJtS76B2t+r0jXrB+cUm2hJL7qF59kbHLBl54yypauoWa1qEu9lgelS5kdwiR93A0c9IRagfLG4VjFydhZBoD6ldWEQjQUflrf00GSoxQpL0QBKRlD7fFNRtMhBmndvu5yoGdixtPXCEKk5BzRl/~4605506~4276528; ak_bmsc=0E5236AFD795DD698B2E15191CEF0FDC~000000000000000000000000000000~YAAQpVcyuNoPVjCIAQAAMTCrRhNkrxzrgkZ1QP7XH0+hyJ2ul+4V0reJDlf1omJylP4/7vc+bxfB8EW1pfuYQWdBmzTBnE84h+7tH1SbFvNNNDul53BJsoOd79t8V0LGQdlXls3FWxITVSwuVlvCQTuJY1jq+uxrTTFFWpuqWQZnWkaLC/p8E7KRycXTaDSh7UW4k6ISRmssUftgDxwjZg43T6IbMyPf9dugLQSg9dKx4p8wyTcNern/fHfx7dAABbnUJkwmP+Y/eR4mfc9MJtIsJ3006DKH7PNoZ5JhtmnN9JTuhwfSEEnCrhs0j/cb2TrsSMo26w4C1xIaUNwZXE77YDci8VIkwEq9NvSTrTZUncSl0rsvoBz0j4QheSI=",
        "uri": "https://www.jetstar.com/"
    }
}
```

```
{
    "href": "https://www.sephora.com/",
    "device": "pc"
}
```

```
{
    "href": "https://www.maersk.com.cn/instantPrice/quotes",
    "telemetry": true,
}
```

```
{
    "href": "https://www.maersk.com.cn/instantPrice/quotes",
    "cookies": {
        "value": "_abck=D719B7C0C6B1EBE8FC8F5C1B804B2265~-1~YAAQJescuEJsVzWIAQAAnwAZQQkN297mPe+Q48Xd0/10jSvgz/y69qQbPEwxUuQZhIhisL+GFAMfvabHtQPRUbiIqzDD6vA9iN9lvjzaAbKaL+aNXF/3EhpYYYUsBa0q92JUxusD8F09nFXy3mfZ8p8GzDk+/ikw4Y8QVQcchjC/s6XYbG+I2RSHl+lDOSvR2biGLFZ1dW2PsFZQ6Fs4M1/ccWfaXg6IRvzjlWaF0vH8GIoljDVRvZxwCeUO71QJORFxeVEEO43BiC3LczJhMomt8pnTbnJcMbMbi1zFcYUKUZjYvB7+kJ1JsMHfVdzbrwTB2I3bePGPgX06RvzCReVCETYpJB7H+XEeJgQQDzKiYZhCONfnae3BQUll~-1~-1~1684722838; bm_sz=751A827227D797408E66A3559D978757~YAAQpVcyuNsPVjCIAQAAMTCrRhNw86NLVNcBypYZvOkbMMnc+ef6EeDWu9UtvPw3OfyfpKLmEFQeDw99mddahdMlOj3VxzPz8eV9mfMSWDLxup33fIKAvsMvnUjvAJV0gpZvTTwdk0atKXCg1DXvs+U+VOvPPJtS76B2t+r0jXrB+cUm2hJL7qF59kbHLBl54yypauoWa1qEu9lgelS5kdwiR93A0c9IRagfLG4VjFydhZBoD6ldWEQjQUflrf00GSoxQpL0QBKRlD7fFNRtMhBmndvu5yoGdixtPXCEKk5BzRl/~4605506~4276528; ak_bmsc=0E5236AFD795DD698B2E15191CEF0FDC~000000000000000000000000000000~YAAQpVcyuNoPVjCIAQAAMTCrRhNkrxzrgkZ1QP7XH0+hyJ2ul+4V0reJDlf1omJylP4/7vc+bxfB8EW1pfuYQWdBmzTBnE84h+7tH1SbFvNNNDul53BJsoOd79t8V0LGQdlXls3FWxITVSwuVlvCQTuJY1jq+uxrTTFFWpuqWQZnWkaLC/p8E7KRycXTaDSh7UW4k6ISRmssUftgDxwjZg43T6IbMyPf9dugLQSg9dKx4p8wyTcNern/fHfx7dAABbnUJkwmP+Y/eR4mfc9MJtIsJ3006DKH7PNoZ5JhtmnN9JTuhwfSEEnCrhs0j/cb2TrsSMo26w4C1xIaUNwZXE77YDci8VIkwEq9NvSTrTZUncSl0rsvoBz0j4QheSI=",
        "uri": "https://www.jetstar.com/"
    },
    "telemetry": true,
}
```

### Response Data（JSON）:

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data._abck`   | `String`  | `验证通过返回的可用的 _abck cookie, 可用于后续验证接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
	"status": 1,
	"msg": "验证通过",
	"id": "8a8f0778-da09-4eea-a32d-e3b508654ba6",
	"cost": "1984.57ms",
	"data": {
		"_abck": "2EDD22DB758F24695963E50D3C9A776F~0~YAAQx\/ggF8FPIJ2HAQAA8nKqrQmFx5H17A\/jMUd1alzWlJ6VXb6NGDhXkb\/1cJW+Bp0jJYvWVj8hQVc1vRKAiKQ1HLm0JIo8kg00KEBoAyRG+VZZPRV6ikricthJ69SlXF99wcHaHwx7mvDZdwwAtJBl+Fp2Kagx62AbUYZjEpc9aOCZ5KXBQhdrwCrzzXWsu5WEgmGovNqegFuIpW1ifsVPe13QSi8EjwF\/nsuJQShLeRgsls1JB0Trwx8Kg3qRFiL9g4rtAdeW8OwYQ4DXj3PoBU56G0I4oCrhm6urGs8wMaU3OdpW6SRBAV93r4FO6K+lmcm8BVcfYc70\/wVuEx3Fx0zpesE0fkdKC6N5c80AjVtSgJnDLFuShDnXo+wsWGROM1vxP7sC7N6raiSN66sX4UxGlkAJiCU=~-1~||1-hkqRyYlvue-1-10-1000-2||~-1"
	}
}
```

### CURL command:

```
curl \
    -H "User-Agent: python-requests/2.28.2" -H "Accept: */*" \
    -H "User-Token: xxx" \
    -H "Content-Type: application/json" \
    --data-binary "{\"href\": \"https://www.jetstar.com/\", \"api\": \"https://www.jetstar.com/3Fl6sx/QIvaPL/b/7Hf/iQxyLG8eyP4/acumkkpfYkV7EO/ZyMtejt5PAc/REZU/Jk85Pn4\"}" \
    --compressed "http://api.nocaptcha.io/api/wanda/akamai/v2"
```

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python

# pip install --upgrade pynocaptcha
from pynocaptcha import crack_akamai_v3
# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from utils import USER_TOKEN, get_idea_proxy


_, response, _ = crack_akamai_v3(USER_TOKEN, {
    'referer': 'https://www.dickssportinggoods.com/s/gift-cards',
    "url": 'https://payments.dickssportinggoods.com/prod/api/paygate/v2/giftcard/balance',
    "json": {
        'cardNumber': '6186553725049271',
        'pin': '22872681',
    },
}, proxy=get_idea_proxy("hk"), debug=True)
print(response['status'], response["body"][:100])
```
