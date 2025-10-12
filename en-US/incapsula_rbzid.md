[`Back to Home`](en.md)    [`Previous`](incapsula_utmvc.md)    [`Next`](akamai.md)    [`中文文档`](../zh-CN/incapsula_rbzid.md)

## Incapsula (rbzid)

### rbzid Situation
* When requesting incapsula scripts, if you get the following, it means rbzid is triggered (kramericaindustries.ac.lib.js, window.rbzns...)
![rbzid](/images/incapsula/rbzid.png)

### Usage of Result
* Keep ua consistent, use the returned verify_url, headers GET to get returned cookies, and keep ua and cookies for subsequent requests
* The returned request header is fixed as x-zebra-zebra, if you want random, use x-zebra- + random(5)

### Request URL (POST):

| Version               | API URL                                                    |
|-------------------|---------------------------------------------------------|
| `rbzid` | `http://api.nocaptcha.io/api/wanda/incapsula/rbzid` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### POST Data (JSON):

| Parameter Name          | Type        | Description  | Required  |
|--------------|-----------|----------------------|-----|
| `href`        | `String`  | `URL of the rbzid script` | `Yes` |
| `user_agent` | `String`  | `ua must be consistent for rbzid cookies, so pass the ua you will use`  | `Yes` |
| `script` | `String`  | `Script result from href request` | `Yes` |

#### json example

```json
{
    "href": "https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=719d34d31c8e3a6e6fffd425f7e032f3",
    "script": "result from href request",
    "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
}
```

### Response Data (JSON):

| Parameter Name            | Type        | Description                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `Whether the call was successful, 1 for success, 0 for failure. Use this value to judge` |
| `msg`          | `String`  | `Chinese description of the result`                    |
| `id`           | `String`  | `The unique request ID for this particular request (can be used for subsequent record queries)`      |
| `data` | `Object`  | `Contains verify_url and headers for subsequent verification`    |
| `cost`         | `String`  | `Verification time taken (in milliseconds)`                    |

```json
{
    "status": 1,
    "msg": "验证成功",
    "id": "61b4bb7f-abf9-4875-ae58-38916e1ecbff",
    "cost": "36.42ms",
    "data": {
        "x-zebra-zebra": "ZDM4ZjBlMjcyOGE1MjhmY2E3ZTFjNjNlODRiN2EyN2RlMzA5ZWM4MTskKGhhc2gpO194Y2FsYyhhcmd1bWVudHMuY2FsbGUpOzA7JChoYXNoKTtfeGNhbGMoYXJndW1lbnRzLmNhbGxlKTstNTkyNTkyNTg3MjA7JChoYXNoKTtfeGNhbGMoYXJndW1lbnRzLmNhbGxlKTtkaXNhYmxlZDskKGhhc2gpO194Y2FsYyhhcmd1bWVudHMuY2FsbGUpOzEyMzEyMw==", 
        "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
    }
}
```

### Call Example

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
from pynocaptcha import IncapsulaRbzidCracker

cracker = IncapsulaRbzidCracker(
    user_token="xxx",
    href="https://premier.hkticketing.com/_Incapsula_Resource?SWJIYLWA=719d34d31c8e3a6e6fffd425f7e032f3",
    script="result from href request",
    user_agent="Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/120.0.0.0 Safari/537.36"
)
ret = cracker.crack()
print(ret)
```
