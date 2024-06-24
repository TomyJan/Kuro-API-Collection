# 社区签到信息

更新时间: 2024.06.24

## 请求地址

> https://api.kurobbs.com/user/signIn/info

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段        | 类型 | 内容         | 备注                                     |
| ----------- | ---- | ------------ | ---------------------------------------- |
| devCode     | str  | 必须但不校验 | 073A9EFAC18FC50616DD15808DAE719DBCB904B7 |
| ip          | str  |              | 192.168.102.138                          |
| source      | str  | 必须         | android                                  |
| version     | str  |              | 2.2.0                                    |
| versionCode | str  |              | 2200                                     |
| token       | str  | token        | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| osVersion       | str  | -            | Android                                  |
| distinct_id     | str  | -            | 96b1567b-b5e6-422f-a1dd-7cb1e58c5db7, UUID 格式 |
| countryCode     | str  | -            | CN                                       |
| model           | str  |              | 23127PN0CC                               |
| lang            | str  |              | zh-Hans                                  |
| channelId       | str  | ? | 2                                        |
| Content-Type    | str  |              | application/x-www-form-urlencoded        |
| Accept-Encoding | str  |              | gzip                                     |
| Cookie | str  |              | user_token=eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| User-Agent      | str  |              | okhttp/3.11.0                            |

## 请求体

字符串拼接

| 字段        | 类型 | 内容                       | 备注               |
| ----------- | ---- | -------------------------- | ------------------ |
| gameId      | num  | 游戏 id                    | 战双 = 2, 鸣潮 = 3 |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容       | 备注         |
| ------- | ---- | ---------- | ------------ |
| code    | num  | 返回值     | 200: 成功    |
| msg     | str  | 提示信息   | 请求成功     |
| success | bool | true/false |              |
| data    | obj  | 详细信息   | 登录成功才有 |

### `data`对象

| 字段         | 类型 | 内容         | 备注 |
| ------------ | ---- | ------------ | ---- |
| continueDays | num  | 连签天数     |      |
| hasSignIn    | bool | 今天是否已签 |      |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/signIn/info'
const headers = {
    'devCode': '073A9EFAC18FC50616DD15808DAE719DBCB904B7',
    'ip': '10.149.57.199',
    'source': 'android',
    'version': '2.2.0',
    'versionCode': '2200',
    'token': 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'osVersion': 'Android',
    'distinct_id': '96b1567b-b5e6-422f-a1dd-7cb1e58c5db7',
    'countryCode': 'CN',
    'model': '23127PN0CC',
    'lang': 'zh-Hans',
    'channelId': '2',
    'Content-Type': 'application/x-www-form-urlencoded',
    'Accept-Encoding': 'gzip',
    'Cookie': 'user_token=eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'User-Agent': 'okhttp/3.11.0',
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
        "continueDays": 32,
        "hasSignIn": false
    },
    "msg": "请求成功",
    "success": true
}
```