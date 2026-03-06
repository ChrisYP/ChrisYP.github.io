------
[`返回首页`](../README.md)    [`上一页`](funcaptcha.md)	[`English Version`](../en-US/castle.md)

## Castle

### Request URL（POST）:

| 版本               | 接口地址                                                    |
|------------------|---------------------------------------------------------|
| `castle（universal）` | `http://api.nocaptcha.io/api/wanda/castle/universal` |

### Request Headers:

| 参数名            | 说明                 | 必须  |
|----------------|--------------------|-----|
| `User-Token`   | `用户密钥, 主页获取`       | `是` |
| `Content-Type` | `application/json` | `是` |
| `Developer-Id` | `开发者 ID, 开发者用户使用, 用户主页邀请链接的字符串(如 xxx/register?c=abcdef, 则 abcdef 为开发者 ID)`           | `否` |

### POST Data（JSON）:

| 参数名          | 类型        | 说明                                                                                                                                                             | 必须  |
|--------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----|
| `href`       | `String`  | `触发 castle 验证的页面地址`                                                                                                                          | `是` |
| `country`    | `String`  | `业务流程使用的代理所属地区国家 code, 如美国（us）、英国（uk）, 详情可咨询管理`    | `否` |
| `user_agent` | `String`  | `自定义 user_agent, 仅支持 chrome/edge, 且版本号 > 115, 如 Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36`       | `否` |
| `proxy` | `String`  | `代理（user:pass@ip:port）, 仅支持 http, 不支持 socks5`       | `否` |

#### json 示例

```
{
    'href': 'https://signin.rockstargames.com/signin/user-form?cid=rsg&returnUrl=%2F',
    'country': 'us'
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
| `data.cookies`   | `Object`  | `验证通过返回的 cookie, 需配合 token 一起使用`    |
| `cost`         | `String`  | `验证耗时（毫秒）`                    |

```
{
    "status": 1,
    "success": true,
    "msg": "验证成功",
    "en_msg": "Verify success",
    "id": "96473722-4e6c-4505-a961-cf5ee3f06f0b",
    "cost": "5118.06ms",
    "data": {
        "token": "xcjFYVfdWiLy6rBJ96WX9Q1UnuDWEjwy6-TyjgxFLD0Jqzxd4MAeham026SW4yA3dQ35P9MKpgTVOYhhxhhJ7zPVw200QXnZxWubAwZdBSSr1Qw3m1JfovBWDtLlxzM_74YIbH-EoCsk_x_oeTguTXPa2yg-HSoXrr_HTfeqjRkG-eV-qPF4d1bmWKq9OcFT2Ak2jY9yeRf4KE-mCcVDldisLSsByai_HsImqBzYplXOEXQ5LluMbL2Dgctg3qSNOCDVKVOA-0pWwEFtYk4W3YQvmrGL5xvxGNj8Kht4yNjnAchGdDs5K3PH8-fa6S7565FbAdzMHbZZq2iVRYh6rPtcVoli8DDMs1SU7XpxihE6ZyX_1bSv03a2yYKfXsHB9Mq_pjvihK91B2ZDy6RlalFuwtw9HQdSXBJMbA_mClguUaOwOM8z7YJ7PxYsG-gBAWC9FACHd3niu-UIQZ9eICNSlYU0dhEHXp3wFNOjFa_C8mhvErF92oyViKWgFhBG6cjgrXDofE3ChDHoyyDRszQljj47N5q8OON4njDlc65WwxvT4UHS27Gl4_4sVM91SvyvnjZI3K9AvqV-JM0hnd-QgUeul6stDY6XcptC5YOtZlGyIYfEfXYd57Q_O4__goOKpfj4874sCpH-VlsjxPY9W1a_ayzSO7HIRLwMv5pmFLOtGBAxRNtgQ3HCPgATHWCB-hnPe2tlViJFoDR2JVLLnrLGiuuYi493uZzNJq2WotlLajYSnbk-XB0hPwn8vH9_NMca0uz1rYxxB32-7VrBe_AEJpg7CyVc90CADxs1B_uccoR7ibBbsTnkyAJ3bCZihNZedChBtcnmf4PR50UMt6ApipZTZPLLYBEz9ZPMarZLbsJ4WDC0ZsKWCACos9Gnf9sHg0Q8YnmF1mwbmFJg3KRULe8wXthtiZ8BB-RUR6vFBc32BEhUx9MFRWyTre7k3NKqyUJ2lmCFXCxGkWuytvKJ14yYlMK-G2Bo5vKf6ifwV0vmjX0BbsOLcAnF3w29-2JQt1xJBER5tbDFowjGDSh1HP_0ChW6_O1oKccuFLkvYgfS6ib9kTJ6sS1uydD4yjcpWvySpz2XqY1TsPY0iwjhumJ6JTVpubfBPFoSYLcoCbdloaRnIVzFd3JYkQXsnvEA54cmPM9O-p9xUCTC4fpLCEbLFk5Fxb93EeLt77gGTbs6VnKWyl-fAKlMqVZ9Z4fFfQaOKsb5GRjlD_N8hF-6ZFPdj6ajWFxzinCYtSYeAKXTvoREwNjohnfVZojq7LcHdepUgjxHK1osb_gXGOkCYFjz05xYwQUBN8FCm2LNoe3kPtMYazSt-xV1bPH8s1j0sLLvyqL3Se9AJeP-3pJlYP9F1uO4nZFfXABtRC_2XSjBvIT7MvoPpb9yOBYlHxR406wVtCMxEoS7x7PS5KgBiZmnwLzuTwgz2PgB0_-3an1yU0z8Jscpf68XqQdKjJqFX5QNhQG2EsZMP-SLp3n8deT0Ghgpkdb8Lr4JufRkeFDEKwwNZ28Jl4f6uGp1VXIUTJHQqfAm2Khce0SqCGIY1uEZRG13hzAAYCa57dQn0ujkqahdpwMHR3JTqdvgO660VJxPgM_lYf4k5untylXj51NPSMBBeg8_Rw1Q6BpREg2BC5MlhrFq8ydgrz2sB3infgh7CqkhXrz64C0-hcGtmUve6nBnvpImjIBsjTl-E2UxOB8SY31IdcgyrqXEUoWHXGKS3Io50AsHiRvyiuwVp6W98vw1VC-0r3muBBDkJERR7TvpdJ9EXKwXU7JDftZIBkq8kGVi_3tbMWQau31z3bbmibQzwfM-Ni7J1qUcI2Vvg6FGuXVQF6BTZtTdlKNOuFoDOzPboi1N42Zj9_NIEGE-PwhvFhUp05B1kn64TUbNwgWXxzyOBUiesGlBPqV6nRd7wmizehWBir5KkmnytfaZ_jP4SWo1qXeFOmzASx_y4HYNxFF6UPWO-xoBBl1SxrDARWf7wWCTkrCyIQ9-7HP9kjkrYKWcwPj4LB_wFha4LqbV12o-r_hHYutk7QE2IiF5C1hmXP2vItTHOhXo4tDsOP2CPqomz0I0egx1C7RI9V89mw4e1CV9nsdjdbI9OeFg2mkEHqFMflaVXy-lxkzJIj6WiDKh5UZGnp7L9clc76d7OS8m2mvl-gCOmKro4yiuM0hlH_9I_efFtEogJWuXA9ySc6u1hqtmTwMYJ3T9ID7ijd3WRdtJs4AgJjg2lKvJflEhnf3R-Q",
        "cookies": {
            "__cuid": "85c1fb1585ce4fd093b13097fffa2524"
        }
    },
    "extra": {
        "user-agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/145.0.0.0 Safari/537.36",
        "sec-ch-ua-platform": "\"Windows\"",
        "sec-ch-ua": "\"Not_A Brand\";v=\"8\", \"Opera\";v=\"120\", \"Chromium\";v=\"145\"",
        "accept-language": "zh-CN,zh;q=0.9,en;q=0.8",
        "sec-ch-ua-arch": "\"x86\"",
        "sec-ch-ua-bitness": "\"64\"",
        "sec-ch-ua-full-version": "\"120.0.6099.216\"",
        "sec-ch-ua-full-version-list": "\"Not_A Brand\";v=\"8.0.0.0\", \"Opera\";v=\"120.0.6099.216\", \"Chromium\";v=\"145.0.7632.68\"",
        "sec-ch-ua-mobile": "?0",
        "sec-ch-ua-model": "\"\"",
        "sec-ch-ua-platform-version": "\"19.0.0\""
    }
}
```

### CURL command:

```
curl \
    -H "User-Agent: python-requests/2.28.2" -H "Accept: */*" \
    -H "User-Token: xxx" \
    -H "Content-Type: application/json" \
    --data-binary "{\"href\":\"https://signin.rockstargames.com/signin/user-form?cid=rsg&returnUrl=%2F",\"country":\"us\"}\" \
    --compressed "http://api.nocaptcha.io/api/wanda/castle/universal"
```

### 调用示例

#### python

```python

# 访问 www.nocaptcha.io 官网获取 User-Token
# get the User-Token from www.nocaptcha.io
from curl_cffi import requests
from utils import USER_TOKEN, get_ipsmart_proxy

country = 'us'
# proxy format: user:pass@ip:port
proxy = get_ipsmart_proxy(country)
session = requests.Session()
session.proxies.update({
    'all': 'http://' + proxy
})

resp = requests.post('http://api.nocaptcha.cn/api/wanda/castle/universal', headers={
    'user-token': USER_TOKEN
}, json={
    'href': 'https://signin.rockstargames.com/signin/user-form?cid=rsg&returnUrl=%2F',
    'proxy': proxy,
    'country': country
}).json()

print(resp)

castle_token = resp['data']['token']
cookies = resp['data']['cookies']

extra = resp['extra']

cookies = {
    'session-id': '49c94630-196d-4682-8703-12a33b0a3a86',
    'rockstarweb_lang.prod': 'en-US',
    'Culture': 'en-US',
}

headers = {
    'Accept': '*/*',
    'Accept-Language': extra['accept-language'],
    'Connection': 'keep-alive',
    'Origin': 'https://signin.rockstargames.com',
    'Referer': 'https://signin.rockstargames.com/signin/user-form?cid=rsg&returnUrl=%2F',
    'Sec-Fetch-Dest': 'empty',
    'Sec-Fetch-Mode': 'cors',
    'Sec-Fetch-Site': 'same-origin',
    'User-Agent': extra['user-agent'],
    'content-type': 'application/json',
    'rockstar-clientid': 'rsg',
    'sec-ch-ua': extra['sec-ch-ua'],
    'sec-ch-ua-mobile': '?0',
    'sec-ch-ua-platform': extra['sec-ch-ua-platform'],
    'x-captchatoken-recaptchaenterprise': '0cAFcWeA65ZmfSngrART3PQzlJbFMmWkbCJtfYSkxhvwvwCtd8X3C-mB7KyCBJ3GutdnZRgdxpLgQFiaxRASpq6UFKofTl3XpDTlwFlP_fNB-hGAxsUP8a2iQabbcmUy25RTPOkIl08RoMV7UioJdkvlM8wmbgBHcPKjiD1zNkTQCF5pM83RdKLGHEuaw8_U6jdSnfsa4CvJW5OxQorDHD08LGPl2TUcj1a7ir61tj-vsmDkF1P92VbcfZ6AaE2K4GaHcyOxNiY7EoWN82Z6VG9buZRdjpMuEKAFocEw6y409f5dUYJGZuhIj2GE5T0AstcLLVEw2WN0__yBMReOQ8FC3BuduR4pI2e_SDVczqXCZHzu_9v9lMhQbp6Cv__-5hzojX0uXOjt_MqX4oafMhtzrXo7d6TrpyrORbbapX1KvqjmJmlwGHFQ2STmn_XVOT9xw6MYSzOSplDSgzz37eFaEIhnYAcPU-1Kv9IJk6geSa-PhMDc0YgSFa4Thcok2IA3hS3oOdsQjbEivjUxGWuVIjC3XdUUDSo3X4OhQKJJ1VkuzWeF3Lza_KKRdD-gEXbO9plkgQVLgU3eMDPO5A8F5bpPf3avucyHuQKXFdgXkWNt91jVjV4bNKupPYP3nXg-9Z9LIT-KdXrg9U-Js3Bs7SIz7H0JnzGiyqIHv-MynVUPXS9fF6hfQsHPzmfUDhzGvVhqGUGN9hgwGcG_6_qj3Z5IOMZ9eCtvCm62VIssO3oDU0YmnzhRN2VTqjg25n1vfChgLePI-WvB1vy2ynmp_0md8mLumZUnsJIc8RwrMW0184vLbq35k1gcV6tVWToREIoa6gMqi5MVfLpMMMqVbyP_iGncdQAREHeBcKx-Vtg5elnoHqt1fkEgdjGdZrUD47dcEOOHxfjTGvill4d6Tp__4Fl5F6wg2_8bxM2x2ssIB9sClVO_UCoTPDO2kcmxum5kGkQZO-okMmAV8ehi9ZZzP6hZsATEjVZEjC_83eGhdTDmsBzN3JeC_B6KG-uVUDzkqT93zM1-04OxiZr_GYAPZ2S1OCr3Kj_B8Cu1GLalyNdE5bfc2Y_qT7ywpAnb3Vs6nItfbE8S_gXJPXguq9znTJT6bn83a2JBvjFiDyxRyHbxv8rcjGGrJSHYt0sxdD1IdmR6B9roh8o_-tTIpgWCOzAMsTh5gkHWCLTa8eduU2pZ3nbUvEYn7x0qGC8tZDM5w5ukSGDiU1Z1CCx5cz951ByKUsK8D0Zg-FW8gteiaU6j1IH0vTHgKPU__nRvPzkycsu_MKphxNukJi7B2sR7Dwfvwep2Gn_A_zJXFbwL0inrddhT8G4qajNScSt8gVwFAoTuYTLPjnSBP5XFpfnk0Lsu7AQtAeVQaAcyVlroeWrPTrzX0byxYcGELLOXT6inahGdDnU113HiJxN1MnRfbkJm4QebXfAR2K4IYMpwtT2TVKhtCsDuICIxgvgMONgWN4LCpU2JYpn0DJN0D4mBckcxOYxfiCEH5s3KQE-DyLsS-Dy55ZMu2vbfHCksMn1HE8EIN91S3OoBaJnNgfiI2U33CYG8TKOSSAKmJlL_TrDdWQowg7wMjMmP-YlEVOKLjEu4uFkovIFxkdcQCuTpriZbzdUiljf1MOJaGcTUBFL8vjMOKmZoxKBwljyaSSGtLLaiCTvM7AM1b1xQBkDUMj9xQgSx0qYCxpwvxeq0MTqNWe_cRnsgZNFZLaO0oSwFziTXBZq5VhnE9NgDdfcF-sCI50f81w4DgWJbtxYGJ2nq-d6q_wi7a4cB8lrnc6wyBend-ezlsTvyy_qZY6xBnsvc17wNQKHGzf799wpb_exIKAKo3JisJTM9qM3CQaXqESFHxY9pKGqlLphRJ8JxfZVZ4pky9k5wVh8mwNPRjxvgFzW1qxuPvUQbRLh_HYytd46pnEOB5Joy5a0pzRcqPabOhoddGnLfEa0uNI-S28Dr4-KBO1yg_N7Kmzhs7XcrmoCJN4xv4vmWJH-gDbxLg950ql4fMSyjVxFerw_yPw0JGjXKFzvsw7YcgLNoFbGMN-M7BM1DEfin73Y8bLZ-L3lc12XGHt4khYWeAFTDYiuBBeyEMCTb_KG2Ba2Fqc_Z7cbwtmAp1e6MbumBmoJwJVmQvrajGcglNdGzLviwvXHIf1amjEdZg1ariQKVIWLQzM2UOF8yVPj1F5IYJqH3RjGsoDgPCoXllBDqZkkAuykfRP9aZimvEIjCeQPueoShpQj7n_Z6ApOnieYzlgK7_Z17Qk_25G8eIKyN9Rdp_UxYz3d025djaTAw9s5V3WGdHLMfBHTWhNOKuQua7aMZ1nNeVO5WTdTsXHOXcj27Y1d4dcsUC7BXUV6DKjOeUgBzKiXpiTjlbaUfmolroAF2SIYyB_lx3KyZZdxL6jS79tDpRwcXJTSh7LwjMZqlPpG_X89ll6ayqYBZAxPzRbO0ptcgIMtQ',
    'x-castle-request-token': castle_token,
    'x-lang': 'en-US',
    'x-requested-with': 'XMLHttpRequest',
}

json_data = {
    'email': 'dsjgvbgv@gmail.com',
    'password': 'jhbdshvf213vvc',
    'keepMeSignedIn': False,
    'deviceName': 'Chrome on Mac',
    'returnUrl': '/',
    'linkInfo': {
        'shouldLink': False,
        'service': None,
        'username': None,
        'serviceVisibility': None,
    },
    'events': [
        {
            'eventName': 'Sign In Form',
            'eventType': 'page-view',
        },
    ],
}

response = session.post('https://signin.rockstargames.com/api/login/rsg', cookies=cookies, headers=headers, json=json_data)
print(response.status_code, response.text)

```
