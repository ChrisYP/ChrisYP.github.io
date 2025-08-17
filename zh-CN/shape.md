------

[`返回首页`](../README.md)    [`上一页`](datadome.md) [`下一页`](vercel.md)    [`English Version`](../en-US/shape.md)

## Shape

### 说明
* 参数调用非常复杂，强烈建议直接使用 `pynocaptcha`，详情看下面 python 示例！！！
* 当看到 `请求头` 或者 `post 表单/json` 中有 `x-xxxx-a` 或者 `xxxx-a`, 代表存在 `shape` 验证
* 如何区分 `v1`/`v2`:
  * 打开 f12 输入 `window.__xr_bmobdb`, 看看是否会输出一个对象, 如果输出了就是 `v1`, 输出的是 `undefined` 就是 `v2`

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `v1` | `http://api.nocaptcha.io/api/wanda/shape/v1` |
| `v2` | `http://api.nocaptcha.io/api/wanda/shape/v2` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### shape/v1 POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `触发 shape 验证的页面地址`    | `是` |
| `vmp_url`    | `String`  | `shape vmp 脚本的 url`    | `是` |
| `vmp_content`    | `String`  | `shape vmp 脚本内容`    | `否` |
| `country`    | `String`  | `业务流程使用的代理所属地区国家 code, 如美国（us）、英国（uk）, 详情可咨询管理`    | `否` |
| `ip`    | `String`  | `业务流程使用的代理流程的 ip 地址（例: 56.214.78.94）, 详情可咨询管理`    | `否` |
| `user_agent` | `String`  | `自定义 user_agent, 必须保持 user-agent 一致, 请传最新版 windows ua`       | `否` |
| `cookies` | `Object`  | `请求 shape 脚本 vmp_url 会返回一个类似 A-pOe7WQAQAA6ZxjB-L2qpl728w8qxyqvIEfRgLl4tjbeVlhQKHxkNAbbgGOATo-EwCucuopwH9eCOfvosJeCA|1|0|7895d35189a49738f34d2f7126c4b88094e685a2 的 cookie, 请携带上传`       | `否` |
| `fast` | `Boolean`  | `是否加速计算, 默认 false （网站风控低可使用该模式）`       | `否` |
| `timeout` | `Integer`  | `验证超时时间`       | `否` |

#### json 示例

```
{
  "href": "https://www.starbucks.com.cn/account",
  "vmp_url": "https://cards.starbucks.com.cn/esabxubs5h.js",
  "vmp_content": "(function d(id,q,y,h){var iH=ReferenceError,iB=TypeError,iV=Object,iT=RegExp,ip=Number,iW=String,ic=Array,iM=iV.bind,iL=iV.call,is=iL.bind(iM,iL),f=iV.apply,ie=is(f),J=[].push,r=[].pop,v=[].slice,P=[].splice,k=[].join,D=[].map,Z=is(J),c=is(v),z=is(k),w=is(D),a={}.hasOwnProperty,io=is(a),p=JSON.strin",
  "country": "hk",
  "ip": "50.114.59.26",
  "cookies": {
    "ZHh6ku4z": "A-pOe7WQAQAA6ZxjB-L2qpl728w8qxyqvIEfRgLl4tjbeVlhQKHxkNAbbgGOATo-EwCucuopwH9eCOfvosJeCA|1|0|7895d35189a49738f34d2f7126c4b88094e685a2"
  }
}
```

### shape/v2 POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|-----------------------------|-----|
| `href`    | `String`  | `触发 shape 验证的页面地址`    | `是` |
| `script_url`    | `String`  | `加载 shape vmp 脚本的 url 地址, 如星巴克的 https://www.starbucks.com/vendor/static/vendor2.js`    | `是` |
| `script_content`    | `String`  | `请求 script_url 返回的脚本内容`    | `是` |
| `vmp_url`    | `String`  | `shape vmp 脚本的 url, 可在 script_content 中匹配出来, 如 https://www.starbucks.com/vendor/static/vendor2.js?seed=AABWGBuTAQAA6Zew1TZ6gymxqAG9Psjx9XG4bdlus6mvja5FZEUuo1TX9R7z&X-DQ7Hy5L1--z=q`    | `是` |
| `pkey`    | `String`  | `shape 加密参数名, x-xxxx-a 中的 xxxx, 如星巴克的 Dq7hy5l1-a 传  dq7hy5l1 即可`    | `是` |
| `request`    | `Object`  | `需要 shape 签名的接口内容`    | `是` |
| `request.url`    | `String`  | `需要 shape 签名的接口地址`    | `是` |
| `vmp_content`    | `String`  | `请求 vmp_url 返回的脚本内容`    | `否` |
| `title`    | `String`  | `需要 shape 请求头参数的接口在的页面的 document.title, 打开 f12 执行 document.title 上传即可, 如 'Starbucks Gift Cards: Starbucks Coffee Company'`    | `否` |
| `proxy`    | `String`  | `若不传 vmp_content, 请传代理, 保持代理一致, 若传代理请使用海外代理, 格式请传 ip:port 或 usr:pwd@ip:port (如果有问题联系管理员)` | `是` |
| `country`    | `String`  | `业务流程使用的代理所属地区国家 code, 如美国（us）、英国（uk）, 详情可咨询管理`    | `否` |
| `ip`    | `String`  | `业务流程使用的代理流程的 ip 地址（例: 56.214.78.94）, 详情可咨询管理`    | `否` |
| `timezone`    | `String`  | `业务流程使用的代理流程的 ip 所属时区（例: America/New_York）, 详情可咨询管理`    | `否` |
| `cookies` | `Object`  | `请求 shape 脚本 vmp_url 会返回一个类似 A04OirWQAQAANesrkEhwOdwESUmWxhQzua76waOt-AY_zSZ4Q1_OPyKoH8YwATJyOxqucgzkwH8AAEB3AAAAAA|1|0|62c86f9725a57529763eb86405e270eea098bfae 的 cookie, 请携带上传`       | `否` |
| `user_agent` | `String`  | `自定义 user_agent, 必须保持 user-agent 一致`       | `否` |
| `timeout` | `Integer`  | `验证超时时间`       | `否` |

#### json 示例

```
{
  "href": "https://www.westjet.com/shop/flight/0?bookid=18-6-2024-1-27-23-95292&lang=en-CA&urlRef=flight-search-results",
  "script_url": "https://www.westjet.com/resources/js/wj_common.js",
  "pkey": "Lov30h0l",
  "request": {
    "url": "https://apiw.westjet.com/ecomm/booktrip/flight-search-api/v1"
  },
  "script_content": "(function(a){var d=document,w=window,u=\"https://www.westjet.com/resources/js/wj_common.js?seed=AEBPg7WQAQAA-wSGc73uzuqyWivL_q0-pId3jk0-P9fHqlorpRQ7P2ZOYs6c&X-Lov30h0l--z=q\",v=\"EvVUDquOd\",i=\"8c4bbc2ac85d070d228a99eb9f47e34a\";if(d.readyState===\"complete\")return;var s=d.currentScript;addEventListener(v,function f(e){e.stopImmediatePropagation();removeEventListener(v,f,!0);e.detail.init(\"A04OirWQAQAAbDc-6r9TVNNycNikz9AHA6AzssVISjXK3F0ItV_OPyKoH8YwATJyOxqucgzkwH8AAEB3AAAAAA==\",\"ib3njszMTrZUftxF6d=ghoHaKclSqNwC8OmV_5LIA2BEJ019kyRu4XY-G7PWQDvep\",[],[1651724521,1195406625,1507366028,1673653107,252694798,299067874,2050858889,983183815],document.currentScript&&document.currentScript.nonce||\"hBFgTukj3RzCZHYKWYU2tmnr\",document.currentScript&&document.currentScript.nonce||\"hBFgTukj3RzCZHYKWYU2tmnr\",[],a)},!0);var o=s&&s.nonce?s.nonce:\"\";try{s&&s.parentNode.removeChild(s)}catch(e){}{if(d.readyState!==\"complete\"){var p=\"<script\";p+=' nonce=\"'+o+'\"';d.write(p+' src=\"'+u+'\" id=\"'+i+'\"></scr'+\"ipt>\")}}}(typeof arguments===\"undefined\"?void 0:arguments))",
  "vmp_url": "https://www.westjet.com/resources/js/wj_common.js?seed=AEBPg7WQAQAA-wSGc73uzuqyWivL_q0-pId3jk0-P9fHqlorpRQ7P2ZOYs6c&X-Lov30h0l--z=q",
  "vmp_content": "(function v(g){var uK={},uc={};var ur=ReferenceError,us=TypeError,uk=Object,uF=RegExp,uO=Number,uM=String,uy=Array,uv=uk.bind,uu=uk.call,uL=uu.bind(uv,uu),c=uk.apply,un=uL(c),J=[].push,q=[].pop,A=[].slice,H=[].splice,N=[].join,D=[].map,n=uL(J),a=uL(A),d=uL(N),h=uL(D),B={}.hasOwnProperty,P=uL(B),W=JS",
  "user_agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36",
  "country": "hk",
  "ip": "50.114.59.26",
  "cookies": {
      "z0t0U8fo": "A04OirWQAQAANesrkEhwOdwESUmWxhQzua76waOt-AY_zSZ4Q1_OPyKoH8YwATJyOxqucgzkwH8AAEB3AAAAAA|1|0|62c86f9725a57529763eb86405e270eea098bfae"
  },
}
```

`vmp` 脚本地址一般为 `*?seed=*&x-xxx--z=q`, 个别网站特殊, 找不到可以联系管理员

### Response Data（JSON）:

#### 提交验证（submit=true）

| 参数名            | 类型        | 说明                            |
|----------------|-----------|-------------------------------|
| `status`       | `Integer` | `调用是否成功, 1 成功, 0 失败, 请使用该值判断` |
| `msg`          | `String`  | `调用结果中文说明`                    |
| `id`           | `String`  | `该次请求 id（唯一, 可用作后续记录查询）`      |
| `data`         | `Array`   | `加密参数数组`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
  "status": 1,
  "msg": "验证成功",
  "id": "811c8e4b-87fc-434d-a7f7-6b79013998df",
  "cost": "1564.7ms",
  "data": [
    {
      "X-DQ7Hy5L1-a": "UbSciDbqiGFciQQlPzRdIkGDQhF5X3FxcGtsis63XbMuoJ5tozgk0r1_lZg9nAPAhpG2_qgtO9t8ywquCHQmQBMbhoco_K8chAsbSujxEGWwUOyuD4USb_vrQ7K52IN-EJIYYtC0g90uvAOCr98bgINpWo4b2q9=errzmy0lvO=D8GOtwNnWtg5FHh1gAggUSg9cKocScYAzfTCcp-nvm2hGL9EcHeQzzlRRRKb-JDjW65ZEqX-kfmSJhbnfMu-q3ePHXvjq_XBxct9IP7dO2hc-eMsWPN3EDs3_cavYpP2bqYUSD-a2v5WZnTbik=ctsdXZyEy21rmpARn-jzGrIFMTclBygb8lw2WPbFAu5yz3EqK06PePtqPalNzS6DBarM8SAQ0UgkBXDG6jipluflHWnJ963Uop0MaZ--ToaiorYu3KrAfBs4jw6PAJJHpJ6Mxr1WyW9yw03i-7TUZ-uWu6Z-==ue6sAwILQFNl0HJwij_5j9dpnTmZeu4piiNvA--03hKXubfBMMcfjEEF3w4ncvtef-6nmPUdaWd7xWKlDGjgztA4aj1XZ3SrdoSqebPsaknMIQ2xEWDEYlRyu7yUAZZFOQn_5nshhzdKJEtxIOZ-vQOkkThGFvyU1opHh0UjYuAp7utm2Yh_WCzIsvoKbiWwZxAGbNZojlD9YFQCBjM7JLyiKxfb5bOdfFX069dswSY13MzKFaMjBo9x2X=d1I3l8oCXBxr2eagd5ezMDTd87w7T30c3nsm56h8HCDr5RLnmNiiTrpopPw-Bhw3HQzfrIruJtKRCN_PL8HjXfOy6Fkf6M5RIWEjJfOwltA37c_G5tIfhTzz4MBHzJZEwwJYYGyEh8bjCR6RAAO2qPlBsZHHATOsfflK0-BtGNYXeOuJEOWAwgRnbtgf_cCQSXKXdAheSnkJcSG1gqoikkKF_1nyRKgfT2DFORKnCPv7n8MtuSmcPGzC2Ic_5zsT9EOXUka0cKOdx=GCCF_=f8b3De0k3OcIp0925tc49wI_58PtxAoxLOc9WYeUqjG30mW=ZF7gq0Jlvj8Moi7zP__lvEnIoBLcjs0yTtFxrnSln=3BRrRQx4_X9UC6HUSjLbEXH2jOa8RD9g=54WF6w9gHCDJ8TI1MAIh6l6JIfMoM5E8cR3AS0FG_YUM7SvsumM3rYj=cF4BAZ941T7bzJt68KQmSd2XHnOawtONf-vOsWn3LB=I4jXziiIT8m0Z2b5WcHUs=7hXRwNLMNaqdvOoLJrFg7nJ6KjGdv4d2aC3xMgQA_0yEN2_ukoENxhaW23R=12Qr4mRjx2MZXsNFSShIFf6eb6vCK9TF=Ors-5xWahx4G2e7x-B51byceMOQo3YjcBrmNeOstDJWeoFTwxnIaeJOgaRPok8fNlNkYQwM13axg21oKvZyMTW15wQNXaNIRkZNWURry3zNepv-U2_QqZbgPNQ6RdUWyA8yY=dousm4hxiWdZKmhAx1cZNsy3lvMtiW7xlLBGLdD-MjlnviY-Md-FWBa6dKgleLd7RBlbbrEl9SZCSNooOJ4NYbPSBNjQTA_JRjiiJM6-dIggHy2Stx=WtgdYQ_dFXAWCERoxgf9X5mC398KJ478B3k4nDxg3Oe=Nt6XqcUA=BcKL_Eo=lI5bNsC_Tw0eWhHkWuJEl=B79gtSInjjY5Bn3mcxKm4NYEd8i9iGXj=EqneKb1WXEZRunLfYsafkqpFlT7TG-zMH6Xh6En-PRzguWWX1H2c2_OCdQRDrjq5SWFve8YyXfU-T4zK==liprN8LOFDbG256z5Ep43ptaz4-85jq0kiaGwmTiQwWXfvYuIFSMuJMM8wi4fhZcUseP1A-NZFzPf-aPzy9hI5SlaHPguy71GmBq5pa6KLmCfhUtRUrpzr5f_wIzzfpoRj8rH5jn6Ut7pYDcd509WU36oDOZlPzNO_H404dlti6pAgHCZgv_535JStbg_s3WpdYX4F-GYoShb9FI8NDwSpqEWPcGkg1KOh_jM_cvkaxjZvwJpC9QBUJjTJL7-cgKTF-NnTxcuBZ8AhmrgEgT7hs8-WGUPpN8gFX=6tXtnlqtwxst8tXL_6PNWKgT-ODI_vJ-ll8KHsbZWjWOWuxKhj81A3lLrYfMAMM277eZSwIwej701csQCCwBhQDNW9uefw4cSvhagAfCOKpnuDDNA0xm59gAKRgs_j7-lmZUEIHJEYdmephboqXFyy7S-ykPe4OCxKiLQd7f0OcM6MidqC5RJGgGBD0HFh36SFurUKFxxasOyyGao0uW1abRZDOigboFps2x9Ccs8qlO4iJAqXMSrwTHF-b_qu45eQEQjn0n7e1jOwyGYbWp8oELdtR8xeLuZ42knqIFAEwrgJe0YL4F_zrbFAZlfj_LmRqIidS94sC_EUzJs=KZ9sgnKkTUSj9u6Mfmt_TDUiF=sUHpgfNckwnaaRWdPc1FqOhKytvN9aEx=fhv62qDADWOZB_Hr4O_5zcuBpH25uHEuer5-HzCLYergU5d8RTILiH_GIJuj3R_TT4SU-sKKdIZZ-_814Dem-NmEogbdLs2JJ=XNvdnK7NTAPtr3b6SRhHBzQUMZ266GrRH1CxHB16NebAm_t4aAujuYpDLK_FNd6aN2asqkbxzLeP-dr7XAChJgqiFF4EyLdYdwIgtXuqlSIJo=yoiP4rjPShM3MjoRg7J=2vEafFu3PXRpOQSUaxtjJ8Xasw6o2Tcmy1dpslFAPtjKQCE0v8tbn0MulePgissmJq-N0NNHTRDlfNj9uNKME0g-IOpcY5GXf7DBN7bfuWzHn_BhlYgvE3YcyEqFReXU8yuff2qYCikztz7oP1je08l5adEYLQRFHWFx1fNlyBkEhRXcBnxf6=5ARoNe8XIl0_bGGrpWqZknpitfmqTxeTlmklymbKQQvxu-0Pt-ikjpb5hrpCx2RklbSuFv_ZfSluqRubQcB3uaFE7qoL2_5nbWCG3qBW8606rc6JT2Y7=XHahDHtnBiuByYOr1LUZH7xoyO4FDeZxYnrL7Gd=U_e8QtjKbrODN=LHmTiXTyQznLlXUgMRpCJIKJdvZnIsDrQGf_GvZw-FkYHpCj9b43ocyF1eQ5NBU2Lmb7fWtPt5mOvN4iI-9a=f58w42RHOSJx51mQOats-HNjk-RaTMTN8=nORJdeOkpUu3ImzwcFy6cNJFLvRuyI0GIuCOdsaZ-BWKhbxDji_GsSLHrXzPXRc--7BKhZn4vCDyJePYHsnmdXm29hiEJsJKPHY0CEoMkJcGbxSuGMuAjcjFP8fw6yMg=0Bc0JC3LNovgL=HfTU7tMkpfURzmL8NYGIXccjld4x6vbW5ZNnAMHklt0macibgJG9DSb36ArDIBYdhaoOvqDMdlzp_ZxSGY19b54eexPywjioA9siial82AI5Gwldoq7ikZKO3sC3aTN09Aon0sGz23u0QSoTY1zmSI-MXQZ0lHi88pASy1jt=8Xu=RswOfnA9NgXmSNzGD_52_KeHONyaXq_SRzYvqE3pCf7sa-1faS3UPBdXTuitiRAqgtFEd3TnDb-ChkBLwIFtsBq4Fs6UX8QEG1yAFNRx1CLz0nDTp2cNow7pGkA7Ni-l6sLWZEW2HO2_5cvrLEm3HDGc=UH09OOHFXwp4TRtNmYMbJ-F7Xa2RMJ=fBntaRH3TW7tgg8K1=C7mQlOkWi47WkEeUcLK6-eaPaWkIOatA6liN4zv5u90KqiIEK4qpbUcK2FKT3adJiNqFdtr4lK3FCSsfsGde20SudgYLi90sNNKUc-jxCImfoU317llLMtMkfGQf6Hx7a5uiuknIrj4ns1=0aCRCb=4vqGPl2RrkNRWoukSObTY3CWFMsEw_IdIIk0WiRKLz2ArjvYJNUbSorpkoq6B6170pKbwbM3xWQiSHaA7msv7XZsapllud6vZvIBeqN-6SLqkOf4womienZIkvckdtwlFPsH_m3ZsOgWm5RMAf9qXyYqo-3bHj=fcEDsjFqHxu=6cyZ5n5pA7wSrwdUnhK8MDJ1tqIA7860DFYOuLl-vyENMI7-BmHr-i0ziux_Q0sZPs1Gptw7k0L_R2BjZEpZ0oKUrT0ZF-I7_uwE6GvhcPA2C5TH9i-4oOch2EhY66IZ8l53=PB2hsAU2NjPzQL6b8Dn5OB18-wDp=tbYfNAHzGtjAva83RhZ88t2fyhj-QnM9FpxWD8zSIAfD1iMD1-LN1rDX0b5dJeB9TvZh1lmzZRetYKCWlf=LrlzqnIbm=flWzTD5AWhbi0P6TBknC6r0z8it2vXf4UxG7Knd5P=6sex601Snup0CD1x2wiF5dgZJO0AyLDsn4S5bvMD723h1CHswsbT32kNCD85Nl=BLN_grNY1_mlAdeCh8Yx27zN1=75ZBvUTHkElXfCxQfckQaawRHqbK=Z4nH7f9I8yrUMNp1dvsApO5i-l52fva1Qa5Aabpv_fuu0q3z-XsqOc0y7hiMfk0FfjNWMQpq4iLv7iH6doF4LTYP2a3BhEpHHJds2z2NFNNTflnn0RSnsjzeEDA4bmmB-m76UXFL39ase0TUot-Z-l5nrE36MmOrgTqre4Sgd46pDI1cXbOMtkgM=n=qxOD1SGoxPS5L79_kLdqx6N5R9KQu_rwvo8pfh2Zg_L2R_ZgnUQn9WvPA3xjALggxDfP=1HjcDbXHXBqfKRaR3seMaH91zwbpqz-EnASl1BZtceOLNeL=xwr2Fk-cQJ8_p8xGojmIFCJqb3ZZqE6oMrHGRb833ezTzw--Sl8fdQvYrLSvAtSqDD8kURNS13eOOWcAUgS=5LAqH9JttkjPU_Mlegbl18wfdBLaEwf=smEDEALbsrCpppv3GvXoYvytDk=I1Aq03euCTLUB6s_JJqDKm8UZYwyCNoZ=QC1uyXdG-6cYttKynrJ6qKvq2Q_d2=gm9o50JXGih8-zngNLtev97g9vGF_PtULe3xupFB0c8TuwwiQ59CGsIGuasYbBUyWsLwKpocflsyGJSEiH8DbgfMiv58LRMB6vNh73cUgmR5YG7YuGuRLaiUjSNbYTcckGucGkefXe-IHfncsZO9BplCO3lNUwUvm2jxC-3WSZg-7DykdCdNwFX4NcQoFMJR_Bq0JBRqItu66nEzUg7qkEG_U6aBRMj-c=9Uo9T6NqQDL9bSa3mqEdlrgo5ojLivtqjPBDd1A6-MqkMkeeULYCRdv0xA76StPgSyuiCQWsth2Exo92LYI-6uc28UsbO-zZnIuoEJ=WP2zn703_-XaBFmaYxlXhIh5tclx80hDceKxXKSNR5bry70WLPa9uFAEQQhIjkLsJq64K7TNRgoUA29zxOkUrKMoCMA6X60gGDvTxiQJ69khxgtKwCf53zEGRJRZnP=XB_bFtHcuiJc1SWfL=D-q5UaIJgRXkrZQPZrOlAnz-32G1cisGhJLtxGe=Mxt6DFgIPr_X6-oz8k9CJd1baMkr=OvNg9lCT997NQa2XGsAyeGpyfTTM4BBx4D=tsyxqZmPPib7nH0kamby0r7NRawA8xJF1bNbY8jNRFXkbQpo2oNTbN3gswBik_kiZozrj7H0I==QwtyqvxsxIwPelQPSxEF=sRGJ9FQtLJ2g-Kvvf4pKm5efqBeKUNb_RjRzfpgQTQKh2fUaAA4cnecUrJFd03Lwic7lox=Hj6G7QxbsYl3SCDqBEgkwLXrsYDc_e1U_XAHZZym8yEw2XX4K6qmSTzeT5GPM9BM6MHH8wbyKyr07YYwo6=N-PmNg-bYsgli_KnvQK9zblOy59yjduHf81q9s7bfMg8KvilTvcRHiEMB0ZrUZxEvOAuwTj--5l6mSdphxHdCi1PU0BZMHuD-8yehIQ0kKhF2JXOSB_yk4LB9=LGQePIExzopX_XQHke4lQrZdwfwjPGQ-otFEzo7vu9avB40tzIWsli_CUgoXxWTTYdjXqWjlMI621Y86Djms1B1WNc2xbn15dcY_6DkfQGWhj3JoCrPkeEr6JxDYUW9NzkJsKhBmYJ=-EdGmxEQDyw3qcDJgpn1nQqvo6EBgzdMmfwR_vaNgTEgf3Iav6IXd17sDKXepmmC61efrn-4Aspr-8pP8GH-03yYK5aMcrcewqGJpjjRCc",
      "X-DQ7Hy5L1-b": "8rqexp",
      "X-DQ7Hy5L1-c": "AADmcwWQAQAA-pF9fq5dCa6-2L2mY6RflTUxyj0fDWl5zjRrJDYeQAcJYZEN",
      "X-DQ7Hy5L1-d": "ABaAhIDBCKGFgQGAAYIQgISigaIAwBGAzvpizi_33wc2HkAHCWGRDf____-zLbjJAYJVRoY7yOaur2CJwXs6q0I",
      "X-DQ7Hy5L1-f": "A5-WeAWQAQAA2bgeNSI5KL5WJFyVOjmHlTz_IpWbZuwpa2mbKWk8TEygWz0vAdyPEfauclIDwH8AAEB3AAAAAA==",
      "X-DQ7Hy5L1-z": "q"
    }
  ],
  "extra": null
}
```

### 调用示例

#### python

```shell
pip install -U pynocaptcha -i https://pypi.python.org/simple
```

```python
# pip install --upgrade pynocaptcha
from pynocaptcha import crack_shape_v1
# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from utils import USER_TOKEN

import hashlib


def generate_id():
    def e():
        return hex(int(65536 * (1 + random.random())))[2:].zfill(4)
    return e() + e() + "-" + e() + "-" + e() + "-" + e() + "-" + e() + e() + e()


proxy = "127.0.0.1:7890"
        
session, shape_headers, extra = crack_shape_v1(
    user_token=USER_TOKEN,
    href='https://www.starbucks.com.cn/',
    script_url='https://cards.starbucks.com.cn/prod/assets/js/esabxubs5hwen.js?async',
    vmp_regexp=r'"(https:\/\/cards\.starbucks\.com\.cn\/prod\/assets\/js\/esabxubs5hwen.js\?seed=.*?&ixGa8B5N8x--z=q)"',
    proxy=proxy,
)

session.cookies.update({
    "sid": "xxx" # starbucks 账号 token
})

transaction_id = generate_id()

headers = {
    'Host': 'profile.starbucks.com.cn',
    'Connection': 'keep-alive',
    'content-length': '0',
    'x-transaction-id': transaction_id,
    'sec-ch-ua-platform': extra['sec-ch-ua-platform'],
    'ixGa8B5N8x-z': shape_headers['ixGa8B5N8x-z'],
    'sec-ch-ua': extra['sec-ch-ua'],
    'X-API-Version': '2.0',
    'sec-ch-ua-mobile': '?0',
    'appKey': '8c2efe7006da1b98b5cf631e4791f2f5',
    'ixGa8B5N8x-c': shape_headers['ixGa8B5N8x-c'],
    'apikey': 'a120a1b39d554c9c89c7f58738b9fd96',
    'ixGa8B5N8x-d': shape_headers['ixGa8B5N8x-d'],
    'ixGa8B5N8x-b': shape_headers['ixGa8B5N8x-b'],
    'x-source-code': 'WEB',
    'sign': hashlib.sha256(("8c2efe7006da1b98b5cf631e4791f2f5" + transaction_id + "{}fc537c09ef4bddb298039ad83ec4dd6b").encode()).hexdigest(),
    'x-msr-version': '2',
    'ixGa8B5N8x-a': shape_headers['ixGa8B5N8x-a'],
    'User-Agent': extra['user-agent'],
    'ixGa8B5N8x-f': shape_headers['ixGa8B5N8x-f'],
    'ixGa8B5N8x-a0': shape_headers.get("ixGa8B5N8x-a0"),
    'Accept': '*/*',
    'Sec-Fetch-Site': 'same-site',
    'Sec-Fetch-Mode': 'cors',
    'Sec-Fetch-Dest': 'empty',
    'Referer': 'https://www.starbucks.com.cn/',
    'Accept-Language': extra['accept-language'],
    'Cookie': 'sid=' + sid,
    'Content-Type': 'application/x-www-form-urlencoded',
}
if not shape_headers.get("ixGa8B5N8x-a0"):
    del headers['ixGa8B5N8x-a0']

for _ in range(2):
    response = session.post(
        'https://profile.starbucks.com.cn/api/v2/customers/detail', 
        headers=headers,
    )
    print(response.status_code, response.text[:100])
```

```python
# pip install --upgrade pynocaptcha
from pynocaptcha import crack_shape_v1, crack_shape_v2
# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from utils import USER_TOKEN, get_idea_proxy


proxy = "127.0.0.1:7890"

href = 'https://tools.usps.com/go/TrackConfirmAction?tRef=fullpage&tLc=2&text28777=&tLabels=420061149261290252835972884185%2C&tABt=false'

user_agent = 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36'

session, result, extra = crack_shape_v2(user_token=USER_TOKEN, href=href, user_agent=user_agent, proxy=proxy)

if isinstance(result, magneto.Response):
    response = result
else:
    headers = result
    response = session.get(href, headers=headers)

if response.status_code == 302:
    print("失败", response.headers, response.text)

if 'This service is currently unavailable' in response.text:
    print('失败')
else:
    print('成功' if '420061149261290252835972884185' in response.text else '失败')
```

```python
# pip install --upgrade pynocaptcha
from pynocaptcha import crack_shape_v1, crack_shape_v2
# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from utils import USER_TOKEN, get_idea_proxy

user_agent = 'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/136.0.0.0 Safari/537.36'

session, shape_headers, extra = crack_shape_v2(
    user_token=USER_TOKEN,
    href='https://www.starbucks.com/gift', 
    pkey="dq7hy5l1",
    user_agent=user_agent,
    request={
        "url": 'https://www.starbucks.com/apiproxy/v1/gift/card/check-balance',
    },
    fast=random.random() > .7,
    proxy=get_idea_proxy("hk"),
    debug=True
)

headers = {
    'accept': 'application/json',
    'accept-language': extra['accept-language'],
    'content-type': 'application/json',
    'origin': 'https://www.starbucks.com',
    'priority': 'u=1, i',
    'referer': 'https://www.starbucks.com/gift',
    'sec-ch-ua': extra['sec-ch-ua'],
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': extra['sec-ch-ua-platform'],
    'sec-fetch-dest': 'empty',
    'sec-fetch-mode': 'cors',
    'sec-fetch-site': 'same-origin',
    'user-agent': extra["user-agent"],
    **shape_headers,
    'x-requested-with': 'XMLHttpRequest',
}

json_data = {
    'cardNumber': '6312845416203301',
    'pin': '13588441',
    'market': 'US',
}

response = session.post('https://www.starbucks.com/apiproxy/v1/gift/card/check-balance', headers=headers, json=json_data)
print(response.status_code, response.text)
```
