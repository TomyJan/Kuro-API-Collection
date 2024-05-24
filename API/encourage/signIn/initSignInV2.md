# 取游戏签到信息 V2

更新时间: 2024.05.24

## 请求地址

> https://api.kurobbs.com/encourage/signIn/initSignInV2

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
| userId   | num  | 库洛 id   |                           |

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
| isSigIn | bool | 今天是否已签到 | true, 注意这个字段单词拼写是错误的 |
| nowServerTimes | str | 当前服务器时间 | 2023-07-16 17:41:43 |
| omissionNnm | num | 漏签天数   | 13 |
| redirectContent | str | (?) | taskCenter |
| redirectText | str | (?)   | 任务中心 |
| redirectType | num | (?)   | 2 |
| repleNum | num | (?)   | 0 |
| sigInNum | num | 签到天数 | 3, 注意这个字段单词拼写是错误的 |
| signInGoodsConfigs | arr | 签到奖励物品数组 |  |

### `signInGoodsConfigs`成员对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| goodsId | num  | 物品 id | 1                  |
| goodsName | str | 物品名称 | 螺母 |
| goodsNum | num  | 物品数量 | 100000 |
| goodsUrl | str | 物品图标链接 | https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png |
| id | num | (?) | 790 |
| isGain | bool | (?) | false |
| serialNum | num | (?) | 从 0 开始递增的 |
| signId | num | (?) | 6 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/encourage/signIn/initSignInV2'
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
  "data": {
    "disposableGoodsList": [],
    "disposableSignNum": 0,
    "eventEndTimes": "2024-05-31 23:59:59",
    "eventStartTimes": "2024-05-01 00:00:00",
    "expendGold": 200,
    "expendNum": 3,
    "isSigIn": false,
    "nowServerTimes": "2024-05-24 18:01:23",
    "omissionNnm": 21,
    "openNotifica": false,
    "redirectContent": "taskCenter",
    "redirectText": "任务中心",
    "redirectType": 2,
    "repleNum": 0,
    "sigInNum": 2,
    "signInGoodsConfigs": [
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 100000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png",
        "id": 790,
        "isGain": false,
        "serialNum": 0,
        "signId": 16
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 10,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ebabbf0b776542d98121e9dd3342ff9f20240518.png",
        "id": 791,
        "isGain": false,
        "serialNum": 1,
        "signId": 16
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c9db6799fc3541d6af94cc7b1b8ff1e420240518.png",
        "id": 792,
        "isGain": false,
        "serialNum": 2,
        "signId": 16
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/f8f88a0b81ab4987b4d721762f08aa7e20240518.png",
        "id": 793,
        "isGain": false,
        "serialNum": 3,
        "signId": 16
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/571e9544a48f441991cd244ce800587720240518.png",
        "id": 794,
        "isGain": false,
        "serialNum": 4,
        "signId": 16
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/15176ef650f8493ea04badddace5ebd420240518.png",
        "id": 795,
        "isGain": false,
        "serialNum": 5,
        "signId": 16
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/03f4c373f9c34afb9c60e06515bc4aa620240518.png",
        "id": 796,
        "isGain": false,
        "serialNum": 6,
        "signId": 16
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 100000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png",
        "id": 797,
        "isGain": false,
        "serialNum": 7,
        "signId": 16
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 10,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ebabbf0b776542d98121e9dd3342ff9f20240518.png",
        "id": 798,
        "isGain": false,
        "serialNum": 8,
        "signId": 16
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/f8f88a0b81ab4987b4d721762f08aa7e20240518.png",
        "id": 799,
        "isGain": false,
        "serialNum": 9,
        "signId": 16
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c9db6799fc3541d6af94cc7b1b8ff1e420240518.png",
        "id": 800,
        "isGain": false,
        "serialNum": 10,
        "signId": 16
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/571e9544a48f441991cd244ce800587720240518.png",
        "id": 801,
        "isGain": false,
        "serialNum": 11,
        "signId": 16
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/15176ef650f8493ea04badddace5ebd420240518.png",
        "id": 802,
        "isGain": false,
        "serialNum": 12,
        "signId": 16
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/03f4c373f9c34afb9c60e06515bc4aa620240518.png",
        "id": 803,
        "isGain": false,
        "serialNum": 13,
        "signId": 16
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 150000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png",
        "id": 804,
        "isGain": false,
        "serialNum": 14,
        "signId": 16
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/f8f88a0b81ab4987b4d721762f08aa7e20240518.png",
        "id": 805,
        "isGain": false,
        "serialNum": 15,
        "signId": 16
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 15,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ebabbf0b776542d98121e9dd3342ff9f20240518.png",
        "id": 806,
        "isGain": false,
        "serialNum": 16,
        "signId": 16
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c9db6799fc3541d6af94cc7b1b8ff1e420240518.png",
        "id": 807,
        "isGain": false,
        "serialNum": 17,
        "signId": 16
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/571e9544a48f441991cd244ce800587720240518.png",
        "id": 808,
        "isGain": false,
        "serialNum": 18,
        "signId": 16
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/15176ef650f8493ea04badddace5ebd420240518.png",
        "id": 809,
        "isGain": false,
        "serialNum": 19,
        "signId": 16
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/03f4c373f9c34afb9c60e06515bc4aa620240518.png",
        "id": 810,
        "isGain": false,
        "serialNum": 20,
        "signId": 16
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/f8f88a0b81ab4987b4d721762f08aa7e20240518.png",
        "id": 811,
        "isGain": false,
        "serialNum": 21,
        "signId": 16
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 150000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png",
        "id": 812,
        "isGain": false,
        "serialNum": 22,
        "signId": 16
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 15,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ebabbf0b776542d98121e9dd3342ff9f20240518.png",
        "id": 813,
        "isGain": false,
        "serialNum": 23,
        "signId": 16
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c9db6799fc3541d6af94cc7b1b8ff1e420240518.png",
        "id": 814,
        "isGain": false,
        "serialNum": 24,
        "signId": 16
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/571e9544a48f441991cd244ce800587720240518.png",
        "id": 815,
        "isGain": false,
        "serialNum": 25,
        "signId": 16
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/15176ef650f8493ea04badddace5ebd420240518.png",
        "id": 816,
        "isGain": false,
        "serialNum": 26,
        "signId": 16
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/03f4c373f9c34afb9c60e06515bc4aa620240518.png",
        "id": 817,
        "isGain": false,
        "serialNum": 27,
        "signId": 16
      },
      {
        "goodsId": 40200,
        "goodsName": "支援突破套组·小",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/255e67bda0ca446dabd4958a42726d7d20240518.png",
        "id": 818,
        "isGain": false,
        "serialNum": 28,
        "signId": 16
      },
      {
        "goodsId": 90030,
        "goodsName": "中型血清组β",
        "goodsNum": 3,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/9b087b6ad62c46f69f10263d96cee83520240518.png",
        "id": 819,
        "isGain": false,
        "serialNum": 29,
        "signId": 16
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 150000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png",
        "id": 820,
        "isGain": false,
        "serialNum": 30,
        "signId": 16
      }
    ],
    "signLoopGoodsList": []
  },
  "msg": "请求成功",
  "success": true
}
```
