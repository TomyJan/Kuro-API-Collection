# 战双小组件数据

注意这里同一个 API 有两套请求参数, 分别用于库街区内`角色信息`页面和桌面小组件数据更新, 但是响应参数一致, 下文都有说明

更新时间: 2025.01.13

## 请求地址

> ~~库街区内: https://event.kurobbs.com/gamer/widget/game2/getData~~ 又改回去了
> 小组件: https://api.kurobbs.com/gamer/widget/game2/getData

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
| gameId   | num  | 游戏 id     | 固定 战双 = 2, 但不校验, 不必须                              |
| roleId   | num  | 游戏角色 id | 仅库街区页面内请求携带, 需要同时携带正确的 `serverId`<br />不携带 `serverId` 将返回默认角色数据, `serverId` 错误将返回全 `null` 数据<br />`roleId`不存在或者未绑定或者错误都会返回 code = 6001, msg = 指挥官还没有设置角色哦~\n请点击打开库街区App在【我的】页面中设置角色后再进行查看~ |
| serverId | num  | 游戏区服 id | 仅库街区页面内请求携带, 不携带则返回默认角色数据<br />星火服 = 1000, 信标服 = ? |
| type     | num  | ?           | 库街区内为 2, 更新卡片为 1, 不校验, 不必须                   |
| sizeType | num  | ?           | 仅更新卡片请求携带, 1, 不校验, 不必须                        |

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
| gameId              | num      | 游戏 id                           | 固定 战双 = 2                                                |
| userId              | num      | 库街区 id                         | 10065669                                                     |
| serverTime          | num      | 十位数服务器时间戳                | 1719475203                                                   |
| serverId            | str      | 服务器 id                         | 星火服 = 1000, 信标服 = ?                                    |
| serverName          | str      | 服务器名称                        | 星火服/信标服                                                |
| signInUrl           | str/null | 签到页面链接, 已完成签到就是 null | `https://web-static.kurobbs.com/events2.0/index.html#/zs-month-sign/home` |
| signInTxt           | str      | 签到提示                          | 已领取每日补给/前往签到                                      |
| hasSignIn           | bool     | 是否已签到                        | true/false                                                   |
| roleId              | str      | 角色 id                           | 46218962                                                     |
| roleName            | str      | 角色昵称                          | TomyJan                                                      |
| actionData          | obj      | 血清数据                          | 这几个对象结构一致                                           |
| dormData            | obj      | 宿舍委托数据                      | 这几个对象结构一致                                           |
| activeData          | obj      | 每日活跃数据                      | 这几个对象结构一致                                           |
| bossData            | arr      | 其他副本战数据                    | 这个数组对象和上面几个对象结构一致                           |
| actionRecoverSwitch | bool     | 角色昵称                          | 首席                                                         |


### `actionData` `dormData` `activeData` 对象 `bossData` 数组成员对象

| 字段             | 类型     | 内容       | 备注                                                         |
| ---------------- | -------- | ---------- | ------------------------------------------------------------ |
| name             | str/null | 名称       | 血清/委托情况...见下方示例数据                               |
| img              | str      | 图标链接   | https://web-static.kurobbs.com/gamerdata/widget/game2/actionIcon.png...见下方示例数据 |
| key              | str/null | 单位       | null/血清/黑卡...见下方示例数据                              |
| refreshTimeStamp | num/null | 十位时间戳 | 血清回满/副本刷新时间戳, 恢复后为0                           |
| expireTimeStamp  | num/null | 十位时间戳 | 资源过期时间戳, 血清好像固定为次月 1日 5 点, 恢复后为0, 其他均为 null |
| value            | str/null | 值         | 未选区/未解锁/`145/240`                                      |
| status           | num      | 状态       | 0 = 恢复中, 1 = 未解锁, 2 = 未选区                           |
| cur              | num      | 当前数量   | 145                                                          |
| total            | num      | 最大数量   | 240                                                          |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/gamer/widget/game2/getData'
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
formData.append('gameId', 2)
formData.append('roleId', '46218962')
formData.append('serverId', '1000')
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
    "gameId": 2,
    "userId": 10065669,
    "serverTime": 1719475203,
    "serverId": "1000",
    "serverName": "星火服",
    "signInUrl": null,
    "signInTxt": "已领取每日补给",
    "hasSignIn": true,
    "roleId": "46218962",
    "roleName": "TomyJan",
    "actionData": {
      "name": "血清",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/actionIcon.png",
      "key": null,
      "refreshTimeStamp": 1719509303,
      "expireTimeStamp": 1719781200,
      "value": "145/240",
      "status": 0,
      "cur": 145,
      "total": 240
    },
    "dormData": {
      "name": "委托情况",
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/dormIcon.png",
      "key": null,
      "refreshTimeStamp": null,
      "expireTimeStamp": null,
      "value": null,
      "status": 0,
      "cur": 8,
      "total": 8
    },
    "activeData": {
      "name": null,
      "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/activeIcon.png",
      "key": "每日活跃",
      "refreshTimeStamp": null,
      "expireTimeStamp": null,
      "value": "0/100",
      "status": 0,
      "cur": 0,
      "total": 100
    },
    "bossData": [
      {
        "name": "幻痛囚笼",
        "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/bossIcon.png",
        "key": "黑卡",
        "refreshTimeStamp": null,
        "expireTimeStamp": null,
        "value": "未选区",
        "status": 2,
        "cur": 0,
        "total": 0
      },
      {
        "name": "历战映射",
        "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/transfiniteIcon.png",
        "key": "算符",
        "refreshTimeStamp": 1720062000,
        "expireTimeStamp": null,
        "value": "0/1500",
        "status": 0,
        "cur": 0,
        "total": 1500
      },
      {
        "name": "纷争战区",
        "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/arenaIcon.png",
        "key": "黑卡",
        "refreshTimeStamp": 1719741600,
        "expireTimeStamp": null,
        "value": "600/600",
        "status": 0,
        "cur": 600,
        "total": 600
      },
      {
        "name": "诺曼矿区",
        "img": "https://web-static.kurobbs.com/gamerdata/widget/game2/strongHoldIcon.png",
        "key": "关卡",
        "refreshTimeStamp": 1720665000,
        "expireTimeStamp": null,
        "value": "0/18",
        "status": 0,
        "cur": 0,
        "total": 18
      }
    ],
    "actionRecoverSwitch": true
  },
  "success": true
}
```