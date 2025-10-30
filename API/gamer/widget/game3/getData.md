# 鸣潮小组件数据

注意这里同一个 API 有两套请求参数, 分别用于库街区内`数据终端`页面和桌面小组件数据更新, 但是响应参数一致, 下文都有说明

更新时间: 2025.01.13

## 请求地址

> ~~库街区内: https://event.kurobbs.com/gamer/widget/game3/getData~~ 又改回去了
> 小组件: https://api.kurobbs.com/gamer/widget/game3/getData
> 小组件: https://api.kurobbs.com/gamer/widget/game3/refresh 两接口地址的请求参数与返回内容相同，但refresh返回的数据更准确点

## 请求方式

POST

## 认证方式

token

## 请求头

注意请求头有两套, 此处为库街区内`角色信息`页面的参数, 类似浏览器环境, 用于更新小组件的请求头请看 [参数总结](/PARAMS.md) 中的例子

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

字符串拼接, 注意两套请求也有不同

| 字段     | 类型 | 内容        | 备注                                                         |
| -------- | ---- | ----------- | ------------------------------------------------------------ |
| gameId   | num  | 游戏 id     | 仅库街区页面内请求携带, 固定 鸣潮 = 3, 但不校验, 不必须      |
| roleId   | num  | 游戏角色 id | 仅库街区页面内请求携带, 需要同时携带正确的 `serverId`<br />不携带 `serverId` 将返回默认角色数据, `serverId` 错误将返回全 `null` 数据<br />`roleId`不存在或者未绑定或者错误都会返回 code = 6001, msg = 暂无数据，\n请漂泊者绑定角色后查看。 |
| serverId | num  | 游戏区服 id | 仅库街区页面内请求携带, 不携带则返回默认角色数据<br />国服 = 76402e5b20be2c39f095a152090afddc, 国际服每个区服都不一样未记录 |
| type     | num  | ?           | 库街区内为 2, 更新卡片为 1, 不校验, 不必须                   |
| sizeType | num  | ?           | 库街区内为 1, 更新卡片为 2, 不校验, 不必须                   |

## 响应体

json, 两个渠道响应完全一致

注意库洛的傻逼服务器有时候返回的时间可能不对, 此时请根据 `data.serverTime` 推算其他时间戳

### 根对象

| 字段    | 类型 | 内容       | 备注                           |
| ------- | ---- | ---------- | ------------------------------ |
| code    | num  | 返回值     | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息   | 请求成功                       |
| success | bool | true/false | token 有效时才有               |
| data    | arr  | 详细信息   | 详细数据, 或者 null            |

### `data`成员对象

| 字段                | 类型     | 内容                              | 备注                                                         |
| ------------------- | -------- | --------------------------------- | ------------------------------------------------------------ |
| gameId              | num      | 游戏 id                           | 固定 鸣潮 = 3                                                |
| userId              | num      | 库街区 id                         | 10065669                                                     |
| serverTime          | num      | 十位数服务器时间戳                | 1719475203                                                   |
| serverId            | str      | 服务器 id                         | 国服 = 76402e5b20be2c39f095a152090afddc, 国际服每个区服都不一样未记录 |
| serverName          | str      | 服务器名称                        | 鸣潮                                                         |
| signInUrl           | str/null | 签到页面链接, 已完成签到就是 null | `https://web-static.kurobbs.com/events2.0/index.html#/mc-month-sign/home` |
| signInTxt           | str      | 签到提示                          | 已完成签到/前往签到                                          |
| hasSignIn           | bool     | 是否已签到                        | true/false                                                   |
| roleId              | str      | 角色 id                           | 101812955                                                    |
| roleName            | str      | 角色昵称                          | 首席                                                         |
| energyData          | obj      | 结晶波片数据                      | 这几个对象结构一致                                           |
| livenessData        | obj      | 每日活跃数据                      | 这几个对象结构一致                                           |
| storeEnergyData     | obj      | 结晶单质                         | 这几个对象结构一致                                           |
| towerData           | obj      | 逆境深塔·深境区                   | 这几个对象结构一致                                           |
| slashTowerData      | obj      | 冥歌海墟·禁忌海域                  | 这几个对象结构一致                                           |
| weeklyData          | obj      | 战歌重奏                          | 这几个对象结构一致                                           |
| weeklyRougeData     | obj      | 千道门扉的异想                     | 这几个对象结构一致                                           |
| battlePassData      | arr      | 其他经验数据                      | 这个数组对象和上面几个对象结构一致                           |
| actionRecoverSwitch | bool     | 角色昵称                          | 首席                                                         |


### `energyData` `livenessData` 对象 `battlePassData` 数组成员对象

| 字段             | 类型     | 内容       | 备注                                                         |
| ---------------- | -------- | ---------- | ------------------------------------------------------------ |
| name             | str      | 名称       | 结晶波片/活跃度...见下方示例数据                             |
| img              | str      | 图标链接   | https://web-static.kurobbs.com/gamerdata/widget/game3/energy.png...见下方示例数据 |
| key              | str/null | 单位       | 暂时均为 null                                                |
| refreshTimeStamp | num/null | 十位时间戳 | 波片回满时间戳, 其他均为 null                                |
| expireTimeStamp  | num/null | 十位时间戳 | 资源过期时间戳, 暂时均为 null                                |
| value            | null     | 值         | null                                                         |
| status           | num      | 状态       | 暂时均为 0                                                   |
| cur              | num      | 当前数量   | 146                                                          |
| total            | num      | 最大数量   | 240                                                          |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/gamer/widget/game3/getData'
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
formData.append('sizeType', 1)
formData.append('type', 2)
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
    "gameId": 3,
    "userId": 10065669,
    "serverTime": 1719475326,
    "serverId": "76402e5b20be2c39f095a152090afddc",
    "serverName": "鸣潮",
    "signInUrl": null,
    "signInTxt": "已完成签到",
    "hasSignIn": true,
    "roleId": "101812955",
    "roleName": "首席",
    "energyData": {
      "name": "结晶波片",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/energy.png",
      "key": null,
      "refreshTimeStamp": 1719508373,
      "expireTimeStamp": null,
      "value": null,
      "status": 0,
      "cur": 146,
      "total": 240
    },
    "livenessData": {
      "name": "活跃度",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/liveness.png",
      "key": null,
      "refreshTimeStamp": null,
      "expireTimeStamp": null,
      "value": null,
      "status": 0,
      "cur": 100,
      "total": 100
    },
    "battlePassData": [
      {
        "name": "电台等级",
        "img": null,
        "key": null,
        "refreshTimeStamp": null,
        "expireTimeStamp": null,
        "value": null,
        "status": 0,
        "cur": 0,
        "total": 0
      },
      {
        "name": "本周经验",
        "img": null,
        "key": null,
        "refreshTimeStamp": null,
        "expireTimeStamp": null,
        "value": null,
        "status": 0,
        "cur": 0,
        "total": 0
      }
    ],
    "storeEnergyData": {
      "name": "结晶单质",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/storeEnergy.png",
      "key": null,
      "value": null,
      "status": 0,
      "cur": 345,
      "total": 480,
      "refreshTimeStamp": 0,
      "timePreDesc": null,
      "expireTimeStamp": 0
    },
    "towerData": {
      "name": "逆境深塔·深境区",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/tower.png",
      "key": null,
      "value": null,
      "status": 0,
      "cur": 12,
      "total": 36,
      "refreshTimeStamp": 1762718400,
      "timePreDesc": "深境区",
      "expireTimeStamp": 0
    },
    "slashTowerData": {
      "name": "冥歌海墟·禁忌海域",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/slashTower.png",
      "key": null,
      "value": "奖励进度：暂无数据",
      "status": 1,
      "cur": 0,
      "total": 0,
      "refreshTimeStamp": 1761508800,
      "timePreDesc": "再生海域",
      "expireTimeStamp": 0
    },
    "weeklyData": {
      "name": "战歌重奏",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/weekly.png",
      "key": null,
      "value": null,
      "status": 0,
      "cur": 0,
      "total": 3,
      "refreshTimeStamp": 0,
      "timePreDesc": null,
      "expireTimeStamp": 0
    },
    "weeklyRougeData": {
      "name": "千道门扉的异想",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game3/weekly.png",
      "key": null,
      "value": null,
      "status": 0,
      "cur": 6000,
      "total": 6000,
      "refreshTimeStamp": 0,
      "timePreDesc": null,
      "expireTimeStamp": 0
    }
  },
  "success": true
}
```