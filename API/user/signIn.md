# 社区签到

更新时间: 20240805

## 请求地址

> https://api.kurobbs.com/user/signIn

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段            | 类型 | 必须 | 内容                              | 备注                                 |
| --------------- | ---- | ---- | --------------------------------- | ------------------------------------ |
| osversion       | str  |      | -                                 | Android                              |
| devcode         | str  |      | 2fba3859fe9bfe9099f2696b8648c2c6  | 似乎不要也行？                       |
| distinct_id     | str  |      | -                                 | 765485e7-30ce-4496-9a9c-a2ac1c03c02c |
| countrycode     | str  |      | -                                 | CN                                   |
| ip              | str  |      |                                   | 10.0.2.233                           |
| model           | str  |      |                                   | 2211133C                             |
| source          | str  | true | android                           | 不填可能会code500                    |
| lang            | str  |      |                                   | zh-Hans                              |
| version         | str  |      |                                   | 1.0.9                                |
| versioncode     | str  |      |                                   | 1090                                 |
| token           | str  | true | token                             | 令牌不能为空                         |
| content-type    | str  | true | application/x-www-form-urlencoded | 不填可能会code500                    |
| accept-encoding | str  |      |                                   | gzip                                 |
| user-agent      | str  |      |                                   | okhttp/3.10.0                        |
| host            | str  | true | api.kurobbs.com                   | 不填可能会code400                    |

## 请求体

字符串拼接

| 字段   | 类型 | 内容    | 备注                                             |
| ------ | ---- | ------- | ------------------------------------------------ |
| gameId | num  | 游戏 id | 战双 = 2, 鸣潮 = 3, 这个参数没卵用啊签到算一个的 |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容       | 备注                                                         |
| ------- | ---- | ---------- | ------------------------------------------------------------ |
| code    | num  | 返回值     | 1511: 签到过了<br />220: token 失效<br />200: 成功, 只有成功时才有签到弹窗 |
| msg     | str  | 提示信息   | 请求成功/请勿重复签到                                        |
| success | bool | true/false | 是否签到成功, token 有效时才有<br />注意如果被风控, 将报 cookie 过期, 但是返回值包含 success = false; 暂不明确风控原理 |
| data    | obj  | 签到结果   | 成功时才有                                                   |

### `data` 对象

| 字段         | 类型 | 内容               | 备注 |
| ------------ | ---- | ------------------ | ---- |
| gainVoList   | arr  | 签到获得的物品数组 |      |
| continueDays | num  | 连签天数           | 1    |

### `gainVoList` 成员对象

| 字段      | 类型 | 内容      | 备注                                                       |
| --------- | ---- | --------- | ---------------------------------------------------------- |
| gainTyp   | num  | 奖品类型? | 应该固定为2=库洛币, 改成其他签到成功弹窗就不显示物品信息了 |
| gainValue | num  | 奖品数量  | 30                                                         |

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

Success: 

```json
{
  "status": true,
  "data": {
    "gainVoList": [
      {
        "gainTyp": 2,
        "gainValue": 30
      }
    ],
    "continueDays": 1
  }
}
```

Failed: 

```json
{
    "code": 1511,
    "msg": "请勿重复签到",
    "success": false
}
```

