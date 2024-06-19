# 鸣潮游戏角色声骸收集数据

包含 `数据坞信息` 和 `声骸收集进度`

更新时间: 2024.06.19

## 请求地址

> https://api.kurobbs.com/gamer/roleBox/aki/calabashData

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

| 字段   | 类型 | 内容        | 备注                                                         |
| ------ | ---- | ----------- | ------------------------------------------------------------ |
| gameId | num  | 游戏 id     | 固定 鸣潮 = 3                                                |
| roleId | num  | 游戏角色 id | 101812955                                                    |
| gameId | num  | 游戏区服 id | CN = 76402e5b20be2c39f095a152090afddc<br />OS 每个区都不一样, 无完整记录 |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 | 请求成功                       |
| success | bool | true     | token 有效时才有               |
| data    | arr  | 详细信息 | 成功时才有, 没绑定就是空数组   |

### `data` 成员对象

| 字段             | 类型 | 内容                  | 备注          |
| ---------------- | ---- | --------------------- | ------------- |
| level             | num | 数据坞等级 | 16 |
| baseCatch    | str | 基础吸收概率 | 20% |
| strengthenCatch | str | 强化吸收概率 | 80% |
| catchQuality | num | 最高可吸收品质 | 5 |
| cost     | num | COST 上限 | 12 |
| maxCount     | num | 声骸收集进度上限 | 208 |
| unlockCount  | num | 当前声骸收集进度 | 170 |
| phantomList             | arr | 声骸信息数组 |           |

### `phantomList` 数组成员对象

| 字段    | 类型 | 内容         | 备注 |
| ------- | ---- | ------------ | ---- |
| phantom | obj  | 声骸信息对象 |      |
| star    | num  | 已收集星级   | 4    |
| maxStar | num  | 最高星级     | 4    |

### `phantom` 成员对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| name      | str  | 声骸名称     | 坚岩斗士                                                     |
| phantomId | num  | 声骸 id      | 390077021                                                    |
| cost      | num  | 声骸 COST    | 3                                                            |
| iconUrl   | str  | 声骸图标     | https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031252086.png |
| acronym   | str  | 声骸名称音序 | jyds, 牢库你真是抽抽又象象啊                                 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/gamer/roleBox/aki/calabashData'
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
        "level": 16,
        "baseCatch": "20%",
        "strengthenCatch": "80%",
        "catchQuality": 5,
        "cost": 12,
        "maxCount": 208,
        "unlockCount": 170,
        "phantomList": [
            {
                "phantom": {
                    "name": "坚岩斗士",
                    "phantomId": 390077021,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031252086.png",
                    "acronym": "jyds"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "寒霜陆龟",
                    "phantomId": 390070105,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031140317.png",
                    "acronym": "hslq"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "审判战士",
                    "phantomId": 390070065,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031277969.png",
                    "acronym": "spzs"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "奏谕乐师",
                    "phantomId": 390077022,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031553238.png",
                    "acronym": "zyls"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "呜咔咔",
                    "phantomId": 390070069,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030821526.png",
                    "acronym": "wkk"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "碎獠猪",
                    "phantomId": 390070075,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031420517.png",
                    "acronym": "slz"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "鸣泣战士",
                    "phantomId": 390070064,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031220479.png",
                    "acronym": "mqzs"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "无冠者",
                    "phantomId": 6000042,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031387956.png",
                    "acronym": "wgz"
                },
                "star": 2,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "振铎乐师",
                    "phantomId": 390077023,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031258204.png",
                    "acronym": "zdls"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "先锋幼岩",
                    "phantomId": 390070051,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031317562.png",
                    "acronym": "xfyy"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "刺玫菇（稚形）",
                    "phantomId": 390070079,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031563789.png",
                    "acronym": "cmg"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "火鬃狼",
                    "phantomId": 390070100,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031107636.png",
                    "acronym": "hzl"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "呼咻咻",
                    "phantomId": 390070068,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031570963.png",
                    "acronym": "hxx"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "湮灭棱镜",
                    "phantomId": 390077017,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031187899.png",
                    "acronym": "ymlj"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "箭簇熊",
                    "phantomId": 390077038,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031054393.png",
                    "acronym": "jcx"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "热熔棱镜",
                    "phantomId": 390077012,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031097315.png",
                    "acronym": "rrlj"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "磐石守卫",
                    "phantomId": 390077024,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030841263.png",
                    "acronym": "pssw"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "巡哨机傀",
                    "phantomId": 6000049,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031113039.png",
                    "acronym": "xsjk"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "裂变幼岩",
                    "phantomId": 390070052,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031197499.png",
                    "acronym": "lbyy"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "破霜猎手",
                    "phantomId": 390070070,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031332563.png",
                    "acronym": "psls"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "飞廉之猩",
                    "phantomId": 6000043,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030978516.png",
                    "acronym": "flzx"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "衍射棱镜",
                    "phantomId": 390077016,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031031142.png",
                    "acronym": "yslj"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "惊蛰猎手",
                    "phantomId": 390070053,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030984882.png",
                    "acronym": "jzls"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "冥渊守卫",
                    "phantomId": 390077025,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031299728.png",
                    "acronym": "mysw"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "燎照之骑",
                    "phantomId": 390080007,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031254258.png",
                    "acronym": "lzzq"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "咔嚓嚓",
                    "phantomId": 390070066,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030833398.png",
                    "acronym": "kcc"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "暗鬃狼",
                    "phantomId": 390077033,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031155308.png",
                    "acronym": "azl"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "戏猿",
                    "phantomId": 6000040,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031211681.png",
                    "acronym": "xy"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "幼猿",
                    "phantomId": 6000038,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031515688.png",
                    "acronym": "yy"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "冷凝棱镜",
                    "phantomId": 390077013,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031298656.png",
                    "acronym": "lnlj"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "巡徊猎手",
                    "phantomId": 390070071,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031100054.png",
                    "acronym": "xhls"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "绿熔蜥",
                    "phantomId": 390077028,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031022897.png",
                    "acronym": "lrx"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "绿熔蜥（稚形）",
                    "phantomId": 390070078,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031470942.png",
                    "acronym": "lrx"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "晶螯蝎",
                    "phantomId": 6000041,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031107501.png",
                    "acronym": "jax"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "刺玫菇",
                    "phantomId": 390077029,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031066539.png",
                    "acronym": "cmg"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "咕咕河豚",
                    "phantomId": 390070076,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031045800.png",
                    "acronym": "gght"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "青羽鹭",
                    "phantomId": 390077005,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031319273.png",
                    "acronym": "qyl"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "车刃镰",
                    "phantomId": 6000046,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030964752.png",
                    "acronym": "crl"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "游弋蝶",
                    "phantomId": 390070074,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031420750.png",
                    "acronym": "yyd"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "通行灯偶",
                    "phantomId": 6000050,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031467856.png",
                    "acronym": "txdo"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "啾啾河豚",
                    "phantomId": 6000047,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031083470.png",
                    "acronym": "jjht"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "辉萤军势",
                    "phantomId": 6000044,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030871596.png",
                    "acronym": "hyjs"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "遁地鼠",
                    "phantomId": 390070077,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031044125.png",
                    "acronym": "dds"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "聚械机偶",
                    "phantomId": 6000048,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030905371.png",
                    "acronym": "jxjo"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "哀声鸷",
                    "phantomId": 6000045,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031069457.png",
                    "acronym": "asz"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "鸣钟之龟",
                    "phantomId": 390080005,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031298428.png",
                    "acronym": "mzzq"
                },
                "star": 2,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "无妄者",
                    "phantomId": 6000053,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716030917799.png",
                    "acronym": "wwz"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "紫羽鹭",
                    "phantomId": 390077004,
                    "cost": 3,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031255040.png",
                    "acronym": "zyl"
                },
                "star": 4,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "朔雷之鳞",
                    "phantomId": 6000039,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031325516.png",
                    "acronym": "slzl"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "无常凶鹭",
                    "phantomId": 6000052,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031585620.png",
                    "acronym": "wcxl"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "阿嗞嗞",
                    "phantomId": 390070067,
                    "cost": 1,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031091634.png",
                    "acronym": "azz"
                },
                "star": 3,
                "maxStar": 4
            },
            {
                "phantom": {
                    "name": "云闪之鳞",
                    "phantomId": 390080003,
                    "cost": 4,
                    "iconUrl": "https://web-static.kurobbs.com/adminConfig/35/phantom_icon/1716031148133.png",
                    "acronym": "yszl"
                },
                "star": 3,
                "maxStar": 4
            }
        ]
    },
    "success": true
}
```