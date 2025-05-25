# [新] 鸣潮游戏角色基础数据

包含 `日常数据` 和 `我的资料`

更新时间: 2025.05.25

### 请求地址

> https://api.kurobbs.com/aki/roleBox/akiBox/baseData

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

| 字段     | 类型 | 内容        | 备注                                             |
| -------- | ---- | ----------- |------------------------------------------------|
| gameId   | num  | 游戏 id     | 固定 鸣潮 = 3                                      |
| roleId   | num  | 游戏角色 id | 从[取账号绑定的游戏账号信息](../../../gamer/role/list.md)获取 |
| serverId | num  | 游戏区服 id | 从[取账号绑定的游戏账号信息](../../../gamer/role/list.md)获取 |

### 响应体

#### 类型：JSON

| 字段    | 类型                      | 内容 | 备注                         |
| ------- |-------------------------|----|----------------------------|
| code    | num                     | 响应码 | 220: token 失效<br />200: 成功 |
| msg     | str                     | 信息 |                            |
| success | bool                    | true | token 有效时才有                |
| data    | **str** | 详细信息 | **此项为字符串类型的JSON**          |


### `data`解析后的结构

| 字段    | 类型   | 内容             | 备注                            |
| ------- |------|----------------|-------------------------------|
| achievementCount    | num  | 成就数量           |                               |
| achievementStar    | num  | 成就总星数          |                               |
| activeDays    | num  | 活跃天数           |                               |
| bigCount    | num  | 中型信标解锁数        |                               |
| boxList    | arr  | 宝箱列表           | Box结构                         |
| chapterId    | num  | 未知             |                               |
| creatTime    | num  | 账号创建事件         | 时间戳<br/>官方返回的字段名打错了？少了个e      |
| energy    | num  | 结晶波片           |                               |
| id    | num  | 账号Id           |                               |
| level    | num  | 账号等级           |                               |
| liveness    | num  | 活跃度            |                               |
| livenessMaxCount    | num  | 活跃度上限          |                               |
| livenessUnlock    | bool | 解锁活跃系统         |                               |
| maxEnergy    | num  | 结晶波片最大值        |                               |
| name    | str  | 账号名称           |                               |
| phantomBoxList    | arr  | 潮汐之遗           | Box结构                         |
| roleNum    | num  | 角色数量           |                               |
| rougeIconUrl    | str  | 肉鸽图标Url        |                               |
| rougeScore    | num  | 当期肉鸽分数         |                               |
| rougeScoreLimit    | num  | 肉鸽上限分数         |                               |
| rougeTitle    | str  | 当期肉鸽名称         |                               |
| showToGuest    | bool | 对外展示           |                               |
| smallCount    | num  | 小型信标解锁数        |                               |
| storeEnergy    | num  | 结晶单质           |                               |
| storeEnergyIconUrl    | str  | 结晶单质图标Url      |                               |
| storeEnergyLimit    | num  | 结晶单质上限         |                               |
| storeEnergyTitle    | str  | 结晶单质标题         |                               |
| treasureBoxList    | arr  | 宝箱列表           | Box结构<br/>不知道为什么这个和上面的宝箱数量不一致 |
| weeklyInstCount    | num  | 潮汐重奏(周本)收取次数   |                               |
| weeklyInstCountLimit    | num  | 潮汐重奏(周本)收取次数上限 |                               |
| weeklyInstIconUrl    | str  | 潮汐重奏(周本)图标Url  |                               |
| weeklyInstTitle    | str  | 潮汐重奏(周本)标题     |                               |
| worldLevel    | num  | 世界等级           |                               |

### `Box`结构

| 字段    | 类型  | 内容   | 备注                                    |
| ------- |-----|------|---------------------------------------|
| boxName    | str | 名称   |                                       |
| num    | num | 数量   |                                       |

### 响应预览(数据已脱敏)

```json
{
  "code": 200,
  "msg": "请求成功",
  "data": "{\"achievementCount\":0,\"achievementStar\":0,\"activeDays\":0,\"bigCount\":0,\"boxList\":[{\"boxName\":\"朴素奇藏箱\",\"num\":0},{\"boxName\":\"基准奇藏箱\",\"num\":0},{\"boxName\":\"精密奇藏箱\",\"num\":0},{\"boxName\":\"辉光奇藏箱\",\"num\":0}],\"chapterId\":0,\"creatTime\":100000000000,\"energy\":0,\"id\":100000000,\"level\":0,\"liveness\":0,\"livenessMaxCount\":0,\"livenessUnlock\":true,\"maxEnergy\":0,\"name\":\"匿名\",\"phantomBoxList\":[{\"name\":\"潮汐之遗·绿\",\"num\":0},{\"name\":\"潮汐之遗·紫\",\"num\":0},{\"name\":\"潮汐之遗·金\",\"num\":0}],\"roleNum\":0,\"rougeIconUrl\":\"xxxxx\",\"rougeScore\":0,\"rougeScoreLimit\":6000,\"rougeTitle\":\"千道门扉的异想\",\"showToGuest\":true,\"smallCount\":0,\"storeEnergy\":0,\"storeEnergyIconUrl\":\"https://web-static.kurobbs.com/gamerdata/widget/game3/storeEnergy.png\",\"storeEnergyLimit\":480,\"storeEnergyTitle\":\"结晶单质\",\"treasureBoxList\":[{\"name\":\"朴素奇藏箱\",\"num\":0},{\"name\":\"基准奇藏箱\",\"num\":0},{\"name\":\"精密奇藏箱\",\"num\":0},{\"name\":\"辉光奇藏箱\",\"num\":0}],\"weeklyInstCount\":0,\"weeklyInstCountLimit\":3,\"weeklyInstIconUrl\":\"https://web-static.kurobbs.com/gamerdata/widget/game3/weeklyInst.png\",\"weeklyInstTitle\":\"战歌重奏收取次数\",\"worldLevel\":0}",
  "success": true
}
```

