[`Back to Home`](en.md)    [`Previous`](akamai.md)    [`Next`](cloudflare.md)    [`中文文档`](../zh-CN/tls.md)

## Tls Client

### Request URL (POST):

| Version          | API Address                                |
|------------------| ------------------------------------------ |
| `v1 (universal)` | `http://api.nocaptcha.io/api/wanda/tls/v1` |

### Request Headers:

| Parameter      | Description                                                  | Required |
| -------------- | ------------------------------------------------------------ | -------- |
| `User-Token`   | `User key, obtain from homepage`                             | `Yes`    |
| `Content-Type` | `application/json`                                           | `Yes`    |
| `Developer-Id` | `Developer ID, used by developer users, string from user homepage invite link (e.g., if link is xxx/register?c=abcdef, then abcdef is the developer ID)` | `No`     |

### POST Data (JSON):

| Parameter       | Type               | Description                                                  | Required |
| --------------- | ------------------ | ------------------------------------------------------------ | -------- |
| `url`           | `String`           | `Request URL address`                                        | `Yes`    |
| `method`        | `String`           | `Request method, get/post`                                   | `No`     |
| `headers`       | `String or Object` | `Request headers, can be string or object, default headers are {'User-Agent': 'random ua'}` | `No`     |
| `cookies.value` | `String or Object` | `Cookies used in the request process, can be string or object, e.g., {'1': '2', '3': '4'} or '1=2; 3=4'` | `No`     |
| `cookies.uri`   | `String`           | `Domain where cookies are set during the request process, use URL` | `No`     |
| `proxy`         | `String`           | `Proxy used in the request process. Supported protocols: http/https/socks5. Format for no-auth proxy: {ip}:{port}. Auth proxy format: {user}:{password}@{ip}:{port}. For socks5 proxy, include the protocol: {protocol}://{ip}:{port}` | `No`     |
| `data`          | `String or Object` | `Body for post request, can be string or object, e.g., {'1': '2', '3': '4'} or '1=2&3=4'` | `No`     |
| `json`          | `String or Object` | `Json data for post request, example {'1': '2', '3': '4'}`   | `No`     |
| `timeout`       | `Number`           | `Request timeout (in seconds), default is 15 seconds`        | `No`     |
| `http2`         | `Boolean`          | `Whether to use http2 protocol, default is false`            | `No`     |
| `redirect`      | `Boolean`          | `Whether to follow redirects, default is true`               | `No`     |
| `ja3`           | `String`           | `Custom ja3 fingerprint. If not provided, it defaults to the latest random Chrome fingerprint` | `No`     |

#### JSON Example

```
{
    "url": "https://api-fashion.dior.com/graph?SubscribeNewsletter",
    "method": "post",
    "headers": {
        'Accept-Language': 'zh-CN,zh;q=0.9',
        'Cache-Control': 'no-cache',
        'Connection': 'keep-alive',
        'DNT': '1',
        'Origin': 'https://www.dior.com',
        'Pragma': 'no-cache',
        'Referer': 'https://www.dior.com/',
        'Sec-Fetch-Dest': 'empty',
        'Sec-Fetch-Mode': 'cors',
        'Sec-Fetch-Site': 'same-site',
        'User-Agent': 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/114.0.0.0 Safari/537.36',
        'accept': '*/*',
        'apollographql-client-name': 'Newlook Couture Catalog K8S',
        'apollographql-client-version': '5.282.3-8601f7a7.hotfix',
        'content-type': 'application/json',
        'sec-ch-ua': '"Not.A/Brand";v="8", "Chromium";v="114", "Google Chrome";v="114"',
        'sec-ch-ua-mobile': '?0',
        'sec-ch-ua-platform': '"macOS"',
        'x-dior-locale': 'zh_hk',
        'x-dior-universe': 'onedior',
    },
    "cookies": {
        "value": "_abck=D719B7C0C6B1EBE8FC8F5C1B804B2265~-1~YAAQJescuEJsVzWIAQAAnwAZQQkN297mPe+Q48Xd0/10jSvgz/y69qQbPEwxUuQZhIhisL+GFAMfvabHtQPRUbiIqzDD6vA9iN9lvjzaAbKaL+aNXF/3EhpYYYUsBa0q92JUxusD8F09nFXy3mfZ8p8GzDk+/ikw4Y8QVQcchjC/s6XYbG+I2RSHl+lDOSvR2biGLFZ1dW2PsFZQ6Fs4M1/ccWfaXg6IRvzjlWaF0vH8GIoljDVRvZxwCeUO71QJORFxeVEEO43BiC3LczJhMomt8pnTbnJcMbMbi1zFcYUKUZjYvB7+kJ1JsMHfVdzbrwTB2I3bePGPgX06RvzCReVCETYpJB7H+XEeJgQQDzKiYZhCONfnae3BQUll~-1~-1~1684722838; bm_sz=751A827227D797408E66A3559D978757~YAAQpVcyuNsPVjCIAQAAMTCrRhNw86NLVNcBypYZvOkbMMnc+ef6EeDWu9UtvPw3OfyfpKLmEFQeDw99mddahdMlOj3VxzPz8eV9mfMSWDLxup33fIKAvsMvnUjvAJV0gpZvTTwdk0atKXCg1DXvs+U+VOvPPJtS76B2t+r0jXrB+cUm2hJL7qF59kbHLBl54yypauoWa1qEu9lgelS5kdwiR93A0c9IRagfLG4VjFydhZBoD6ldWEQjQUflrf00GSoxQpL0QBKRlD7fFNRtMhBmndvu5yoGdixtPXCEKk5BzRl/~4605506~4276528; ak_bmsc=0E5236AFD795DD698B2E15191CEF0FDC~000000000000000000000000000000~YAAQpVcyuNoPVjCIAQAAMTCrRhNkrxzrgkZ1QP7XH0+hyJ2ul+4V0reJDlf1omJylP4/7vc+bxfB8EW1pfuYQWdBmzTBnE84h+7tH1SbFvNNNDul53BJsoOd79t8V0LGQdlXls3FWxITVSwuVlvCQTuJY1jq+uxrTTFFWpuqWQZnWkaLC/p8E7KRycXTaDSh7UW4k6ISRmssUftgDxwjZg43T6IbMyPf9dugLQSg9dKx4p8wyTcNern/fHfx7dAABbnUJkwmP+Y/eR4mfc9MJtIsJ3006DKH7PNoZ5JhtmnN9JTuhwfSEEnCrhs0j/cb2TrsSMo26w4C1xIaUNwZXE77YDci8VIkwEq9NvSTrTZUncSl0rsvoBz0j4QheSI=",
        "uri": "https://www.dior.com/"
    },
    "json": {
        "operationName": "SubscribeNewsletter",
        "variables": {
            "input": {
                "newsletters": {
                    "couture": true,
                    "beauty": false
                },
                "profiling": {},
                "user": {
                    "title": "Mme",
                    "email": "1456551412@qq.com",
                    "firstName": "afasdf",
                    "lastName": "qweqwe"
                }
            }
        },
        "query": "mutation SubscribeNewsletter($input: NewslettersOptinLegacyInput!) {\n  subscribeNewsletter(input: $input) {\n    success\n    errorMessages\n    errorDetail\n    __typename\n  }\n}\n"
    },
    "proxy": "socks5h://123:456@127.0.0.1:1234",
    "http2": true,
    "redirect": false,
    "ja3": "771,4865-4866-4867-49195-49199-49196-49200-52393-52392-49171-49172-156-157-47-53,5-43-18-10-13-51-23-16-17513-27-65281-35-45-0-11-21,29-23-24,0"
}
```

### Response Data (JSON):

| Parameter       | Type      | Description                                                  |
| --------------- | --------- | ------------------------------------------------------------ |
| `status`        | `Integer` | `Call success status, 1 for success, 0 for failure, use this value to determine` |
| `msg`           | `String`  | `Chinese description of call result`                         |
| `id`            | `String`  | `Unique ID for this request (can be used for subsequent record queries)` |
| `data.status`   | `Number`  | `Response status code`                                       |
| `data.text`     | `String`  | `Response body`                                              |
| `data.cookies`  | `String`  | `Response cookies`                                           |
| `data.location` | `String`  | `Redirect URL`                                               |
| `cost`          | `String`  | `Validation time (in milliseconds)`                          |

```
{
    "status": 1,
    "msg": "验证成功",
    "id": "049bfae2-4e84-4f29-99aa-a33688991355",
    "cost": "1414.15ms",
    "data": {
        "response": {
            "status": 200,
            "text": "{\"data\":{\"subscribeNewsletter\":{\"success\":true,\"errorMessages\":null,\"errorDetail\":null,\"__typename\":\"NewsletterOptinResponse\"}}}\n",
            "tls": {
                "ja3": '771,4865-4866-4867-49195-49199-49196-49200-52393-52392-49171-49172-156-157-47-53,51-23-43-45-27-17513-5-11-18-10-13-0-35-65281-16-21-41,29-23-24,0',
                "ja3_hash": '2795d91de2c9d7e36984350e338ddc9a',
                "akamai": '1:65536,2:0,3:1000,4:6291456,6:262144|15663105|0|m,a,s,p',
                "akamai_hash": '46cedabdca2073198a42fa10ca4494d0'
            },
            "cookies": "dtCookie=v_4_srv_5_sn_2A2A9F901F6BE925EF475041C744108A_perc_100000_ol_0_mul_1_app-3Aea7c4b59f27d43eb_1; _abck=6D43584C164A308CFC85AE1462D56CD1~0~YAAQpqg7FxN5F5+IAQAAXFwfvgpoxc0IH5DxeBHUCgDMC4vh8eHRZkqMr5rUFAxg+Zjwi0ouU4PF9WIT9rdcJtenDDu9T438N+xtPqd0JdzKePw3Y7u7OJkZe95KAzQ/L9VqCPLEvHC9Nap2ELrgIY32GRzJKj2qgPmuX4avgoopJmJ7hLhfq9rGwqkfBWaykDHs1MHb8xSjmr/bGbDHbpzSlThrEU8PlKxL/QWOIgPDyD/hZWi5wVyLG5zim5hVeykHZEiXgucS9u/gTHUGMmlz+EZU+Gj1rZ5/vMRqe9mieGJj+93IZElOAdT5SeXmmr++XZx8PEJaE8UTj+gCADhi74Up9AR7HxFcL5yI2uixdkQt28OYUzA4JwGmk2YpBDH4ZIVTnsxQ2TmlmtC4U3Avhw==~-1~-1~-1; ak_bmsc=A512C03708A82AF15509075AC3463465~000000000000000000000000000000~YAAQpqg7FxR5F5+IAQAAXFwfvhTDvOQ0kF5T1aOHbbK5JhAaIMLCpBliUMAWu13oybOeiok1hxUFG20Mp1stJJbQxgyROf+1V15DXyjemkWmqrjmeJOn8Mvpc4WCREAxrm7Zc8lwhFROzvGnSnX4kddVIId8yePfkYELbxCjEV1jOCqj51hz8iyF5C76Ee02geGNTfpR0DwllMVnNxFDnhIJBhUjZ7XMbPta1zFJndZ4WuOdqzWVt/U/F6Iqq73eEV9oGQLxj6xDMd+PTLWB67ogSnDsG3HsFTrX9H8zC7Ql4o36B8lvAJQL8Nnyj36ezqJSOUoxweZuhsnpOajJ3qLPdsRrkqueMEXtFXFMbBs/uNKCAssX/edlkFM=; bm_sz=3C1D2E1D2A280881BAAD40C1A120F210~YAAQpqg7FxV5F5+IAQAAXFwfvhSWkY43adkIgLvfWY2v1NZKi/+2KElW+DrSt0lTZfVqiV4mpq4lDVgpuDAl3o7ttti5s2JA/WkrvIXeZKHFSDvEFwS6E3Moe7bCInlKFHSG1BvjrBoRTdHhDrIc9LEDNx2pWqhpdTs0pp3ZqouXmjVRvHHFTXh6k5Ct3vIVnyUvY6eHcvoa4ILtkvKKaY5fitwBt5OdMDa/3IJYgdeFGWXdwAZOoP5y9sO0IriqCJBQns2q+UYebGi4Y3ZO27Vu6JDOOz/NkP+8w+1Jr2xN~3487801~3359042"
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
from pynocaptcha import TlsV1Cracker

cracker = TlsV1Cracker(
    user_token="xxx",
    url="https://www.baidu.com/",
)
ret = cracker.crack()
print(ret)
```
