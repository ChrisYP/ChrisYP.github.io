[`Back to Home`](en.md)    [`Previous`](datadome.md)    [`Next`](vercel.md)    [`中文文档`](../zh-CN/shape.md)

## Shape

### Description
* Parameter invocation is very complex, strongly recommend using `pynocaptcha` directly, see the python example below!
* When you see `x-xxxx-a` or `xxxx-a` in request headers or post form/json, it means `shape` verification exists
* How to distinguish `v1`/`v2`:
  * Open f12 and enter `window.__xr_bmobdb`, if it outputs an object, it's `v1`; if it outputs `undefined`, it's `v2`

### Request URL (POST):

| Version               | API URL                                                    |
|------------------|---------------------------------------------------------|
| `v1` | `http://api.nocaptcha.io/api/wanda/shape/v1` |
| `v2` | `http://api.nocaptcha.io/api/wanda/shape/v2` |

### Request Headers:

| Parameter Name            | Description                 | Required  |
|----------------|--------------------|-----|
| `User-Token`   | `User secret, get from homepage`       | `Yes` |
| `Content-Type` | `application/json` | `Yes` |
| `Developer-Id` | `Developer ID, for developer users, string from homepage invite link (e.g. xxx/register?c=abcdef, then abcdef is Developer ID)`           | `No` |

### shape/v1 POST Data (JSON):

| Parameter Name          | Type        | Description                                                                                                                                                             | Required  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `Page URL that triggers shape verification`    | `Yes` |
| `vmp_url`    | `String`  | `shape vmp script url`    | `Yes` |
| `vmp_content`    | `String`  | `shape vmp script content`    | `No` |
| `country`    | `String`  | `Country code of proxy used in business flow, e.g. US (us), UK (uk), consult admin for details`    | `No` |
| `ip`    | `String`  | `IP address of proxy used in business flow (e.g. 56.214.78.94), consult admin for details`    | `No` |
| `user_agent` | `String`  | `Custom user_agent, must keep user-agent consistent, please use latest Windows UA`       | `No` |
| `cookies` | `Object`  | `Requesting shape script vmp_url will return a cookie like A-pOe7WQAQAA6ZxjB-L2qpl728w8qxyqvIEfRgLl4tjbeVlhQKHxkNAbbgGOATo-EwCucuopwH9eCOfvosJeCA|1|0|7895d35189a49738f34d2f7126c4b88094e685a2, please upload`       | `No` |
| `fast` | `Boolean`  | `Accelerate calculation, default false (can use if website risk control is low)`       | `No` |
| `timeout` | `Integer`  | `Verification timeout`       | `No` |

#### json example

```
{
  "href": "https://www.starbucks.com.cn/account",
  "vmp_url": "https://cards.starbucks.com.cn/esabxubs5h.js",
  "vmp_content": "(function d(id,q,y,h){var iH=ReferenceError,iB=TypeError,iV=Object,iT=RegExp,ip=Number,iW=String,ic=Array,iM=iV.bind,iL=iV.call,is=iL.bind(iM,iL),f=iV.apply,ie=is(f),J=[].push,r=[].pop,v=[].slice,P=[].splice,k=[].join,D=[].map,Z=is(J),c=is(v),z=is(k),w=is(D),a={}.hasOwnProperty,io=is(a),p=JSON.strin",
  "country": "hk",
  "ip": "50.114.59.26"
}
```
