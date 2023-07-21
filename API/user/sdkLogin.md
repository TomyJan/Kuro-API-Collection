# 验证码登录 APP 端

注意, APP 端只能同时有一个登录, 也就是获取下一个 token 后前一个 token 就会失效

且获取的 APP 端的 token 不可用于 Web 端的接口

所以推荐通过抓包来让 APP 和 其他自动化业务使用同一个 token 

## 请求地址

> https://api.kurobbs.com/user/sdkLogin

## 请求方式
POST

## 认证方式

null

## 请求头

| 字段            | 类型 | 内容 | 备注                                 |
| --------------- | ---- | ---- | ------------------------------------ |
| osversion       | str  | -    | Android                              |
| devcode         | str  | -    | 2fba3859fe9bfe9099f2696b8648c2c6     |
| distinct_id     | str  | -    | 765485e7-30ce-4496-9a9c-a2ac1c03c02c |
| countrycode     | str  | -    | CN                                   |
| ip              | str  |      | 10.0.2.233                           |
| model           | str  |      | 2211133C                             |
| source          | str  |      | android                              |
| lang            | str  |      | zh-Hans                              |
| version         | str  |      | 1.0.9                                |
| versioncode     | str  |      | 1090                                 |
| content-type    | str  |      | application/x-www-form-urlencoded    |
| accept-encoding | str  |      | gzip                                 |
| user-agent      | str  |      | okhttp/3.10.0                        |

## 请求体

字符串拼接

| 字段     | 类型 | 内容   | 备注                             |
| -------- | ---- | ------ | -------------------------------- |
| code     | num  | 验证码 | APP 端与 Web 端通用              |
| devCode  | str  | -      | 2fba3859fe9bfe9099f2696b8648c2c6 |
| gameList | unk  | -      | null                             |
| mobile   | num  | 手机号 |                                  |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容       | 备注                                                         |
| ------- | ---- | ---------- | ------------------------------------------------------------ |
| code    | num  | 返回值     | -10000: 参数空了<br />-130: 验证码错误<br />过期也会提示错误<br />200: 成功 |
| msg     | str  | 提示信息   |                                                              |
| success | bool | true/false |                                                              |
| data    | obj  | 详细信息   | 登录成功才有                                                 |

### `data`对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| gender    | num  | (?)          | 3                                                            |
| signature | str  | 签名         | 这个人很懒，还没有签名。                                     |
| headUrl   | str  | 头像图片链接 | https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadTwentyone.png |
| headCode | str | 头像 ID   | 35 |
| userName | str | 昵称      |    |
| userId | str | 账号 ID   | 10065669 |
| isRegister | str | 早期的注册用户 | 非早期注册用户 0 |
| isOfficial | str | (?)   | 我是 0 |
| status | str | (?)   | 我是 0 |
| unRegistering | bool | (?)   | 我是 0 |
| token | str | token |    |
| refreshToken | str | refreshToken | 目前不知道哪个接口用来refresh |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/sdkLogin'
const headers = {
    osversion: 'Android',
    devcode: '2fba3859fe9bfe9099f2696b8648c2c6',
    distinct_id: '765485e7-30ce-4496-9a9c-a2ac1c03c02c',
    countrycode: 'CN',
    ip: '10.0.2.233',
    model: '2211133C',
    source: 'android',
    lang: 'zh-Hans',
    version: '1.0.9',
    versioncode: '1090',
    'content-type': 'application/x-www-form-urlencoded',
    'accept-encoding': 'gzip',
    'user-agent': 'okhttp/3.10.0',
}

const formData = new URLSearchParams()
formData.append('code', 114514)
formData.append('devCode', '2fba3859fe9bfe9099f2696b8648c2c6')
formData.append('gameList', '')
formData.append('mobile', 18888888888)
try {
    const response = await fetch(url, {
        method: 'POST',
        headers: headers,
        body: formData,
    })

    if (!response.ok) {
        throw new Error('fetch error: ' + response.status)
    }

    const rsp = await response.json()

    if (rsp.code === 200) {
        console.info('fetch rsp:', JSON.stringify(rsp));
    } else {
        console.error('fetch error:', JSON.stringify(rsp));
    }
} catch (error) {
    console.error('fetch error:', error);
}
```

### 响应

```json
{
  code: 200,
  data: {
    gender: 3,
    signature: '这个人很懒，还没有签名。',
    headUrl: 'https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadTwentyone.png',
    headCode: '35',
    userName: 'TomyJan',
    userId: '10065669',
    isRegister: 0,
    isOfficial: 0,
    status: 0,
    unRegistering: false,
    token: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    refreshToken: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjY5LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAAAAAAAAAAAAA-AAAAAAAAAAAAAAAAAAAAAAAAA-0'
  }
}
```
