# [新] 鸣潮游戏角色探索数据

更新时间: 2025.05.25

### 请求地址

> https://api.kurobbs.com/aki/roleBox/akiBox/exploreIndex

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

| 字段    | 类型   | 内容     | 备注                                    |
| ------- |------|--------|---------------------------------------|
| detectionInfoList    | arr  | 声骇探寻信息 | DetectionInfo结构                                      |
| exploreList    | arr  | 探索信息   | Explore结构                                      |
| open    | bool | 对外展示   |                                       |

### `DetectionInfo`结构

| 字段    | 类型  | 内容     | 备注          |
| ------- |-----|--------|-------------|
| acronym    | str | 名称简写   | 每个字拼音的第一个字母组成 |
| detectionIcon    | str | 图标Url  |             |
| detectionId    | num | 声骇 id  | long        |
| detectionName    | str | 名称     |         |
| level    | num | 声骇品质   |         |
| levelName    | str | 声骇品质名称 |         |

### `Explore`结构

| 字段    | 类型  | 内容     | 备注           |
| ------- |-----|--------|--------------|
| areaInfoList    | arr | 地区信息   | AreaInfo结构   |
| country    | obj | 国家信息   | Country结构    |
| countryProgress    | str | 国家总探索度 | 字符串包裹的float值 |

### `AreaInfo`结构

| 字段    | 类型  | 内容      | 备注     |
| ------- |-----|---------|--------|
| areaId    | num | 地区 id   |        |
| areaName    | str | 地图名称    |        |
| areaPic    | str | 地区预览图Url |        |
| areaProgress    | num | 地区探索度   | float  |
| itemList    | arr | 探索物进度     | Item结构 |

### `Item`结构

| 字段    | 类型  | 内容    | 备注                                                                                                                                                                                                                                                                                                                                                          |
| ------- |-----|-------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| icon    | str | 图标Url |                                                                                                                                                                                                                                                                                                                                                             |
| name    | str | 探索物名称 |                                                                                                                                                                                                                                                                                                                                                             |
| progress    | num | 探索进度  | float                                                                                                                                                                                                                                                                                                                                                       |
| type    | num | 类型    | 奇藏=1<br/>信标=2<br/>声匣=3<br/>观景点=4<br/>飞猎手=5<br/>区域任务=6<br/>定风铎=8<br/>伏霜虫=9<br/>约兰的战术测试=11<br/>溢彩画=12<br/>藏宝地=13<br/>巡礼之梦=14<br/>三兄弟挑战=15<br/>全息战略·刀伶之舞=16<br/>音乐飞萤=17<br/>巡礼之梦·梦魇=18<br/>暗影徘徊的遗迹=19<br/>白月？绯月？=20<br/>三重冠塔=21<br/>声骸挑战·幻觉=22<br/>声匣·拉古那=23<br/>残息海岸=24<br/>青栎庭院=25<br/>声骸挑战·刀伶操控=26<br/>飞翼竞速=27<br/>行船竞速=28<br/>闪翼挑战=29<br/> |

### `Country`结构

| 字段    | 类型  | 内容                    | 备注        |
| ------- |-----|-----------------------|-----------|
| bgColor    | str | 背景颜色                  | 十六进制颜色字符串 |
| countryId    | num | 国家 id                 |           |
| countryName    | str | 国家名称                  |           |
| detailPageAreaMaskColor    | str | 详细信息页面区域蒙版颜色          | 十六进制颜色字符串     |
| detailPageAreaPic    | str | 详情页面区域图片Url(指南针)      |     |
| detailPageDarkColor    | str | 详细信息页面深色              | 十六进制颜色字符串     |
| detailPageFontColor    | str | 详细信息页面字体颜色            | 十六进制颜色字符串    |
| detailPageImage    | str | 详情页面图片Url(国家图标，样式A)   |     |
| detailPageLightColor    | str | 详细信息页面浅色              | 十六进制颜色字符串    |
| detailPagePic    | str | 详细信息页面图片Url(带国家图标的名片) |     |
| detailPageProgressColor    | str | 详细页面进度颜色              | 十六进制颜色字符串    |
| homePageIcon    | str | 主页页面图片Url(国家图标，样式B)   |     |
| homePageImage    | str | 主页页面图片Url(国家图标，样式C)   |     |


### 响应预览(数据已脱敏)

```
 数据过多，不展示
```