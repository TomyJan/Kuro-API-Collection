# 鸣潮游戏角色探索数据

更新时间: 2024.06.19

# 状态

<font color=Red>已失效</font>，替代方案：[[新] 鸣潮游戏角色探索数据](../../../aki/roleBox/akiBox/baseData.md)

## 请求地址

> https://api.kurobbs.com/gamer/roleBox/aki/exploreIndex

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

| 字段        | 类型 | 内容              | 备注                                                         |
| ----------- | ---- | ----------------- | ------------------------------------------------------------ |
| gameId      | num  | 游戏 id           | 固定 鸣潮 = 3                                                |
| roleId      | num  | 游戏角色 id       | 101812955                                                    |
| gameId      | num  | 游戏区服 id       | CN = 76402e5b20be2c39f095a152090afddc<br />OS 每个区都不一样, 无完整记录 |
| channelId   | num  | 游戏区服渠道 id ? | 19                                                           |
| countryCode | num  | 国家代码          | 璜珑 = 1                                                     |

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

| 字段            | 类型 | 内容             | 备注 |
| --------------- | ---- | ---------------- | ---- |
| countryCode | num  | 国家代码 | 1 |
| countryName | str  | 国家名称 | 璜珑 |
| countryProgress | str  | 国家探索度% | 18.40 |
| areaInfoList | arr  | 地区探索信息数组 |     |
| detectionInfoList | arr  | 残象探寻信息数组, 应该是只包含已发现的残像?懒得上小号测试 |     |
| open       | bool | 对外显示 | true |

### `areaInfoList` 数组成员对象

| 字段         | 类型 | 内容                   | 备注   |
| ------------ | ---- | ---------------------- | ------ |
| areaId       | num  | 地区 id                | 2      |
| areaProgress | num  | 地区探索进度%          | 11     |
| areaName     | str  | 地区名称               | 云陵谷 |
| itemList     | arr  | 地区的探索物品进度数组 |        |

### `itemList` 数组成员对象

| 字段     | 类型 | 内容          | 备注                                                         |
| -------- | ---- | ------------- | ------------------------------------------------------------ |
| type     | num  | 物品类型      | 1-5 分别对应 奇藏, 信标, 声匣, 观景点, 飞猎手                |
| name     | str  | 物品名称      | `type` 对应物品名称                                          |
| progress | num  | 物品收集进度% | https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030815569.png |

### `detectionInfoList` 数组成员对象

| 字段          | 类型 | 内容                           | 备注                                                         |
| ------------- | ---- | ------------------------------ | ------------------------------------------------------------ |
| detectionId   | num  | 残象 id                        | 310000090                                                    |
| detectionName | str  | 残象名称                       | 阿嗞嗞                                                       |
| detectionIcon | str  | 残象图标                       | https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030815569.png |
| level         | num  | 残象等级                       | 0-3 分别对应轻波, 巨浪, 怒涛, 海啸级                         |
| levelName     | str  | 等级名称                       | `level` 对应名称                                             |
| acronym       | str  | 残象名称音序, 应该是用来排序的 | azz, 幽默牢库                                                |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/gamer/roleBox/aki/exploreIndex'
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
formData.append('channelId', 19)
formData.append('countryCode', 1)
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
        "countryCode": 1,
        "countryName": "瑝珑",
        "countryProgress": "18.40",
        "areaInfoList": [
            {
                "areaId": 2,
                "areaProgress": 11,
                "areaName": "云陵谷",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 50
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 0
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 9
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 3,
                "areaProgress": 26,
                "areaName": "今州城",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 100
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 23
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 2
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 4,
                "areaProgress": 21,
                "areaName": "中曲台地",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 89
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 10
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 14
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 15
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 5,
                "areaProgress": 12,
                "areaName": "荒石高地",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 89
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 9
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 2
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 6,
                "areaProgress": 20,
                "areaName": "归墟港市",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 100
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 10
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 23
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 7,
                "areaProgress": 10,
                "areaName": "无光之森",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 70
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 8
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 3
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 8,
                "areaProgress": 21,
                "areaName": "无明湾",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 75
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 0
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 12
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 100
                    }
                ]
            },
            {
                "areaId": 9,
                "areaProgress": 21,
                "areaName": "北落野",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 100
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 0
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 22
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 20
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            },
            {
                "areaId": 10,
                "areaProgress": 20,
                "areaName": "怨鸟泽",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 100
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 17
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 10
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 34
                    }
                ]
            },
            {
                "areaId": 12,
                "areaProgress": 22,
                "areaName": "虎口山脉",
                "itemList": [
                    {
                        "type": 2,
                        "name": "信标",
                        "progress": 100
                    },
                    {
                        "type": 3,
                        "name": "声匣",
                        "progress": 0
                    },
                    {
                        "type": 1,
                        "name": "奇藏",
                        "progress": 9
                    },
                    {
                        "type": 5,
                        "name": "飞猎手",
                        "progress": 0
                    },
                    {
                        "type": 4,
                        "name": "观景点",
                        "progress": 0
                    }
                ]
            }
        ],
        "detectionInfoList": [
            {
                "detectionId": 310000090,
                "detectionName": "阿嗞嗞",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030815569.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "azz"
            },
            {
                "detectionId": 310000070,
                "detectionName": "审判战士",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031095744.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "spzs"
            },
            {
                "detectionId": 320000010,
                "detectionName": "坚岩斗士",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031161397.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "jyds"
            },
            {
                "detectionId": 310000080,
                "detectionName": "咔嚓嚓",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031321014.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "kcc"
            },
            {
                "detectionId": 310000270,
                "detectionName": "寒霜陆龟",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031247513.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "hslq"
            },
            {
                "detectionId": 310000220,
                "detectionName": "刺玫菇（稚形）",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030989042.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "cmg"
            },
            {
                "detectionId": 320000090,
                "detectionName": "刺玫菇",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031258622.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "cmg"
            },
            {
                "detectionId": 310000030,
                "detectionName": "惊蛰猎手",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031491490.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "jzls"
            },
            {
                "detectionId": 320000040,
                "detectionName": "奏谕乐师",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030876719.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "zyls"
            },
            {
                "detectionId": 320000050,
                "detectionName": "振铎乐师",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031120625.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "zdls"
            },
            {
                "detectionId": 310000290,
                "detectionName": "残星·重锤造匠",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030829445.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "cxzczj"
            },
            {
                "detectionId": 310000230,
                "detectionName": "流放者",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031430200.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "lfz"
            },
            {
                "detectionId": 310000240,
                "detectionName": "流放者",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030691129.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "lfz"
            },
            {
                "detectionId": 320000100,
                "detectionName": "暗鬃狼",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031226069.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "azl"
            },
            {
                "detectionId": 310000060,
                "detectionName": "鸣泣战士",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030641633.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "mqzs"
            },
            {
                "detectionId": 320000070,
                "detectionName": "冥渊守卫",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030909673.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "mysw"
            },
            {
                "detectionId": 310000010,
                "detectionName": "先锋幼岩",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030751611.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "xfyy"
            },
            {
                "detectionId": 310000310,
                "detectionName": "残星·枭面造匠",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031366349.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "cxxmzj"
            },
            {
                "detectionId": 310000320,
                "detectionName": "残星·枪肢造匠",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030761155.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "cxqzzj"
            },
            {
                "detectionId": 310000050,
                "detectionName": "巡徊猎手",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031152132.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "xhls"
            },
            {
                "detectionId": 310000040,
                "detectionName": "破霜猎手",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031321698.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "psls"
            },
            {
                "detectionId": 310000110,
                "detectionName": "呜咔咔",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031361824.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "wkk"
            },
            {
                "detectionId": 310000190,
                "detectionName": "碎獠猪",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031232055.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "slz"
            },
            {
                "detectionId": 310000330,
                "detectionName": "通行灯偶",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031273666.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "txdo"
            },
            {
                "detectionId": 340000010,
                "detectionName": "无冠者",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031219597.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "wgz"
            },
            {
                "detectionId": 310000200,
                "detectionName": "遁地鼠",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031038850.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "dds"
            },
            {
                "detectionId": 310000280,
                "detectionName": "火鬃狼",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031141403.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "hzl"
            },
            {
                "detectionId": 310000210,
                "detectionName": "绿熔蜥（稚形）",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030899564.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "lrx"
            },
            {
                "detectionId": 310000100,
                "detectionName": "呼咻咻",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030979166.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "hxx"
            },
            {
                "detectionId": 310000170,
                "detectionName": "湮灭棱镜",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030656708.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "ymlj"
            },
            {
                "detectionId": 320000120,
                "detectionName": "箭簇熊",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031399289.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "jcx"
            },
            {
                "detectionId": 310000150,
                "detectionName": "热熔棱镜",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031077266.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "rrlj"
            },
            {
                "detectionId": 310000300,
                "detectionName": "锐爪幼猿",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030819623.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "rzyy"
            },
            {
                "detectionId": 310000250,
                "detectionName": "抛石幼猿",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031461148.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "psyy"
            },
            {
                "detectionId": 320000080,
                "detectionName": "绿熔蜥",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031125251.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "lrx"
            },
            {
                "detectionId": 320000060,
                "detectionName": "磐石守卫",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031161358.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "pssw"
            },
            {
                "detectionId": 320000180,
                "detectionName": "巡哨机傀",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030705837.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "xsjk"
            },
            {
                "detectionId": 310000020,
                "detectionName": "裂变幼岩",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031432712.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "lbyy"
            },
            {
                "detectionId": 330000050,
                "detectionName": "飞廉之猩",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031388165.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "flzx"
            },
            {
                "detectionId": 310000120,
                "detectionName": "咕咕河豚",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031478234.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "gght"
            },
            {
                "detectionId": 310000160,
                "detectionName": "衍射棱镜",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030644671.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "yslj"
            },
            {
                "detectionId": 320000030,
                "detectionName": "青羽鹭",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031106633.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "qyl"
            },
            {
                "detectionId": 310000260,
                "detectionName": "晶螯蝎",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031342539.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "jax"
            },
            {
                "detectionId": 320000020,
                "detectionName": "紫羽鹭",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030668633.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "zyl"
            },
            {
                "detectionId": 340000060,
                "detectionName": "聚械机偶",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030880507.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "jxjo"
            },
            {
                "detectionId": 320000140,
                "detectionName": "流放者首领",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030626717.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "lfzsl"
            },
            {
                "detectionId": 310000130,
                "detectionName": "啾啾河豚",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030791984.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "jjht"
            },
            {
                "detectionId": 310000180,
                "detectionName": "游弋蝶",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030949830.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "yyd"
            },
            {
                "detectionId": 340000080,
                "detectionName": "云闪之鳞",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031349963.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "yszl"
            },
            {
                "detectionId": 320000170,
                "detectionName": "躁乱戏猿",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031402652.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "zlxy"
            },
            {
                "detectionId": 310000140,
                "detectionName": "冷凝棱镜",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030935676.png",
                "level": 0,
                "levelName": "轻波级",
                "acronym": "lnlj"
            },
            {
                "detectionId": 320000110,
                "detectionName": "嚣风戏猿",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030908489.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "xfxy"
            },
            {
                "detectionId": 320000150,
                "detectionName": "流放者工匠",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030799354.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "lfzgj"
            },
            {
                "detectionId": 320000160,
                "detectionName": "处刑人",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031173114.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "cxr"
            },
            {
                "detectionId": 320000130,
                "detectionName": "车刃镰",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030916964.png",
                "level": 1,
                "levelName": "巨浪级",
                "acronym": "crl"
            },
            {
                "detectionId": 330000020,
                "detectionName": "燎照之骑",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031506434.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "lzzq"
            },
            {
                "detectionId": 330000040,
                "detectionName": "辉萤军势",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030878197.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "hyjs"
            },
            {
                "detectionId": 330000060,
                "detectionName": "哀声鸷",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030669661.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "asz"
            },
            {
                "detectionId": 340000020,
                "detectionName": "鸣钟之龟",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031304621.png",
                "level": 3,
                "levelName": "海啸级",
                "acronym": "mzzq"
            },
            {
                "detectionId": 340000070,
                "detectionName": "无妄者",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716031326113.png",
                "level": 3,
                "levelName": "海啸级",
                "acronym": "wwz"
            },
            {
                "detectionId": 330000030,
                "detectionName": "无常凶鹭",
                "detectionIcon": "https://web-static.kurobbs.com/adminConfig/34/monster_icon/1716030629902.png",
                "level": 2,
                "levelName": "怒涛级",
                "acronym": "wcxl"
            }
        ],
        "open": true
    },
    "success": true
}
```