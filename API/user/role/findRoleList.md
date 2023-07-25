# 取绑定游戏账号列表

## 请求地址

> https://api.kurobbs.com/user/role/findRoleList

## 请求方式
POST

## 认证方式

token

## 请求头

| 字段            | 类型 | 内容  | 备注                                             |
| --------------- | ---- | ----- | ------------------------------------------------ |
| osversion       | str  | -     | Android                                          |
| devcode         | str  | -     | 2fba3859fe9bfe9099f2696b8648c2c6                 |
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

字符串拼接

| 字段   | 类型 | 内容    | 备注               |
| ------ | ---- | ------- | ------------------ |
| gameId | num  | 游戏 id | 战双 = 2, 鸣潮 = 3 |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 |                                |
| success | bool | true     | token 有效时才有               |
| data    | arr  | 详细信息 | 成功时才有                     |

### `data`成员对象


| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| bindStatus | num  | 绑定状态     | 1 |
| createTime | num | 绑定时间戳 | 1688285969000 |
| gameId | num | 游戏 id | 战双 = 2, 鸣潮 = 3 |
| isDefault | bool | 是否默认展示账号 |  |
| isHidden | bool | (?)  | false |
| roleId | str | 游戏账号 id | 46218962 |
| roleName | str | 游戏账号昵称 | TomyJan |
| serverId | str | 服务器 id | 星火服 = 1000, 信标服 = ? |
| serverName | str | 服务器名称 | 星火服 |
| userId | str | 账号 id | 10065669 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/role/findRoleList'
const headers = {
    osversion: 'Android',
    devcode: '2fba3859fe9bfe9099f2696b8648c2c6',
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
  "data": [
    {
      "bindStatus": 1,
      "createTime": 1689578678000,
      "gameId": 2,
      "isDefault": false,
      "isHidden": false,
      "roleId": "23547501",
      "roleName": "指挥官06348",
      "serverId": "1000",
      "serverName": "星火服",
      "userId": "10065669"
    },
    {
      "bindStatus": 1,
      "createTime": 1688285969000,
      "gameId": 2,
      "isDefault": true,
      "isHidden": false,
      "roleId": "46218962",
      "roleName": "TomyJan",
      "serverId": "1000",
      "serverName": "星火服",
      "userId": "10065669"
    }
  ],
  "msg": "请求成功",
  "success": true
}
```
