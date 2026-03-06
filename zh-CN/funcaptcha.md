------
[`返回首页`](../README.md)    [`上一页`](unlocker.md)  [`下一页`](castle.md)	[`English Version`](../en-US/funcaptcha.md)

## Funcaptcha

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `funcaptcha（sense）` | `http://api.nocaptcha.io/api/wanda/funcaptcha/sense` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| `href`       | `String`  | `触发 funcaptcha 验证的页面地址`                                                                                                                          | `是` |
| `action`  | `String`  | `提前定义好的各个网站的参数配置, 如 login、register, 传了该参数则 public_key、title、api_host 等都不需要再传, 可联系管理员获取`   | `否` |
| `public_key`        | `String`  | `funcaptcha 的 key （如 
https://ark.coinbase.com/v2/32FBE3BC-228C-4967-9D76-8B27B3EBCF08/settings 的 32FBE3BC-228C-4967-9D76-8B27B3EBCF08）`       | `否` |
| `blob`  | `String` | `funcaptcha 配置参数, 联系管理员获取`   | `否` |
| `title`    | `String`  | `无需保持代理一致, 若传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `否` |
| `api_host`    | `String`  | `funcaptcha 业务流程的 host（如 
https://ark.coinbase.com/v2/32FBE3BC-228C-4967-9D76-8B27B3EBCF08/settings 等接口使用的 host: ark.coinbase.com）, 可不传` | `否` |
| `script_src`    | `String`  | `funcaptcha 的脚本地址, 以 api.js 结尾（如 https://ark.coinbase.com/v2/api.js）, 可不传` | `否` |
| `country`    | `String`  | `业务流程使用的代理所属地区国家 code, 如美国（us）、英国（uk）, 详情可咨询管理`    | `否` |
| `user_agent` | `String`  | `自定义 user_agent, 仅支持 chrome/edge, 且版本号 > 115, 如 Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36`       | `否` |
| `proxy` | `String`  | `代理（user:pass@ip:port）, 仅支持 http, 不支持 socks5`       | `否` |

#### json 示例

```
{
    'href': 'https://id.sonyentertainmentnetwork.com/id/create_account_ca/?entry=create_account&duid=0000000700090100544cac84ef82de92ad693fe8ad7d2cac277153bf416df1dab6d03762be9d305a&response_type=code&client_id=e4a62faf-4b87-4fea-8565-caaabb3ac918&scope=web%3Acore&access_type=offline&state=8baf922d800be7b1f705485091609db9b6a3976f6b13d57e1bdfb5f4a8213e91&service_entity=urn%3Aservice-entity%3Apsn&ui=pr&smcid=web%3Apdc&redirect_uri=https%3A%2F%2Fweb.np.playstation.com%2Fapi%2Fsession%2Fv1%2Fsession%3Fredirect_uri%3Dhttps%253A%252F%252Fio.playstation.com%252Fcentral%252Fauth%252Flogin%253Flocale%253Dzh-hans_CN%2526postSignInURL%253Dhttps%25253A%25252F%25252Fwww.playstation.com%25252Fzh-hans-cn%25252F%2526cancelURL%253Dhttps%25253A%25252F%25252Fwww.playstation.com%25252Fzh-hans-cn%25252F%26x-psn-app-ver%3D%2540sie-ppr-web-session%252Fsession%252Fv5.44.3&auth_ver=v3&no_captcha=true&cid=50cda37a-1183-4f0b-afdb-cfee22d4b504#/create_account/wizard/finish?entry=create_account',
    'action': 'register',
    'user_agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36',
    'proxy': 'user:pass@ip:port',
    'country': 'us'
}
```

```
{
    'href': "https://login.coinbase.com/signup",
    'api_host': "ark.coinbase.com",
    'public_key': "32FBE3BC-228C-4967-9D76-8B27B3EBCF08",
    'title': 'Coinbase - SignIn',
    'blob': 'xxx'
}
```

```
{
    'href': 'https://x.com/i/flow/signup?input_flow_data=%7B%22requested_variant%22%3A%22eyJyZWRpcmVjdF91cmwiOiIvIn0%3D%22%7D',
    'public_key': '2CB16598-CB82-4CF7-B332-5990DB66F3AB',
    'title': 'SignIn X / X',
}
```

### Response Data（JSON）:

#### 提交验证（submit=true）

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data.token`   | `String`  | `验证通过返回的可用的 token`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
    "status": 1,
    "success": true,
    "msg": "验证成功",
    "en_msg": "Verify success",
    "id": "c6dbdf94-5f0d-4016-82ce-0b20a6960bcb",
    "cost": "10902.14ms",
    "data": {
        "token": "41018993ef55cfb78.1839867301|r=us-east-1|meta=3|metabgclr=%23ffffff|metaiconclr=%23757575|guitextcolor=%23000000|lang=fr|pk=9869C2EE-434F-4116-A2E5-B6E1237239DA|at=40|rid=71|ag=101|cdn_url=https%3A%2F%2Fclient-api.arkoselabs.com%2Fcdn%2Ffc|surl=https%3A%2F%2Fclient-api.arkoselabs.com|smurl=https%3A%2F%2Fclient-api.arkoselabs.com%2Fcdn%2Ffc%2Fassets%2Fstyle-manager"
    },
    "extra": {
        "user-agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/139.0.0.0 Safari/537.36",
        "sec-ch-ua-platform": "\"macOS\"",
        "sec-ch-ua": "\"Not;A=Brand\";v=\"99\", \"Google Chrome\";v=\"139\", \"Chromium\";v=\"139\"",
        "accept-language": "fr-FR,fr;q=0.9",
        "sec-ch-ua-arch": "\"x86\"",
        "sec-ch-ua-bitness": "\"64\"",
        "sec-ch-ua-full-version": "\"139.0.7258.66\"",
        "sec-ch-ua-full-version-list": "\"Not;A=Brand\";v=\"99.0.0.0\", \"Google Chrome\";v=\"139.0.7258.66\", \"Chromium\";v=\"139.0.7258.66\"",
        "sec-ch-ua-mobile": "?0",
        "sec-ch-ua-model": "\"\"",
        "sec-ch-ua-platform-version": "\"13.6.2\""
    }
}
```

### CURL command:

```
curl \
    -H "User-Agent: python-requests/2.28.2" -H "Accept: */*" \
    -H "User-Token: xxx" \
    -H "Content-Type: application/json" \
    --data-binary "{\"href\":\"https://x.com/i/flow/signup?input_flow_data=%7B%22requested_variant%22%3A%22eyJyZWRpcmVjdF91cmwiOiIvIn0%3D%22%7D\",\"public_key\":\"2CB16598-CB82-4CF7-B332-5990DB66F3AB\",\"title\":\"SignIn X / X\"}" \
    --compressed "http://api.nocaptcha.io/api/wanda/funcaptcha/sense"
```

### 调用示例

#### python

```python

# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from curl_cffi import requests
from utils import USER_TOKEN, get_ipsmart_proxy

country = 'hk'
# proxy format: user:pass@ip:port
proxy = get_ipsmart_proxy(country)
session = requests.Session()
session.proxies.update({
    'all': 'http://' + proxy
})

resp = requests.post('http://api.nocaptcha.cn/api/wanda/funcaptcha/sense', headers={
    'user-token': USER_TOKEN
}, json={
    'href': 'https://id.sonyentertainmentnetwork.com/id/create_account_ca/?entry=create_account&duid=0000000700090100544cac84ef82de92ad693fe8ad7d2cac277153bf416df1dab6d03762be9d305a&response_type=code&client_id=e4a62faf-4b87-4fea-8565-caaabb3ac918&scope=web%3Acore&access_type=offline&state=8baf922d800be7b1f705485091609db9b6a3976f6b13d57e1bdfb5f4a8213e91&service_entity=urn%3Aservice-entity%3Apsn&ui=pr&smcid=web%3Apdc&redirect_uri=https%3A%2F%2Fweb.np.playstation.com%2Fapi%2Fsession%2Fv1%2Fsession%3Fredirect_uri%3Dhttps%253A%252F%252Fio.playstation.com%252Fcentral%252Fauth%252Flogin%253Flocale%253Dzh-hans_CN%2526postSignInURL%253Dhttps%25253A%25252F%25252Fwww.playstation.com%25252Fzh-hans-cn%25252F%2526cancelURL%253Dhttps%25253A%25252F%25252Fwww.playstation.com%25252Fzh-hans-cn%25252F%26x-psn-app-ver%3D%2540sie-ppr-web-session%252Fsession%252Fv5.44.3&auth_ver=v3&no_captcha=true&cid=50cda37a-1183-4f0b-afdb-cfee22d4b504#/create_account/wizard/finish?entry=create_account',
    'action': 'register',
    'proxy': proxy,
}).json()

print(resp)
```
