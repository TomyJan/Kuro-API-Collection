# 取游戏签到信息 V2

更新时间: 2024.06.29

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
| disposableGoodsList | arr | 新手(针对游戏角色)一次性签到签到奖励物品数组 | 已经做过了就是空数组 |
| disposableSignNum | num | 新手(针对游戏角色)一次性签到活动已签天数? | 目前签满了就是 5 天 |
| eventEndTimes | str  | 本期活动结束时间 | 2024-06-30 23:59:59                      |
| eventStartTimes | str  | 本期活动开始时间 | 2024-06-01 00:00:00 |
| expendGold | num  | 补签消耗库洛币数量 | https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadTwentyone.png |
| expendNum | num | 剩余补签次数 | 一个月 3 次 |
| isSigIn | bool | 今天是否已签到 | true, 注意这个字段单词拼写是错误的 |
| loopDescription | str | 限时签到描述 | 无 |
| loopEndTimes | str | 限时签到结束时间 | 2024-07-12 23:59:59 |
| loopSignName | str | 限时签到名称 | 限时签到 / 限时签到活动 |
| loopSignNum | num | 限时签到已签天数 | 1 |
| loopStartTimes | str | 限时签到开始时间 | 2024-06-28 13:00:00 |
| nowServerTimes | str | 当前服务器时间 | 2024-06-29 01:42:55                                          |
| omissionNnm | num | 漏签天数   | 28 |
| openNotifica | bool | 弹窗通知(?) | false |
| redirectContent | str | (?) | taskCenter |
| redirectText | str | (?)   | 任务中心 |
| redirectType | num | (?)   | 2 |
| repleNum | num | (?)   | 0 |
| sigInNum | num | 签到天数 | 1, 注意这个字段单词拼写是错误的 |
| signInGoodsConfigs | arr | 签到奖励物品数组 |  |
| signLoopGoodsList | arr | 限时签到奖励物品数组 | |

### `disposableGoodsList` `signInGoodsConfigs` `signLoopGoodsList` 成员对象

注意三个签到活动数组成员有所不同

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| goodsId | num  | 物品 id | 1                  |
| goodsName | str | 物品名称 | 螺母 |
| goodsNum | num  | 物品数量 | 100000 |
| goodsUrl | str | 物品图标链接 | https://prod-alicdn-community.kurobbs.com/signInIcon/81d4054407ee4a87bfb0171fc43881b220240518.png |
| id | num | (?) | 只有 `signInGoodsConfigs` 有, 递增 |
| isGain | bool | 是否已获得 | false |
| serialNum | num | (?) | `disposableGoodsList` 中为签到几天可获得, 其他俩为从 0 开始递增 |
| signId | num | (?) | `disposableGoodsList` 没有, (?)日常签到 = 21, 限时签到 = 6 |

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
        "disposableGoodsList": [
            {
                "goodsId": 10000,
                "goodsName": "星声",
                "goodsNum": 10,
                "goodsUrl": "https://web-static.kurobbs.com/game/item/3/3.png",
                "isGain": true,
                "serialNum": 1
            },
            {
                "goodsId": 10000,
                "goodsName": "星声",
                "goodsNum": 20,
                "goodsUrl": "https://web-static.kurobbs.com/game/item/3/3.png",
                "isGain": false,
                "serialNum": 3
            },
            {
                "goodsId": 10000,
                "goodsName": "星声",
                "goodsNum": 30,
                "goodsUrl": "https://web-static.kurobbs.com/game/item/3/3.png",
                "isGain": false,
                "serialNum": 5
            }
        ],
        "disposableSignNum": 1,
        "eventEndTimes": "2024-06-30 23:59:59",
        "eventStartTimes": "2024-06-01 00:00:00",
        "expendGold": 200,
        "expendNum": 3,
        "isSigIn": true,
        "loopDescription": "无",
        "loopEndTimes": "2024-07-12 23:59:59",
        "loopSignName": "限时签到活动",
        "loopSignNum": 1,
        "loopStartTimes": "2024-06-28 13:00:00",
        "nowServerTimes": "2024-06-29 01:42:55",
        "omissionNnm": 28,
        "openNotifica": false,
        "redirectContent": "taskCenter",
        "redirectText": "任务中心",
        "redirectType": 2,
        "repleNum": 0,
        "sigInNum": 1,
        "signInGoodsConfigs": [
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 870,
                "isGain": false,
                "serialNum": 0,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 871,
                "isGain": false,
                "serialNum": 1,
                "signId": 21
            },
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 20,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/14b7f2470950490eb827d63180f4721720240526.png",
                "id": 872,
                "isGain": false,
                "serialNum": 2,
                "signId": 21
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 8000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/044a8c4edc2f49bdb252fa482d5c2e4220240526.png",
                "id": 873,
                "isGain": false,
                "serialNum": 3,
                "signId": 21
            },
            {
                "goodsId": 36000002,
                "goodsName": "中级密音筒",
                "goodsNum": 1,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/d1f43ceb94464f87a6d4a5c6e9639a6c20240526.png",
                "id": 874,
                "isGain": false,
                "serialNum": 4,
                "signId": 21
            },
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 875,
                "isGain": false,
                "serialNum": 5,
                "signId": 21
            },
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 20,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/14b7f2470950490eb827d63180f4721720240526.png",
                "id": 876,
                "isGain": false,
                "serialNum": 6,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 877,
                "isGain": false,
                "serialNum": 7,
                "signId": 21
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 8000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/044a8c4edc2f49bdb252fa482d5c2e4220240526.png",
                "id": 878,
                "isGain": false,
                "serialNum": 8,
                "signId": 21
            },
            {
                "goodsId": 36000002,
                "goodsName": "中级密音筒",
                "goodsNum": 1,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/d1f43ceb94464f87a6d4a5c6e9639a6c20240526.png",
                "id": 879,
                "isGain": false,
                "serialNum": 9,
                "signId": 21
            },
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 880,
                "isGain": false,
                "serialNum": 10,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 881,
                "isGain": false,
                "serialNum": 11,
                "signId": 21
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 10000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/044a8c4edc2f49bdb252fa482d5c2e4220240526.png",
                "id": 882,
                "isGain": false,
                "serialNum": 12,
                "signId": 21
            },
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 20,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/14b7f2470950490eb827d63180f4721720240526.png",
                "id": 883,
                "isGain": false,
                "serialNum": 13,
                "signId": 21
            },
            {
                "goodsId": 36000002,
                "goodsName": "中级密音筒",
                "goodsNum": 1,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/d1f43ceb94464f87a6d4a5c6e9639a6c20240526.png",
                "id": 884,
                "isGain": false,
                "serialNum": 14,
                "signId": 21
            },
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 885,
                "isGain": false,
                "serialNum": 15,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 886,
                "isGain": false,
                "serialNum": 16,
                "signId": 21
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 12000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/044a8c4edc2f49bdb252fa482d5c2e4220240526.png",
                "id": 887,
                "isGain": false,
                "serialNum": 17,
                "signId": 21
            },
            {
                "goodsId": 36000002,
                "goodsName": "中级密音筒",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/d1f43ceb94464f87a6d4a5c6e9639a6c20240526.png",
                "id": 888,
                "isGain": false,
                "serialNum": 18,
                "signId": 21
            },
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 889,
                "isGain": false,
                "serialNum": 19,
                "signId": 21
            },
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 20,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/14b7f2470950490eb827d63180f4721720240526.png",
                "id": 890,
                "isGain": false,
                "serialNum": 20,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 891,
                "isGain": false,
                "serialNum": 21,
                "signId": 21
            },
            {
                "goodsId": 36000002,
                "goodsName": "中级密音筒",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/d1f43ceb94464f87a6d4a5c6e9639a6c20240526.png",
                "id": 892,
                "isGain": false,
                "serialNum": 22,
                "signId": 21
            },
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 3,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 893,
                "isGain": false,
                "serialNum": 23,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 894,
                "isGain": false,
                "serialNum": 24,
                "signId": 21
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 12000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/044a8c4edc2f49bdb252fa482d5c2e4220240526.png",
                "id": 895,
                "isGain": false,
                "serialNum": 25,
                "signId": 21
            },
            {
                "goodsId": 36000002,
                "goodsName": "中级密音筒",
                "goodsNum": 2,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/d1f43ceb94464f87a6d4a5c6e9639a6c20240526.png",
                "id": 896,
                "isGain": false,
                "serialNum": 26,
                "signId": 21
            },
            {
                "goodsId": 43010002,
                "goodsName": "中级共鸣促剂",
                "goodsNum": 3,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c2113b8bfc15446c8ba3d7bbb457519720240526.png",
                "id": 897,
                "isGain": false,
                "serialNum": 27,
                "signId": 21
            },
            {
                "goodsId": 43020002,
                "goodsName": "中级能源核心",
                "goodsNum": 3,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/ecd8c9d1ceab42df8b21bab2544fae6920240526.png",
                "id": 898,
                "isGain": false,
                "serialNum": 28,
                "signId": 21
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 12000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/044a8c4edc2f49bdb252fa482d5c2e4220240526.png",
                "id": 899,
                "isGain": false,
                "serialNum": 29,
                "signId": 21
            }
        ],
        "signLoopGoodsList": [
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 30,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/9824a29ae13748c1adaa92f266326f9320240626.png",
                "isGain": true,
                "serialNum": 0,
                "signId": 6
            },
            {
                "goodsId": 43010003,
                "goodsName": "高级共鸣促剂",
                "goodsNum": 3,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/8a41f941d7a9429da8cd6b88a0d8313020240626.png",
                "isGain": false,
                "serialNum": 1,
                "signId": 6
            },
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 30,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/9824a29ae13748c1adaa92f266326f9320240626.png",
                "isGain": false,
                "serialNum": 2,
                "signId": 6
            },
            {
                "goodsId": 43020003,
                "goodsName": "高级能源核心",
                "goodsNum": 3,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/c394c7e6d89a4d70babdda5f4c3c3c1520240626.png",
                "isGain": false,
                "serialNum": 3,
                "signId": 6
            },
            {
                "goodsId": 2,
                "goodsName": "贝币",
                "goodsNum": 30000,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/92bd173eb11c465088d9793a6707d15620240626.png",
                "isGain": false,
                "serialNum": 4,
                "signId": 6
            },
            {
                "goodsId": 36000003,
                "goodsName": "高级密音筒",
                "goodsNum": 3,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/b8ad7ce119e14d1aa9c6037e42fe6a7f20240626.png",
                "isGain": false,
                "serialNum": 5,
                "signId": 6
            },
            {
                "goodsId": 3,
                "goodsName": "星声",
                "goodsNum": 40,
                "goodsUrl": "https://prod-alicdn-community.kurobbs.com/signInIcon/9824a29ae13748c1adaa92f266326f9320240626.png",
                "isGain": false,
                "serialNum": 6,
                "signId": 6
            }
        ]
    },
    "msg": "请求成功",
    "success": true
}
```
