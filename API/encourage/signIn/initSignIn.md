# 取游戏签到信息

## 请求地址

> https://api.kurobbs.com/encourage/signIn/initSignIn

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
| origin           | str  |       | https://web-static.kurobbs.com                               |
| x-requested-with | str  |       | com.kurogame.kjq                                             |
| sec-fetch-site   | str  |       | same-site                                                    |
| sec-fetch-mode   | str  |       | cors                                                         |
| sec-fetch-dest   | str  |       | empty                                                        |
| accept-encoding  | str  |       | gzip, deflate, br                                            |
| accept-language  | str  |       | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7                          |

## 请求体

字符串拼接

| 字段     | 类型 | 内容      | 备注                      |
| -------- | ---- | --------- | ------------------------- |
| gameId   | num  | 游戏 id   | 战双 = 2, 鸣潮 = 3        |
| serverId | str  | 服务器 id | 星火服 = 1000, 信标服 = ? |
| roleId   | num  | 游戏 uid  | 46218962                  |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容       | 备注                           |
| ------- | ---- | ---------- | ------------------------------ |
| code    | num  | 返回值     | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息   |                                |
| success | bool | true/false | token 有效时才有               |
| data    | obj  | 详细信息   | 成功才有                       |

### `data`对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| eventEndTimes | str  | 本期活动结束时间 | 2023-07-31 23:59:59                                         |
| eventStartTimes | str  | 本期活动开始时间 | 2023-07-01 00:00:00                  |
| expendGold | num  | (?) | https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadTwentyone.png |
| expendNum | num | (?) | 3 |
| nowServerTimes | str | 当前服务器时间 | 2023-07-16 17:41:43 |
| omissionNnm | num | 漏签天数   | 13 |
| redirectContent | str | (?) | taskCenter |
| redirectText | str | (?)   | 任务中心 |
| redirectType | num | (?)   | 2 |
| repleNum | num | (?)   | 0 |
| sigIn | bool | 今天是否已签到 | true, 注意这个字段单词拼写是错误的 |
| sigInNum | num | 签到天数 | 3, 注意这个字段单词拼写是错误的 |
| signInGoodsConfigs | arr | 签到奖励物品数组 |  |

### `signInGoodsConfigs`成员对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| goodsIcon | str  | 物品图标链接 | https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419327938299.png |
| goodsId | num  | 物品 id | 1                  |
| goodsNum | num  | 物品数量 | 100000 |
| id | num | (?) | 423 |
| serialNum | num | (?) | 从 0 开始递增的 |
| signId | num | (?) | 6 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/encourage/signIn/initSignIn'
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
    "eventEndTimes": "2023-07-31 23:59:59",
    "eventStartTimes": "2023-07-01 00:00:00",
    "expendGold": 200,
    "expendNum": 3,
    "nowServerTimes": "2023-07-16 17:41:43",
    "omissionNnm": 13,
    "redirectContent": "taskCenter",
    "redirectText": "任务中心",
    "redirectType": 2,
    "repleNum": 0,
    "sigIn": true,
    "sigInNum": 3,
    "signInGoodsConfigs": [
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419327938299.png",
        "goodsId": 1,
        "goodsNum": 100000,
        "id": 423,
        "serialNum": 0,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419582796928.png",
        "goodsId": 60001,
        "goodsNum": 10,
        "id": 424,
        "serialNum": 1,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419428211097.png",
        "goodsId": 30013,
        "goodsNum": 5,
        "id": 425,
        "serialNum": 2,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419546830077.png",
        "goodsId": 50005,
        "goodsNum": 50,
        "id": 426,
        "serialNum": 3,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419455634432.png",
        "goodsId": 31104,
        "goodsNum": 5,
        "id": 427,
        "serialNum": 4,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419481262966.png",
        "goodsId": 31204,
        "goodsNum": 5,
        "id": 428,
        "serialNum": 5,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419618811440.png",
        "goodsId": 60002,
        "goodsNum": 5,
        "id": 429,
        "serialNum": 6,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419327938299.png",
        "goodsId": 1,
        "goodsNum": 100000,
        "id": 430,
        "serialNum": 7,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419582796928.png",
        "goodsId": 60001,
        "goodsNum": 10,
        "id": 431,
        "serialNum": 8,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419546830077.png",
        "goodsId": 50005,
        "goodsNum": 50,
        "id": 432,
        "serialNum": 9,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419428211097.png",
        "goodsId": 30013,
        "goodsNum": 5,
        "id": 433,
        "serialNum": 10,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419455634432.png",
        "goodsId": 31104,
        "goodsNum": 5,
        "id": 434,
        "serialNum": 11,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419481262966.png",
        "goodsId": 31204,
        "goodsNum": 5,
        "id": 435,
        "serialNum": 12,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419618811440.png",
        "goodsId": 60002,
        "goodsNum": 5,
        "id": 436,
        "serialNum": 13,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419327938299.png",
        "goodsId": 1,
        "goodsNum": 150000,
        "id": 437,
        "serialNum": 14,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419546830077.png",
        "goodsId": 50005,
        "goodsNum": 50,
        "id": 438,
        "serialNum": 15,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419582796928.png",
        "goodsId": 60001,
        "goodsNum": 15,
        "id": 439,
        "serialNum": 16,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419428211097.png",
        "goodsId": 30013,
        "goodsNum": 8,
        "id": 447,
        "serialNum": 24,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419455634432.png",
        "goodsId": 31104,
        "goodsNum": 8,
        "id": 448,
        "serialNum": 25,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419481262966.png",
        "goodsId": 31204,
        "goodsNum": 8,
        "id": 449,
        "serialNum": 26,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419618811440.png",
        "goodsId": 60002,
        "goodsNum": 8,
        "id": 450,
        "serialNum": 27,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419506725543.png",
        "goodsId": 40200,
        "goodsNum": 5,
        "id": 451,
        "serialNum": 28,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419646391697.png",
        "goodsId": 90030,
        "goodsNum": 3,
        "id": 452,
        "serialNum": 29,
        "signId": 6
      },
      {
        "goodsIcon": "https://prod-alicdn-community.kurobbs.com/signInIcon/1688123419327938299.png",
        "goodsId": 1,
        "goodsNum": 150000,
        "id": 453,
        "serialNum": 30,
        "signId": 6
      }
    ]
  },
  "msg": "请求成功",
  "success": true
}
```
