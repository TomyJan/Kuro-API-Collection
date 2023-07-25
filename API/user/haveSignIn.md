# 是否社区签到

## 请求地址

> https://api.kurobbs.com/user/haveSignIn

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段            | 类型 | 内容  | 备注                                 |
| --------------- | ---- | ----- | ------------------------------------ |
| osversion       | str  | -     | Android                              |
| devcode         | str  | -     | 2fba3859fe9bfe9099f2696b8648c2c6     |
| distinct_id     | str  | -     | 765485e7-30ce-4496-9a9c-a2ac1c03c02c |
| countrycode     | str  | -     | CN                                   |
| ip              | str  |       | 10.0.2.233                           |
| model           | str  |       | 2211133C                             |
| source          | str  |       | android                              |
| lang            | str  |       | zh-Hans                              |
| version         | str  |       | 1.0.9                                |
| versioncode     | str  |       | 1090                                 |
| token           | str  | token |                                      |
| content-type    | str  |       | application/x-www-form-urlencoded    |
| accept-encoding | str  |       | gzip                                 |
| user-agent      | str  |       | okhttp/3.10.0                        |

## 请求体

字符串拼接

| 字段   | 类型 | 内容    | 备注                                             |
| ------ | ---- | ------- | ------------------------------------------------ |
| gameId | num  | 游戏 id | 战双 = 2, 鸣潮 = 3, 这个参数没卵用啊签到算一个的 |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容       | 备注                           |
| ------- | ---- | ---------- | ------------------------------ |
| code    | num  | 返回值     | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息   |                                |
| success | bool | true       | token 有效时才有               |
| data    | bool | 是否已签到 | 成功时才有                     |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/haveSignIn'
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
    token: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'content-type': 'application/x-www-form-urlencoded',
    'accept-encoding': 'gzip',
    'user-agent': 'okhttp/3.10.0',
}

const formData = new URLSearchParams()
formData.append('gameId', 2)
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
  "code": 200,
  "data": false,
  "msg": "请求成功",
  "success": true
}
```