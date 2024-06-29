# 取游戏签到记录 V2

更新时间: 2024.06.29

## 请求地址

> https://api.kurobbs.com/encourage/signIn/queryRecordV2

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段               | 类型 | 内容  | 备注                                                         |
| ------------------ | ---- | ----- | ------------------------------------------------------------ |
| pragma             | str  | -     | no-cache                                                     |
| cache-control      | str  | -     | no-cache                                                     |
| sec-ch-ua          | str  | -     | "Not/A)Brand";v="8", "Chromium";v="126", "Android WebView";v="126" |
| source             | str  | -     | android                                                      |
| sec-ch-ua-mobile   | str  | -     | ?1                                                           |
| user-agent         | str  | UA    | Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/126.0.6478.26 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0 |
| content-type       | str  | -     | application/x-www-form-urlencoded                            |
| accept             | str  | -     | application/json, text/plain, \*/\*                          |
| devcode            | str  | -     | 61.178.245.28, Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/126.0.6478.26 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0 |
| token              | str  | token | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| sec-ch-ua-platform | str  | -     | "Android"                                                    |
| origin             | str  |       | https://web-static.kurobbs.com                               |
| x-requested-with   | str  |       | com.kurogame.kjq                                             |
| sec-fetch-site     | str  |       | same-site                                                    |
| sec-fetch-mode     | str  |       | cors                                                         |
| sec-fetch-dest     | str  |       | empty                                                        |
| accept-encoding    | str  |       | gzip, deflate, br, zstd                                      |
| accept-language    | str  |       | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7                          |
| priority           | str  |       | u=1, i                                                       |

## 请求体

字符串拼接

| 字段     | 类型 | 内容      | 备注                      |
| -------- | ---- | --------- | ------------------------- |
| gameId   | num  | 游戏 id   | 战双 = 2, 鸣潮 = 3        |
| serverId | str  | 服务器 id | 星火服 = 1000, 信标服 = ? |
| roleId   | num  | 游戏 uid  | 46218962                  |
| userId   | num  | 库洛 id   |                           |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容               | 备注                           |
| ------- | ---- | ------------------ | ------------------------------ |
| code    | num  | 返回值             | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息           |                                |
| success | bool | true/false         | token 有效时才有               |
| data    | arr  | 签到获得的物品数组 | 成功才有                       |

### `data`成员对象

| 字段        | 类型 | 内容         | 备注                                               |
| ----------- | ---- | ------------ | -------------------------------------------------- |
| goodsId     | num  | 物品 id      | 1                                                  |
| goodsName   | str  | 物品名称     | 螺母                                               |
| goodsNum    | num  | 物品数量     | 100000                                             |
| goodsUrl    | str  | 物品图标链接 | https://web-static.kurobbs.com/game/item/2/1.png   |
| id          | num  | (?)          | 26194816                                           |
| sendState   | bool | (?)          | false                                              |
| sendStateV2 | num  | (?)          | 0                                                  |
| sigInDate   | str  | 签到日期     | 战双: 2024-06-02<br />鸣潮: 2024-06-04 00:02:22    |
| type        | num  | 签到类型?    | 0 = 普通签到, 2 = 新手一次性签到活动, 3 = 限时签到 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/encourage/signIn/queryRecordV2'
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
formData.append('serverId', 1000)
formData.append('roleId', 46218962)
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
    "data": [
        {
            "goodsId": "1",
            "goodsName": "螺母",
            "goodsNum": 100000,
            "goodsUrl": "https://web-static.kurobbs.com/game/item/2/1.png",
            "id": "26194816",
            "sendState": false,
            "sendStateV2": 0,
            "sigInDate": "2024-06-02",
            "type": 0
        },
        {
            "goodsId": "29",
            "goodsName": "6星·意识碎片",
            "goodsNum": 50,
            "goodsUrl": "https://web-static.kurobbs.com/game/item/2/29.png",
            "id": "26194817",
            "sendState": false,
            "sendStateV2": 0,
            "sigInDate": "2024-06-02",
            "type": 3
        }
    ],
    "msg": "请求成功",
    "success": true
}
```