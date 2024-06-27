# 鸣潮游戏角色基础数据

包含 `日常数据` 和 `我的资料`

更新时间: 2024.06.19

## 请求地址

> https://api.kurobbs.com/gamer/roleBox/aki/baseData

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
| sec-ch-ua-mobile   | str  | 1     | ?1                                                           |
| user-agent         | str  | UA    | Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.2 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0 |
| content-type       | str  | -     | application/x-www-form-urlencoded                            |
| accept             | str  | -     | application/json, text/plain, \*/\*                          |
| devcode            | str  | -     | 61.178.245.214, Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.2 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0 |
| token              | str  | token | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| sec-ch-ua-platform | str  | -     | "Android"                                                    |
| origin             | str  |       | https://web-static.kurobbs.com                               |
| sec-fetch-site     | str  |       | same-site                                                    |
| sec-fetch-mode     | str  |       | cors                                                         |
| sec-fetch-dest     | str  |       | empty                                                        |
| accept-encoding    | str  |       | gzip, deflate, br, zstd                                      |
| accept-language    | str  |       | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7                          |
| priority           | str  | (?)   | u=1, i                                                       |

## 请求体

字符串拼接

| 字段     | 类型 | 内容        | 备注                                                         |
| -------- | ---- | ----------- | ------------------------------------------------------------ |
| gameId   | num  | 游戏 id     | 固定 鸣潮 = 3                                                |
| roleId   | num  | 游戏角色 id | 101812955                                                    |
| serverId | num  | 游戏区服 id | CN = 76402e5b20be2c39f095a152090afddc<br />OS 每个区都不一样, 无完整记录 |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 | 请求成功                       |
| success | bool | true     | token 有效时才有               |
| data    | arr  | 详细信息 | 成功时才有, 没绑定就是空数组   |

### `data`成员对象

| 字段             | 类型 | 内容                  | 备注          |
| ---------------- | ---- | --------------------- | ------------- |
| name             | str  | 角色昵称              | 首席          |
| id               | num  | 角色 id               | 101812955     |
| creatTime        | num  | 创角时间, 13 位时间戳 | 1716426597815 |
| activeDays       | num  | 游戏天数              | 28            |
| level            | num  | 联觉等级              | 40            |
| worldLevel       | num  | 索拉等级              | 5             |
| roleNum          | num  | 解锁角色              | 16            |
| soundBox         | num  | 解锁声匣数            | 7             |
| energy           | num  | 当前结晶波片          | 206           |
| maxEnergy        | num  | 结晶波片上限          | 240           |
| liveness         | num  | 今日活跃度            | 100           |
| livenessMaxCount | num  | 今日活跃度上限        | true          |
| livenessUnlock   | bool | 解锁了活跃度?         | true          |
| chapterId        | num  | (?)                   | 7             |
| bigCount         | num  | 中型信标解锁数        | 10            |
| smallCount       | num  | 小型信标解锁数        | 60            |
| achievementCount | num  | 已达成成就            | 67            |
| boxList          | arr  | 宝箱列表              |               |
| showToGuest      | num  | 对外展示              | true          |

### `boxList`数组成员对象

| 字段    | 类型 | 内容       | 备注       |
| ------- | ---- | ---------- | ---------- |
| boxName | str  | 宝箱名称   | 朴素奇藏箱 |
| num     | num  | 已获得数量 | 56         |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/gamer/roleBox/aki/baseData'
const headers = {
    pragma: 'no-cache',
    cache-control: 'no-cache',
    sec-ch-ua: '"Not)A;Brand";v="99", "Android WebView";v="127", "Chromium";v="127"',
    source: 'android',
    sec-ch-ua-mobile: '?1',
    user-agent: 'Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.2 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0',
    content-type: 'application/x-www-form-urlencoded',
    accept: 'application/json, text/plain, */*',
    devcode: '61.178.245.214, Mozilla/5.0 (Linux; Android 14; 23127PN0CC Build/UKQ1.230804.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/127.0.6533.2 Mobile Safari/537.36 Kuro/2.2.0 KuroGameBox/2.2.0',
    token: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    sec-ch-ua-platform: ''"Android"',
    origin: 'https://web-static.kurobbs.com',
    sec-fetch-site: 'same-site',
    sec-fetch-mode: 'cors',
    sec-fetch-dest: 'empty',
    accept-encoding: 'gzip, deflate, br, zstd',
    accept-language: 'zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7',
    priority: 'u=1, i',
}

const formData = new URLSearchParams()
formData.append('gameId', 3)
formData.append('roleId', '101812955')
formData.append('serverId', '76402e5b20be2c39f095a152090afddc')
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
    "msg": "请求成功",
    "data": {
        "name": "首席",
        "id": 101812955,
        "creatTime": 1716426597815,
        "activeDays": 28,
        "level": 40,
        "worldLevel": 5,
        "roleNum": 16,
        "soundBox": 7,
        "energy": 206,
        "maxEnergy": 240,
        "liveness": 100,
        "livenessMaxCount": 100,
        "livenessUnlock": true,
        "chapterId": 7,
        "bigCount": 10,
        "smallCount": 60,
        "achievementCount": 67,
        "boxList": [
            {
                "boxName": "朴素奇藏箱",
                "num": 56
            },
            {
                "boxName": "基准奇藏箱",
                "num": 29
            },
            {
                "boxName": "精密奇藏箱",
                "num": 9
            },
            {
                "boxName": "辉光奇藏箱",
                "num": 2
            }
        ],
        "showToGuest": true
    },
    "success": true
}
```