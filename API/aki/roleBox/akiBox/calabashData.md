# [新] 鸣潮游戏角色声骸收集数据

包含 `数据坞信息` 和 `声骸收集进度`

更新时间: 2025.05.25

### 请求地址

> https://api.kurobbs.com/aki/roleBox/akiBox/calabashData

### 请求方式

POST

### 认证方式

token

### 请求头(最简)

| 字段      | 类型  | 内容 | 备注                                         |
|---------|-----|----|--------------------------------------------|
| source  | str | 平台 | android                                    |
| token   | str | 令牌 | 从[验证码登录 APP 端](../../../user/sdkLogin.md)获取 |
| devCode | str | 自定 | 随机生成即可                                     |

### 请求体

| 字段     | 类型 | 内容      | 备注                                             |
| -------- | ---- |---------|------------------------------------------------|
| gameId   | num  | 游戏 id   | 固定 鸣潮 = 3                                      |
| roleId   | num  | 游戏角色 id | 从[取账号绑定的游戏账号信息](../../../gamer/role/list.md)获取 |
| serverId | num  | 游戏区服 id | 从[取账号绑定的游戏账号信息](../../../gamer/role/list.md)获取 |
| channelId | num  | 渠道 id   | 已知为 **19**                                     |
| countryCode | num  | 国家 id   | 隍陇=1<br/>黑海岸=900<br/>黎那汐塔=3                    |

### 响应体

#### 类型：JSON

| 字段    | 类型                      | 内容 | 备注                         |
| ------- |-------------------------|----|----------------------------|
| code    | num                     | 响应码 | 220: token 失效<br />200: 成功 |
| msg     | str                     | 信息 |                            |
| success | bool                    | true | token 有效时才有                |
| data    | **str** | 详细信息 | **此项为字符串类型的JSON**          |


### `data`解析后的结构

| 字段    | 类型   | 内容    | 备注        |
| ------- |------|-------|-----------|
| baseCatch    | str  | 基础捕获率 | 百分比字符串    |
| catchQuality    | num  | 可捕获品质 |           |
| cost    | num  | 总可用费用 |           |
| isUnlock    | bool | 是否解锁  |           |
| level    | num  | 数据坞等级 |           |
| maxCount    | num  | 声骇总数量 |           |
| phantomList    | arr  | 声骇列表  | Phantom结构 |
| strengthenCatch    | str  | 强力捕获率 | 百分比字符串    |
| unlockCount    | num  | 声骇解锁数量  |           |

### `Phantom`结构

| 字段    | 类型  | 内容 | 备注             |
| ------- |-----|----|----------------|
| maxStar    | num | 最大星级 |                |
| phantom    | obj | 声骇数据 | InnerPhantom结构 |
| star    | num | 星级 |  |

### `InnerPhantom`结构

| 字段      | 类型  | 内容       | 备注          |
|---------|-----|----------|-------------|
| acronym | str | 名称简写     | 每个字拼音的第一个字母组成 |
| cost    | num | 费用       |             |
| iconUrl    | str | 声骇大头照Url |             |
| name    | str | 声骇名称     |             |
| phantomId    | num | 声骇 id    | long        |

### 响应预览(数据已脱敏)

```
 数据过多，不展示
```