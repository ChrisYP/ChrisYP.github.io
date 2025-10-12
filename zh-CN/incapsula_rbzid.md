------

[`返回首页`](../README.md)    [`上一页`](incapsula_utmvc.md)     [`下一页`](akamai.md)    [`English Version`](../en-US/incapsula_rbzid.md)

## Incapsula ( rbzid )

### rbzid 情况
* 请求 incapsual 脚本时, 返回如下情况代表触发了 rbzid, (kramericaindustries.ac.lib.js, window.rbzns...)
![rbzid](/images/incapsula/rbzid.png)

### 结果使用
* 保持 ua 一致, 使用返回的 verify_url, headers GET 拿到返回 cookies, 后续保持 ua 一直带上 cookies 即可
* 返回的请求头固定为 x-zebra-zebra, 如果你想随机 x-zebra- + random(5) 即可

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|-------------------|---------------------------------------------------------|
| `rbzid` | `http://api.nocaptcha.io/api/wanda/incapsula/rbzid` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明  | 必须  |
|--------------|-----------|----------------------|-----|
| `href`        | `String`  | `返回 rbzid 脚本的 url` | `是` |
| `user_agent` | `String`  | `rbzid cookies 使用需要 ua 一致, 所以请传你将使用的 ua`  | `是` |
| `script` | `String`  | `href 请求的结果脚本` | `是` |

#### json 示例

```
{
    "href": "https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=719d34d31c8e3a6e6fffd425f7e032f3",
    "script": "href 请求结果"
    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
}
```

### Response Data（JSON）:

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data` | `Object`  | `包含 verify_url 和 headers 用于后续验证`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
    "status": 1,
    "msg": "验证成功",
    "id": "61b4bb7f-abf9-4875-ae58-38916e1ecbff",
    "cost": "36.42ms",
    "data": {
        'x-zebra-zebra': 'ZDM4ZjBlMjcyOGE1MjhmY2E3ZTFjNjNlODRiN2EyN2RlMzA5ZWM4MTskKGhhc2gpO194Y2FsYyhhcmd1bWVudHMuY2FsbGUpOzA7JChoYXNoKTtfeGNhbGMoYXJndW1lbnRzLmNhbGxlKTstNTkyNTkyNTg3MjA7JChoYXNoKTtfeGNhbGMoYXJndW1lbnRzLmNhbGxlKTtkaXNhYmxlZDskKGhhc2gpO194Y2FsYyhhcmd1bWVudHMuY2FsbGUpOzEyMzEyMw==', 
        'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36'
    }
}
```

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import IncapsulaRbzidCracker

cracker = IncapsulaUtmvcCracker(
    user_token="xxx",
    href="https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=719d34d31c8e3a6e6fffd425f7e032f3",
    script="href 请求结果",
    user_agent = "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
)
ret = cracker.crack()
print(ret)
```