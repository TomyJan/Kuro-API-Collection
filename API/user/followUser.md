# 关注用户

更新时间: unrecorded

## 请求地址

> https://api.kurobbs.com/user/followUser

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

| 字段         | 类型 | 内容     | 备注               |
| ------------ | ---- | -------- | ------------------ |
| followUserId | num  | 用户 id  |                    |
| operateType  | num  | 操作类型 | 1 = 关注, 2 = 取关 |

## 响应体

json, 且请求失败返回也一样

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 | 请求成功                       |
| success | bool | true     | token 有效时才有               |
| data    | obj  | 签到结果 | 成功时才有                     |

### `data` 对象

| 字段     | 类型 | 内容                            | 备注 |
| -------- | ---- | ------------------------------- | ---- |
| isFollow | num  | 固定为 1 , 只有操作是关注时才有 |      |
| success  | bool | true                            |      |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/followUser'
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
formData.append('followUserId', 10065669)
formData.append('operateType', 1)
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
        console.info('感谢关注主包捏, 这个 api 的 rsp 是 ', JSON.stringify(rsp))
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
    "isFollow": 1,
    "success": true
  },
  "msg": "请求成功",
  "success": true
}
```

