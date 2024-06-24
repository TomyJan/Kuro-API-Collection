# 取游戏签到信息 V2

更新时间: 2024.06.24

## 请求地址

> https://api.kurobbs.com/encourage/signIn/initSignInV2

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段               | 类型 | 内容  | 备注                                                         |
| ------------------ | ---- | ----- | ------------------------------------------------------------ |
| pragma             | str  | -     | no-cache                                                     |
| cache-control      | str  | -     | no-cache                                                     |
| sec-ch-ua          | str  | -     | "Not)A;Brand";v="99", "Android WebView";v="127", "Chromium";v="127" |
| source             | str  | -     | android                                                      |
| sec-ch-ua-mobile   | str  | -     | ?1                                                           |
| user-agent         | str  | UA    | Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.15 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0 |
| content-type       | str  | -     | application/x-www-form-urlencoded                            |
| accept             | str  | -     | `application/json, text/plain, */*`                          |
| devcode            | str  | -     | 61.178.245.214, Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.15 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0 |
| token              | str  | token | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| sec-ch-ua-platform | str  | -     | "Android"                                                    |
| origin             | str  |       | https://web-static.kurobbs.com                               |
| sec-fetch-site     | str  |       | same-site                                                    |
| sec-fetch-mode     | str  |       | cors                                                         |
| sec-fetch-dest     | str  |       | empty                                                        |
| accept-encoding    | str  |       | gzip, deflate, br, zstd                                      |
| accept-language    | str  |       | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7                          |
| priority           | str  | -     | u=1, i                                                       |

## 请求体

字符串拼接

| 字段     | 类型 | 内容      | 备注                                                         |
| -------- | ---- | --------- | ------------------------------------------------------------ |
| gameId   | num  | 游戏 id   | 战双 = 2, 鸣潮 = 3                                           |
| serverId | str  | 服务器 id | 战双: 星火服 = 1000, 信标服 = ?<br />鸣潮: 国服 = 76402e5b20be2c39f095a152090afddc, 其他未记录 |
| roleId   | num  | 游戏 uid  | 46218962                                                     |
| userId   | num  | 库洛 id   | 10065669                                                     |

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
| disposableGoodsList | arr | (?) |  |
| disposableSignNum | num | (?) | 5 |
| eventEndTimes | str  | 本期活动结束时间 | 2023-07-31 23:59:59                                         |
| eventStartTimes | str  | 本期活动开始时间 | 2023-07-01 00:00:00                  |
| expendGold | num  | (?) | https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadTwentyone.png |
| expendNum | num | (?) | 3 |
| isSigIn | bool | 今天是否已签到 | true, 注意这个字段单词拼写是错误的 |
| loopDescription | str | 限时签到描述 | 无 |
| loopEndTimes | str | 限时签到结束时间 | 2024-06-10 23:59:59 |
| loopSignName | str | 限时签到名称 | 限时签到 |
| loopSignNum | num | 限时签到已签天数 | 2 |
| loopStartTimes | str | 限时签到开始时间 | 2024-06-01 00:00:00 |
| nowServerTimes | str | 当前服务器时间 | 2023-07-16 17:41:43 |
| omissionNnm | num | 漏签天数   | 13 |
| openNotifica | bool | 弹窗通知(?) | false |
| redirectContent | str | (?) | taskCenter |
| redirectText | str | (?)   | 任务中心 |
| redirectType | num | (?)   | 2 |
| repleNum | num | (?)   | 0 |
| sigInNum | num | 签到天数 | 3, 注意这个字段单词拼写是错误的 |
| signInGoodsConfigs | arr | 签到奖励物品数组 |  |
| signLoopGoodsList | arr | 限时签到奖励物品数组 | |

### `signInGoodsConfigs` `signLoopGoodsList` 成员对象

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
    'pragma': 'no-cache',
    'cache-control': 'no-cache',
    'sec-ch-ua': '"Not)A;Brand";v="99", "Android WebView";v="127", "Chromium";v="127"',
    'source': 'android',
    'sec-ch-ua-mobile': '?1',
    'user-agent': 'Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.15 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0',
    'content-type': 'application/x-www-form-urlencoded',
    'accept': 'application/json, text/plain, */*',
    'devcode': '61.178.245.214, Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.15 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0',
    'token': 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'sec-ch-ua-platform': '"Android"',
    'origin': 'https://web-static.kurobbs.com',
    'sec-fetch-site': 'same-site',
    'sec-fetch-mode': 'cors',
    'sec-fetch-dest': 'empty',
    'accept-encoding': 'gzip, deflate, br, zstd',
    'accept-language': 'zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7',
    'priority': 'u=1, i',
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
    "disposableSignNum": 5,
    "eventEndTimes": "2024-06-30 23:59:59",
    "eventStartTimes": "2024-06-01 00:00:00",
    "expendGold": 200,
    "expendNum": 3,
    "isSigIn": false,
    "nowServerTimes": "2024-06-24 20:56:42",
    "omissionNnm": 0,
    "openNotifica": false,
    "redirectContent": "taskCenter",
    "redirectText": "任务中心",
    "redirectType": 2,
    "repleNum": 0,
    "sigInNum": 23,
    "signInGoodsConfigs": [
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 100000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/190aa57b24214baaab421a79e75f6bc420240528.png",
        "id": 900,
        "isGain": false,
        "serialNum": 0,
        "signId": 22
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 10,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/4c6845aefb36470ca7689057dc5ef21c20240528.png",
        "id": 901,
        "isGain": false,
        "serialNum": 1,
        "signId": 22
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/96448f44069c423c900d8056d81b9c9020240528.png",
        "id": 902,
        "isGain": false,
        "serialNum": 2,
        "signId": 22
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/501adb3295e94f0682b571938cd4957720240528.png",
        "id": 903,
        "isGain": false,
        "serialNum": 3,
        "signId": 22
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/eb4adabb73d74690ac54d08225639d0f20240528.png",
        "id": 904,
        "isGain": false,
        "serialNum": 4,
        "signId": 22
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/efaa880208a34f268796f5e4b4015c8f20240528.png",
        "id": 905,
        "isGain": false,
        "serialNum": 5,
        "signId": 22
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/6c6f3f4bc60d45aaad4bd518560aad5f20240528.png",
        "id": 906,
        "isGain": false,
        "serialNum": 6,
        "signId": 22
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 100000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/190aa57b24214baaab421a79e75f6bc420240528.png",
        "id": 907,
        "isGain": false,
        "serialNum": 7,
        "signId": 22
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 10,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/4c6845aefb36470ca7689057dc5ef21c20240528.png",
        "id": 908,
        "isGain": false,
        "serialNum": 8,
        "signId": 22
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/501adb3295e94f0682b571938cd4957720240528.png",
        "id": 909,
        "isGain": false,
        "serialNum": 9,
        "signId": 22
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/96448f44069c423c900d8056d81b9c9020240528.png",
        "id": 910,
        "isGain": false,
        "serialNum": 10,
        "signId": 22
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/eb4adabb73d74690ac54d08225639d0f20240528.png",
        "id": 911,
        "isGain": false,
        "serialNum": 11,
        "signId": 22
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/efaa880208a34f268796f5e4b4015c8f20240528.png",
        "id": 912,
        "isGain": false,
        "serialNum": 12,
        "signId": 22
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/6c6f3f4bc60d45aaad4bd518560aad5f20240528.png",
        "id": 913,
        "isGain": false,
        "serialNum": 13,
        "signId": 22
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 150000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/190aa57b24214baaab421a79e75f6bc420240528.png",
        "id": 914,
        "isGain": false,
        "serialNum": 14,
        "signId": 22
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/501adb3295e94f0682b571938cd4957720240528.png",
        "id": 915,
        "isGain": false,
        "serialNum": 15,
        "signId": 22
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 15,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/4c6845aefb36470ca7689057dc5ef21c20240528.png",
        "id": 916,
        "isGain": false,
        "serialNum": 16,
        "signId": 22
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/96448f44069c423c900d8056d81b9c9020240528.png",
        "id": 917,
        "isGain": false,
        "serialNum": 17,
        "signId": 22
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/eb4adabb73d74690ac54d08225639d0f20240528.png",
        "id": 918,
        "isGain": false,
        "serialNum": 18,
        "signId": 22
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/efaa880208a34f268796f5e4b4015c8f20240528.png",
        "id": 919,
        "isGain": false,
        "serialNum": 19,
        "signId": 22
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/6c6f3f4bc60d45aaad4bd518560aad5f20240528.png",
        "id": 920,
        "isGain": false,
        "serialNum": 20,
        "signId": 22
      },
      {
        "goodsId": 50005,
        "goodsName": "活动角色研发券",
        "goodsNum": 50,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/501adb3295e94f0682b571938cd4957720240528.png",
        "id": 921,
        "isGain": false,
        "serialNum": 21,
        "signId": 22
      },
      {
        "goodsId": 1,
        "goodsName": "螺母",
        "goodsNum": 150000,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/190aa57b24214baaab421a79e75f6bc420240528.png",
        "id": 922,
        "isGain": false,
        "serialNum": 22,
        "signId": 22
      },
      {
        "goodsId": 60001,
        "goodsName": "低级突破材料黑盒",
        "goodsNum": 15,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/4c6845aefb36470ca7689057dc5ef21c20240528.png",
        "id": 923,
        "isGain": false,
        "serialNum": 23,
        "signId": 22
      },
      {
        "goodsId": 30013,
        "goodsName": "经验仓·大",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/96448f44069c423c900d8056d81b9c9020240528.png",
        "id": 924,
        "isGain": false,
        "serialNum": 24,
        "signId": 22
      },
      {
        "goodsId": 31104,
        "goodsName": "武器强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/eb4adabb73d74690ac54d08225639d0f20240528.png",
        "id": 925,
        "isGain": false,
        "serialNum": 25,
        "signId": 22
      },
      {
        "goodsId": 31204,
        "goodsName": "意识强化素材Ⅳ",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/efaa880208a34f268796f5e4b4015c8f20240528.png",
        "id": 926,
        "isGain": false,
        "serialNum": 26,
        "signId": 22
      },
      {
        "goodsId": 60002,
        "goodsName": "高级突破材料黑盒",
        "goodsNum": 8,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/6c6f3f4bc60d45aaad4bd518560aad5f20240528.png",
        "id": 927,
        "isGain": false,
        "serialNum": 27,
        "signId": 22
      },
      {
        "goodsId": 40200,
        "goodsName": "支援突破套组·小",
        "goodsNum": 5,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/9ae9c0dfdf2f471396dd9ef01b08d6eb20240528.png",
        "id": 928,
        "isGain": false,
        "serialNum": 28,
        "signId": 22
      },
      {
        "goodsId": 90030,
        "goodsName": "中型血清组β",
        "goodsNum": 3,
        "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/0f95cc73699a43528e5ae4a8c98ff59220240528.png",
        "id": 929,
        "isGain": false,
        "serialNum": 29,
        "signId": 22
      }
    ],
    "signLoopGoodsList": []
  },
  "msg": "请求成功",
  "success": true
}
```
