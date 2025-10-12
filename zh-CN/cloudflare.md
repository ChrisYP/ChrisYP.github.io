------

[`返回首页`](../README.md)    [`上一页`](tls.md)      [`下一页`](aws.md)    [`English Version`](../en-US/cloudflare.md)

## CloudFlare

### 服务说明

* 线上仅为测试服务, 稳定/量大/独享/包月/优惠 请联系管理员

### 类型说明

* 类型一: cookies (普通模式: `cf_clearance`、`__cf_bm`)
* 当未出现跳转页面, 但是存在 `cf_clearance` 时, 可设置参数 alpha=true 通过无感验证(也可咨询管理员), proxy 必传
![cookies样例](/images/cloudflare/cookies.png)

* 类型二: 验证码式 (turnstile: `cf_turnstile-response`)(此类型消耗 300 点 传入代理 150 点), proxy 非必传
* ps: 一般嵌入在登录框中, 验证参数为 `captcha_api_key` 等键名（只是举例不一定是这个）, 参数值为 `0.` 开头的。

![验证码式样例](/images/cloudflare/captcha.png)

### 参数查找

* cookies 类型: 直接输入触发页面地址即可

* turnstile 类型: 需要额外输入 sitekey 参数
![sitekey](/images/cloudflare/sitekey.png)

### 结果说明

* cloudflare cookies模式 需要保持 ip、ua 一致
* cloudflare cookies模式 校验 tls 指纹, 请自行使用 tls 请求库或使用 tls 转发服务
* cloudflare turnstile模式 结果通常可直接使用, 传入代理只需 150 点

### Request URL（POST）:

| 版本                | 接口地址                                                     |
|-------------------|----------------------------------------------------------|
| `通用版（universal）`  | `http://api.nocaptcha.io/api/wanda/cloudflare/universal`  |

### Request Headers:

| 参数名            | 说明                                                                         | 必须  |
|----------------|----------------------------------------------------------------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`                                                               | `是` |
| `Content-Type` | `application/json`                                                         | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)` | `否` |

### POST Data（JSON）:

| 参数名        | 类型        | 说明                                                                             | 必须  |
|------------|-----------|--------------------------------------------------------------------------------|-----|
| `href`  | `String`  | `触发验证的地址`                                           | `是` |
| `proxy`    | `String`  | `cookies模式必传, turnstile非必传` | `是` |
| `sitekey`       | `String`  | `turnstile 类型需要传入(价格为 300 点)`                                         | `否` |
| `explicit`       | `Bool`  | `turnstile 类型需要传入, f12 查看 https://challenges.cloudflare.com/turnstile/v0/api.js?onload=cf__reactTurnstileOnLoad&render=explicit 的 js 连接中是否有 render=explicit 参数, 如有则填 true, 没有不填即可, 默认 false`                                         | `否` |
| `action`       | `String`   | `turnstile 类型中传入, 具体解释看下`                                         | `否` |
| `cdata`       | `String`  | `turnstile 类型中传入, turnstile.render 的参数中有 cdata 才传`                                         | `否` |
| `user_agent` | `String` | `自定义请求头, 如果返回提示不支持自定义则不要传`                            | `否` |
| `alpha` | `Boolean` | `是否为无感 cookies`                            | `否` |

#### action / cdata 查找(非必须, 如有疑问可联系管理员)

当验证类型为 `turnstile`, 并在目标网站的 `*turnstile/v0/api.js` 链接中发现有 `render=explicit` 参数, 那么传入 `explicit=true`, `action`, `cdata` 查找步骤如下:

* 打开 f12 搜索 `window.turnstile.render`
![render](/images/cloudflare/render.png)

* 在该处下断点, 并清除 cookie 缓存刷新页面, 在此处断下来, 查看 `action` 的值填入即可
![action](/images/cloudflare/action.png)

### 参数示例

#### cookies 类型

```json
{
    "href": "https://nowsecure.nl/",
    "proxy": "usr:pwd@ip:port",
}

```

#### turnstile 类型
```json
{
    "href": "https://visa.vfsglobal.com/chn/zh/deu/login",
    "proxy": "usr:pwd@ip:port",
    "sitekey": "0x4AAAAAAACYaM3U_Dz-4DN1"
}
```

#### turnstile action 类型
```json
{
    "href": "https://app.ogcom.xyz/signup?step=first",
    "proxy": "usr:pwd@ip:port",
    "sitekey": "0x4AAAAAAASTIy9n6lEJjrIE",
    "action": "verification_code",
    "explicit": true,
}
```


### Response Data（JSON）

| 参数名          | 类型        | 说明                            |
|--------------|-----------|-------------------------------|
| `status`     | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`        | `String`  | `调用结果中文说明`                    |
| `id`         | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.cookies` | `String`  | `验证通过返回的 cookies`          |
| `data.token` | `String`  | `验证通过返回的 token(turnstile 使用)`               |
| `cost`       | `String`  | `验证耗时（毫秒）`                    |


```
{
"cost": "3380.01ms",
"data": {
"token": "xxx",
"cookies": "xxx=xxx;"
},
"id": "bc174976-81b2-418e-a6e3-9f7c0bbd41ae",
"msg": "验证成功",
"status": 1
}
```

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import CloudFlareCracker

cracker = CloudFlareCracker(
user_token="xxx,
sitekey="0x4AAAAAAACYaM3U_Dz-4DN1",
href="https://visa.vfsglobal.com/chn/zh/deu/login",
proxy="usr:pwd@ip:port",
debug=True,
)
ret = cracker.crack()
print(ret)
```