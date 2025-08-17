[`Back to Home`](en.md)    [`Previous`](perimeterx.md)   [`Next`](datadome.md)    [`中文文档`](../zh-CN/kasada.md)

## Kasada

### Pricing
* `x-kpsdk-ct` consumes `1000` points, must pass `href`, `ips_url`
* `x-kpsdk-cd` consumes `50` points, must pass `href`

### Description
* Parameter invocation is very complex, strongly recommend using `pynocaptcha` directly, see the python example below!
* When you see `x-kpsdk-ct` or `x-kpsdk-cd` in request headers, it means `kasada` verification exists
* For x-kpsdk-ct, keep user_agent consistent, result can be used multiple times
* For x-kpsdk-cd, can only be used once
* Supports `pure calculation mode`, for pure calculation please request `ips_url` API yourself, upload response content `ips_script` and response headers `ips_headers`, pure calculation mode does not require proxy

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `x-kpsdk-ct` | `http://api.nocaptcha.io/api/wanda/kasada/ct` |
| `x-kpsdk-cd` | `http://api.nocaptcha.io/api/wanda/kasada/cd` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### x-kpsdk-ct POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `f12 search /149e9513-01fa-4fb0-aad4-566afd725d1b/2d206a39-8ed7-437e-a3be-862e0f06eea3/fp?x-kpsdk-v=j-1.1.0, if not found search /149e9513-01fa-4fb0-aad4-566afd725d1b/2d206a39-8ed7-437e-a3be-862e0f06eea3/ips.js?, fill in the url of the request containing this link in response html`    | `Yes` |
| `fp_html` | `String` | `Response content of request ending with /fp?x-kpsdk-v=j-1.1.0` | `Yes` |
| `ips_url`    | `String`  | `Script address ending with ips.js`    | `Yes` |
| `fp_host` | `String` | `Domain of request ending with /fp?x-kpsdk-v=j-1.1.0` | `No` |
| `ips_script`    | `String`  | `Response content of request ending with ips.js`    | `No` |
| `ips_headers`    | `String`  | `Response headers of request ending with ips.js`    | `No` |
| `submit`    | `Boolean`  | `Whether to submit tl request, directly return x-kpsdk-ct, default not submit, recommend not filling and use pure calculation mode`    | `No` |
| `proxy`    | `String`  | `Keep proxy consistent, use overseas proxy, format: ip:port or usr:pwd@ip:port (contact admin if issues)` | `No` |
| `country`    | `String`  | `Country code of proxy used in business process, e.g. US (us), UK (uk), consult admin for details`    | `No` |
| `ip`    | `String`  | `IP address of proxy used in business process (e.g. 56.214.78.94), consult admin for details`    | `No` |
| `user_agent` | `String`  | `Custom user_agent, keep consistent with subsequent verification request APIs`       | `No` |
| `timeout` | `Integer`  | `Verification timeout`       | `No` |

### x-kpsdk-cd POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `Page URL that triggers kasada verification`    | `Yes` |
| `st`    | `Integer`  | `x-kpsdk-st returned by ct API`    | `Yes` |
| `ct`    | `String`  | `x-kpsdk-ct returned by ct API`    | `Yes` |

#### x-kpsdk-ct json example

```json
{
    "href": "https://api.crowdgen.com/149e9513-01fa-4fb0-aad4-566afd725d1b/2d206a39-8ed7-437e-a3be-862e0f06eea3/fp?x-kpsdk-v=j-1.1.0",
    "fp_host": "api.crowdgen.com",
    "fp_html": "<!DOCTYPE html><html><head></head><body><script>window.KPSDK={};KPSDK.now=typeof performance!=='undefined'&&performance.now?performance.now.bind(performance):Date.now.bind(Date);KPSDK.start=KPSDK.now();window.parent.postMessage('KPSDK:MC:CiQxM2RlOTc1Ni1kNmMyLTQ3MDItOTFkZC1hOGUzZDdjOGJjYWU:DllWUiZYDA...",
    "ips_script": "KPSDK.scriptStart=KPSDK.now();\"use strict\";(function(){var C=function(v,u,f){for(var a=u.length,r=a-f,t=[],M=0;M<v.length;)for(var h=0,l=1;;){var x=u.indexOf(v[M++]);if(h+=l*(x%f),x<f){t.push(h|0);break}h+=f*l,l*=r}return t};var s=\"7CI1IKIJIjIAIYIWInIbI4a=5=1<C=1+Z1<C=11N+<C=1K1<C=1Jv+<C=1j8K<C=1A3I...",
    "ips_headers": {
        "via": "1.1 53b2bbb13e5db590d598ee4e9aa9bd80.cloudfront.net (CloudFront)",
        "x-cache": "Miss from cloudfront",
        "p3p": "CP=\"This site does not specify a policy in the P3P header\"",
        "access-control-expose-headers": "x-kpsdk-ct,x-kpsdk-r,x-kpsdk-c",
        "x-kpsdk-r": "1-AA",
        "x-kpsdk-ct": "0ICFRuAoYP3moorFdO2iQq6vhcbHNSygkrDoKFyMREAOjqIRlqlpNMeiyLrd7Pu290rhSTvDyf62nhOZ132LVkI0SZktfWzlGDUS0DJbevip5kghoBdRhf77kApVef89UEOCAYbs6TTKraEhuQapM5FWvU57ixfMj58hSiIR",
        "x-amz-cf-id": "zgHjq3UDbJQexs6W2cdIclz8PSWGffqvOvZWTdexO9nKJMLlUIIX0Q==",
        "pragma": "no-cache",
        "expires": "0",
        "cache-control": "no-cache, no-store, must-revalidate",
        "set-cookie": "KP_UIDz-ssn=0ICFRuAoYP3moorFdO2iQq6vhcbHNSygkrDoKFyMREAOjqIRlqlpNMeiyLrd7Pu290rhSTvDyf62nhOZ132LVkI0SZktfWzlGDUS0DJbevip5kghoBdRhf77kApVef89UEOCAYbs6TTKraEhuQapM5FWvU57ixfMj58hSiIR; Max-Age=86400; Path=/; Expires=Sat, 07 Jun 2025 09:02:51 GMT; HttpOnly; Secure; SameSite=None",
        "date": "Fri, 06 Jun 2025 09:02:51 GMT",
        "x-amz-cf-pop": "HKG62-C2",
        "content-type": "application/javascript; charset=utf-8"
    },
    "cookies": {
        "KP_UIDz-ssn": "0ICFRuAoYP3moorFdO2iQq6vhcbHNSygkrDoKFyMREAOjqIRlqlpNMeiyLrd7Pu290rhSTvDyf62nhOZ132LVkI0SZktfWzlGDUS0DJbevip5kghoBdRhf77kApVef89UEOCAYbs6TTKraEhuQapM5FWvU57ixfMj58hSiIR",
        "KP_UIDz": "0ICFRuAoYP3moorFdO2iQq6vhcbHNSygkrDoKFyMREAOjqIRlqlpNMeiyLrd7Pu290rhSTvDyf62nhOZ132LVkI0SZktfWzlGDUS0DJbevip5kghoBdRhf77kApVef89UEOCAYbs6TTKraEhuQapM5FWvU57ixfMj58hSiIR"
    },
    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/134.0.0.0 Safari/537.36",
    "iframe": true,
    "submit": false,
    "is_auth": false
}
```

#### x-kpsdk-cd json example

```json
{
    "href": "https://xxxxxx/",
    "st": 1716775584627,
    "ct": "value of x-kpsdk-ct"
}
```

### x-kpsdk-ct Response Data (JSON):

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data['x-kpsdk-ct']`   | `String`  | `The available x-kpsdk-ct parameter returned after successful verification, can be used in request headers for subsequent verification APIs`    |
| `data['x-kpsdk-st']`   | `String`  | `Used for subsequent kasada/cd API to generate x-kpsdk-cd parameter, bound with x-kpsdk-ct parameter`    |
| `data['x-kpsdk-cd']`   | `String`  | `The available x-kpsdk-cd parameter returned after successful verification, please recall kasada/cd API to generate this parameter when using ct multiple times`    |
| `data['headers']`   | `Object`  | `/tl API request header parameters`    |
| `data['post_data']`   | `Object`  | `/tl API request body base64 string, please base64 decode before use`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

### x-kpsdk-cd Response Data (JSON):

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data['x-kpsdk-cd']`   | `String`  | `The available x-kpsdk-cd parameter returned after successful verification, can be used in request headers for subsequent verification APIs (can only be used once)`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "4635.12ms",
  "data": {
    "x-kpsdk-st": 1716775584627,
    "x-kpsdk-cd": "{\"workTime\":1716775584627,\"id\":\"e7910834208cfc67a3340ff934bdb5b1\",\"answers\":[9,9],\"duration\":39,\"d\":1886,\"st\":1716775584814,\"rst\":1716775586700}", 
    "x-kpsdk-ct": "0aTWZlyuZj8xdBYhR3kCblUF4ljSLJNyk8LWEbjERVaayHo5DUU5VTEh7NWYldd5brUpu0KHOR38y2H6ObgzziQA28FKq4i5DX14UVmY93efP2ejJNYybda4Tmqc6v2EscnP4K3tEAxP1a7uUtPEXMuTYutYLhSrDxOEzJa"
  }
}
```

```json
{
  "status": 1,
  "msg": "验证成功",
  "id": "639e056b-49bd-4895-94ab-68d59e00873e",
  "cost": "1635.12ms",
  "data": {
    "headers": {
      "x-kpsdk-im": "CiRmOTgyZTY5Yy0wMDZhLTQ1YzEtYjllZS03NzY2MWY5NDIzZjg",
      "x-kpsdk-ct": "0KbYqxscaXy3q8xoCxrGhYnKwCX08pVkjSQJ45g7hZhzvyvemuDkgGpv5eV3B6vV2UhWOuE8NInnv8oBcxlmqFk8gOAquRxuv5vl7m4O9qqnOwdBBWY7ufrBz6kdDpSOn9cYuiWkpad71lKwUszx7KzLHDcqQxx3ccwPTnYd",
      "x-kpsdk-dt": "1020nz6ax72z29w4lw11uow37w5f",
      "x-kpsdk-v": "j-0.0.0"
    },
    "post_data": "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"
```

### Call Example

#### python (Strongly recommend using pynocaptcha encapsulated calling method, other methods cannot guarantee pass rate)

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
# pip install --upgrade pynocaptcha
from pynocaptcha import crack_kasada, KasadaCdCracker
# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from utils import USER_TOKEN, get_idea_proxy

href = 'https://app.crowdgen.com/'

session, kpsdk_res, extra = crack_kasada(
    user_token=USER_TOKEN,
    href='https://api.crowdgen.com/149e9513-01fa-4fb0-aad4-566afd725d1b/2d206a39-8ed7-437e-a3be-862e0f06eea3/fp?x-kpsdk-v=j-1.1.0',
    proxy=get_idea_proxy("hk"),
    debug=True
)

kpsdk_ct = kpsdk_res['x-kpsdk-ct']
kpsdk_st = kpsdk_res['x-kpsdk-st']
kpsdk_v = kpsdk_res['x-kpsdk-v']

kpsdk_cd = KasadaCdCracker(
    show_ad=False,
    internal_host=True,
    user_token=USER_TOKEN,
    href=href,
    ct=kpsdk_ct,
    st=kpsdk_st,
    debug=True
).crack()["x-kpsdk-cd"]

headers = {
    'accept': 'application/json, text/plain, */*',
    'accept-language': session.client_hints['accept-language'],
    'authorization': 'Bearer undefined',
    'content-type': 'application/json',
    'origin': 'https://app.crowdgen.com',
    'priority': 'u=1, i',
    'referer': 'https://app.crowdgen.com/',
    'sec-ch-ua': session.client_hints['sec-ch-ua'],
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': session.client_hints['sec-ch-ua-platform'],
    'sec-fetch-dest': 'empty',
    'sec-fetch-mode': 'cors',
    'sec-fetch-site': 'same-site',
    'user-agent': session.client_hints['user-agent'],
    'x-kpsdk-cd': kpsdk_cd,
    'x-kpsdk-ct': kpsdk_ct,
    'x-kpsdk-v': kpsdk_v,
}

json_data = {
    'email': 'rwegfv@gmail.com',
    'password': 'klwubfrewfg2123',
}

response = session.post('https://api.crowdgen.com/api/v1/user/auth/login', headers=headers, json=json_data)
print(response.status_code, response.text)
```
