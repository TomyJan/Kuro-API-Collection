# 发送验证码 APP 端

更新时间: 2024.06.17

## 请求地址

> https://api.kurobbs.com/user/getSmsCode

## 请求方式

POST

## 认证方式

null

## 请求头

| 字段            | 类型 | 内容 | 备注                                     |
| --------------- | ---- | ---- | ---------------------------------------- |
| osVersion       | str  | -    | Android                                  |
| devCode         | str  | -    | 073A9EFAC18FC50616DD15808DAE719DBCB904B7 |
| distinct_id     | str  | -    | 96b1567b-b5e6-422f-a1dd-7cb1e58c5db7     |
| countryCode     | str  | -    | CN                                       |
| ip              | str  |      | 192.168.102.138                          |
| model           | str  |      | 23127PN0CC                               |
| source          | str  | 必须 | android                                  |
| lang            | str  |      | zh-Hans                                  |
| version         | str  |      | 2.2.0                                    |
| versionCode     | str  |      | 2200                                     |
| channelId       | str  |      | 2                                        |
| Content-Type    | str  |      | application/x-www-form-urlencoded        |
| Accept-Encoding | str  |      | gzip                                     |
| User-Agent      | str  |      | okhttp/3.11.0                            |

## 请求体

字符串拼接

| 字段        | 类型 | 内容                       | 备注 |
| ----------- | ---- | -------------------------- | ---- |
| mobile      | num  | 手机号                     |      |
| geeTestData | str  | url 编码的极验数据, 可为空 |      |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容       | 备注                               |
| ------- | ---- | ---------- | ---------------------------------- |
| code    | num  | 返回值     | 200: 成功<br />242: 发送验证码频繁 |
| msg     | str  | 提示信息   | 请求成功                           |
| success | bool | true/false |                                    |
| data    | obj  | 详细信息   | 登录成功才有                       |

### `data`对象

| 字段    | 类型 | 内容         | 备注                                                         |
| ------- | ---- | ------------ | ------------------------------------------------------------ |
| geeTest | bool | 是否需要极验 | 验证码发送失败也会返回成功, 只有这个值为 false 才是验证码发送成功 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/getSmsCode'
const headers = {
    osVersion: 'Android',
    devCode: '073A9EFAC18FC50616DD15808DAE719DBCB904B7',
    distinct_id: '96b1567b-b5e6-422f-a1dd-7cb1e58c5db7',
    countryCode: 'CN',
    ip: '192.168.102.138',
    model: '23127PN0CC',
    source: 'android',
    lang: 'zh-Hans',
    version: '2.2.0',
    versionCode: '2200',
    channelId: '2',
    'content-type': 'application/x-www-form-urlencoded',
    'accept-encoding': 'gzip',
    'user-agent': 'okhttp/3.11.0',
}

const formData = new URLSearchParams()
formData.append('mobile', 18888888888)
formData.append('geeTestData', '%7B%22captcha_id%22%3A%223f7e2d848ce0cb7e7d019d621e556ce2%22%2C%22lot_number%22%3A%222bc78d090fc54c418876148920e8aa5b%22%2C%22pass_token%22%3A%223368e3f33f2fdd0499941f33277f5e470ec9bc2a10e570842ed603b6e71696c7%22%2C%22gen_time%22%3A%221718625086%22%2C%22captcha_output%22%3A%22fh4K-uAVO00jSSOyBqkwKKDf4vxSbT9WahyYVZdQ-uLp6ctUCbbIovpsMDFmEIhowDUHFSBewXv7SSCfrf9OZJVbpknEskQY_sp6OFs9DVO4eNt9jOWmMA4gBNpS2Pp6POwhU-SvxpmumfS2kdXZfuGJfkwkdw47wFAvkngr2ipYiixN4wy6LEy-BZxOF5se0WVKdhlBVuVToR1P4GwF24ndqp3knrHB71xuZVfv4Uf2bzF2rYBRRkznKC6dtybn706OVFzKE9dqU7gOUjsxnTeRRQeWt9AHcZRMEc7g0IzmBW5oedROcsyBnUsVD1TpOjUcwhcvq-xT3n7ayciK-qGpZzN51cqpiAaA3g2fPlee-GS22ZzI_WxHqUEeqEElGqQTi_ewD8smjyF-y3B-KJV2K-anCCxAHI6W3TIZ6iVSjxx-9XtV75AD1gwi4XycRchdgjPocmAPGaLWLb3sd70TLOYGMLh3Ase69y8MAbc%3D%22%7D')
try {
    const response = await fetch(url, {
        method: 'POST',
        headers: headers,
        body: formData,
    })

    if (!response.ok) {
        console.error('fetch error: ', response.status, response.statusText)
    }

    const rsp = await response.json()

    if (rsp.code === 200) {
        console.info('api rsp:', JSON.stringify(rsp))
    } else {
        console.error('api error:', JSON.stringify(rsp))
    }
} catch (error) {
    console.error('fetch error:', error)
}
```

### 响应

```json
{
    "code": 200,
    "data": {
        "geeTest": false
    },
    "msg": "请求成功",
    "success": true
}
```