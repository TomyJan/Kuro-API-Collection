# 取活动奖券数量

## 请求地址

> https://api.kurobbs.com/activity/lottery/getRemain

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段             | 类型 | 内容  | 备注                                                         |
| ---------------- | ---- | ----- | ------------------------------------------------------------ |
| pragma           | str  | -     | no-cache                                                     |
| cache-control    | str  | -     | no-cache                                                     |
| accept           | str  | -     | application/json, text/plain, \*/\*                          |
| source           | str  | -     | android                                                      |
| user-agent       | str  | UA    | Mozilla/5.0 (Linux; Android 13; 2211133C Build/TKQ1.220905.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/114.0.5735.131 Mobile Safari/537.36 Kuro/1.0.9 KuroGameBox/1.0.9 |
| token            | str  | token | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| content-type     | str  |       | application/x-www-form-urlencoded                            |
| origin           | str  |       | https://web-static.kurobbs.com                               |
| x-requested-with | str  |       | com.kurogame.kjq                                             |
| sec-fetch-site   | str  |       | same-site                                                    |
| sec-fetch-mode   | str  |       | cors                                                         |
| sec-fetch-dest   | str  |       | empty                                                        |
| accept-encoding  | str  |       | gzip, deflate, br                                            |
| accept-language  | str  |       | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7                          |

## 请求体

空

## 响应体

json

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: cookie过期<br />200: 成功 |
| message | str  | 提示信息 | success, 貌似和 msg 一样       |
| msg     | str  | 提示信息 | success                        |
| data    | obj  | true     | 失败时为 null                  |

### `data` 对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| remainCount    | num  | 奖券数量 |  |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/activity/lottery/getRemain'
const headers = {
    pragma: 'no-cache',
    'cache-control': 'no-cache',
    accept: 'application/json, text/plain, */*',
    source: 'android',
    'user-agent': 'Mozilla/5.0 (Linux; Android 13; 2211133C Build/TKQ1.220905.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/114.0.5735.131 Mobile Safari/537.36 Kuro/1.0.9 KuroGameBox/1.0.9',
    token: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'content-type': 'application/x-www-form-urlencoded',
    origin: 'https://web-static.kurobbs.com',
    'x-requested-with': 'com.kurogame.kjq',
    'sec-fetch-site': 'same-site',
    'sec-fetch-mode': 'cors',
    'sec-fetch-dest': 'empty',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7',
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
  "message": "success",
  "msg": "success",
  "data": {
    "remainCount": 0
  }
}
```