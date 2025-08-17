------
[`Back to Home`](en.md)    [`Previous`](hcaptcha.md)    [`Next`](incapsula_utmvc.md)    [`中文文档`](../zh-CN/incapsula.md)

## Incapsula ( reese84 )

### FAQs

* Where is the submitted `href` in the interface? (In cases with multiple `src`, choose the link with the `async` keyword)
    * ![incapsula](/images/incapsula/incapsula.png)
* Example of href response (The response will include code similar to `ob` obfuscation)
    * ![incapsula](/images/incapsula/incapsula2.png)

### Why Choose Us

* Universality: All known sites can pass verification.
* Supreme Speed: Interface uses `pure algorithm` to calculate parameters, with `protocol submission` and `synchronous return`.
* Stability: Timely updates (no more than two hours) to better support your business.

### Request URL (POST):

| Version               | Interface URL                                                |
|-------------------|---------------------------------------------------------|
| `reese84 (universal)` | `http://api.nocaptcha.io/api/wanda/incapsula/reese84` |

### Request Headers:

| Parameter Name | Description | Required |
|----------------|-------------|----------|
| `User-Token`   | `User secret key, obtained from homepage` | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, used by developer user. Invitational link string on user homepage (e.g. xxx/register?c=abcdef, then abcdef is developer ID)` | `No` |

### POST Data (JSON):

| Parameter Name | Type       | Description | Required |
|----------------|------------|-------------|----------|
| `href`         | `String`   | `The address to get incapsula js when triggering incapsula verification` | `Yes` |
| `user_agent`   | `String`   | `User agent used for the request process. Subsequent request checks for UA consistency, so please pass the UA you will use for subsequent requests.` | `Yes` |
| `cookies` | `Object`  | `Use when a message is displayed indicating that cookies containing rbzid and rbzsessionid are required`                                                                                                      | `No` |


#### json example:

```
{
  "href": "https://www.priceline.com.au/Cawdor-asse-my-Nightning-we-from-Dealell-Come-Ty",
  "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/108.0.0.0 Safari/537.36",
}
```

### Response Data (JSON):

| Parameter Name  | Type       | Description |
|-----------------|------------|-------------|
| `status`        | `Integer`  | `Call success status, 1 for success, 0 for failure, please use this value for judgment` |
| `msg`           | `String`   | `Description of the call result in English` |
| `id`            | `String`   | `Unique request ID for this call (can be used for subsequent record queries)` |
| `data.solution` | `String`   | `The returned solution after verification, can be used for subsequent requests to get resee84 interface` |
| `cost`          | `String`   | `Verification time taken (in milliseconds)` |

```
{
  'status': 1,
  'msg': 'Verification successful',
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


### Example Call

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
