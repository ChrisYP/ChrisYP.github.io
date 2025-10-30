------

[`返回首页`](../README.md)    [`上一页`](shape.md)    [`下一页`](discord_join_channel.md)    [`English Version`](../en-US/vercel.md)

## Vercel

### 价格说明
* 消耗 `150` 点, 需要传入 `proxy`

### 说明
* 当打开目标页面，出现以下提示，抓包有发送 `/.well-known/vercel/security/request-challenge` 接口，且 `cookies` 中有 `_vcrcs` 代表存在 `vercel` 验证
    ![验证样式](/images/vercel/img1.png)

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `通用版（universal）` | `http://api.nocaptcha.io/api/wanda/vercel/universal` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `触发 vercel 验证的页面地址`    | `是` |
| `proxy`    | `String`  | `需保持代理一致, 传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `否` |
| `user_agent` | `String`  | `自定义 user_agent`       | `否` |
| `timeout` | `Integer`  | `验证超时时间`       | `否` |

#### json 示例

```
{
    "href": "https://faucet.story.foundation/",
    "proxy": "user:pass@ip:port",
}
```

### Response Data（JSON）:

#### 提交验证

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data._vcrcs`   | `String`  | `验证通过返回的可用的 _vcrcs cookie, 可用���后续验证接口`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "2635.12ms",
  "data": {
    "_vcrcs": "1.1726824386.3600.NGZhZDA1MjA3YzE0ZWM1ZjQwYzZmYmNiMTRmNGI0ODY=.98089ffd4040710db7cee73152aafefb"
  },
  "extra": {
    "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/127.0.0.0 Safari/537.36",
    "sec-ch-ua-platform": "\"Windows\"",
    "sec-ch-ua": "\"Not)A;Brand\";v=\"99\", \"Google Chrome\";v=\"127\", \"Chromium\";v=\"127\"",
    "accept-language": "en-US,en;q=0.9",
    "sec-ch-ua-arch": "\"x86\"",
    "sec-ch-ua-bitness": "\"64\"",
    "sec-ch-ua-full-version": "\"127.0.6533.4\"",
    "sec-ch-ua-full-version-list": "\"Not)A;Brand\";v=\"99.0.0.0\", \"Google Chrome\";v=\"127.0.6533.4\", \"Chromium\";v=\"127.0.6533.4\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-model": "\"\"",
    "sec-ch-ua-platform-version": "\"12.0.0\""
  }
}
```

### 调用示例

#### python

```python
version = random.randint(118, 128)
user_agent = random.choice([
    f"Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{version}.0.0.0 Safari/537.36",
    f'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/{version}.0.0.0 Safari/537.36'
])

# href = 'https://faucet.story.foundation/'
href = 'https://www.anime.com/'

proxy = "代理"
resp = requests.post("http://api.nocaptcha.cn/api/wanda/vercel/universal", headers={
    "User-Token": USER_TOKEN
}, json={
    "href": href,
    "user_agent": user_agent,
    "proxy": proxy,
    "timeout": 30
}).json()
print(resp)
```
