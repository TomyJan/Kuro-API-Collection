# 取库洛币总数

## 请求地址

> https://api.kurobbs.com/encourage/gold/getTotalGold

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段            | 类型 | 内容  | 备注                                             |
| --------------- | ---- | ----- | ------------------------------------------------ |
| osversion       | str  | -     | Android                                          |
| devcode         | str  | -     | 2fba3859fe9bfe9099f2696b8648c2c6                 |
| distinct_id     | str  | -     | 765485e7-30ce-4496-9a9c-a2ac1c03c02c             |
| countrycode     | str  | -     | CN                                               |
| ip              | str  |       | 10.0.2.233                                       |
| model           | str  |       | 2211133C                                         |
| source          | str  |       | android                                          |
| lang            | str  |       | zh-Hans                                          |
| version         | str  |       | 1.0.9                                            |
| versioncode     | str  |       | 1090                                             |
| token           | str  | token |                                                  |
| content-type    | str  |       | application/x-www-form-urlencoded; charset=utf-8 |
| accept-encoding | str  |       | gzip                                             |
| user-agent      | str  |       | okhttp/3.10.0                                    |

## 请求体

空, 对, 它在 POST 空气

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token<br />失效 200: 成功 |
| msg     | str  | 提示信息 | 请求成功                       |
| success | bool | true     | token 有效时才有               |
| data    | obj  | 详细信息 | 成功时才有                     |

### `data` 对象

| 字段    | 类型 | 内容       | 备注 |
| ------- | ---- | ---------- | ---- |
| goldNum | num  | 库洛币总数 |      |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/encourage/gold/getTotalGold'
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
    'content-type': 'application/x-www-form-urlencoded; charset=utf-8',
    'accept-encoding': 'gzip',
    'user-agent': 'okhttp/3.10.0',
}

try {
    const response = await fetch(url, {
        method: 'POST',
        headers: headers,
        body: '',
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
        "goldNum": 410
    },
    "msg": "请求成功",
    "success": true
}
```