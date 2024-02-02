# 活动绑定游戏角色

更新时间: unrecorded

## 请求地址

> https://api.kurobbs.com/activity/gamer/role/bindRole

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

字符串拼接

| 字段     | 类型 | 内容        | 备注          |
| -------- | ---- | ----------- | ------------- |
| gameId   | num  | 游戏 id     | 2 = 战双…     |
| roleId   | num  | 游戏账号 id | 46218962      |
| serverId | num  | 服务器 id   | 1000 = 星火服 |
| userId   | num  | 库洛账号 id | 10065669      |

## 响应体

json

| 字段    | 类型 | 内容     | 备注                                               |
| ------- | ---- | -------- | -------------------------------------------------- |
| code    | num  | 返回值   | 1903: 绑定过了<br />220: cookie过期<br />200: 成功 |
| message | str  | 提示信息 | 绑定成功, 貌似和 msg 一样                          |
| msg     | str  | 提示信息 | 绑定成功/角色绑定失败, 用户已存在绑定角色          |
| data    | obj  | 详细信息 | 失败时为 null                                      |

### `data` 对象

| 字段       | 类型 | 内容                          | 备注                       |
| ---------- | ---- | ----------------------------- | -------------------------- |
| id         | null | null                          |                            |
| userId     | num  | 库洛账号 id                   | 10065669                   |
| gameId     | num  | 游戏 id                       | 2                          |
| serverId   | num  | 服务器 id                     | 1000                       |
| roleId     | num  | 游戏帐号 id                   | 46218962                   |
| activityId | num  | 活动 id? 然鹅并没有哪里会用到 | 237108                     |
| createTime | str  | (?)                           | 2023-07-30T09:08:32.26747  |
| updateTime | str  | (?)                           | 2023-07-30T09:08:32.267471 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/activity/gamer/role/bindRole'
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

const formData = new URLSearchParams()
formData.append('gameId', 2)
formData.append('roleId', 46218962)
formData.append('serverId', 1000)
formData.append('userId', 10065669)
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
  "message": "绑定成功",
  "msg": "绑定成功",
  "data": {
    "id": null,
    "userId": 10241734,
    "gameId": 2,
    "serverId": 1000,
    "roleId": 43884358,
    "activityId": 237108,
    "createTime": "2023-07-30T09:08:32.26747",
    "updateTime": "2023-07-30T09:08:32.267471"
  }
}
```