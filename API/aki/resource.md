# 鸣潮获取账号资源统计

更新时间: 2025.05.29

### 请求地址

> **周**: https://api.kurobbs.com/aki/resource/week  
> **月**: https://api.kurobbs.com/aki/resource/month  
> **版本**: https://api.kurobbs.com/aki/resource/version

### 请求方式

POST

### 认证方式

token

### 请求头(最简)

| 字段      | 类型  | 内容 | 备注                                    |
|---------|-----|----|---------------------------------------|
| source  | str | 平台 | android                               |
| token   | str | 令牌 | 从[验证码登录 APP 端](../user/sdkLogin.md)获取 |
| devCode | str | 自定 | 随机生成即可                                |

### 请求体

| 字段     | 类型  | 内容      | 备注                                       |
| -------- |-----|---------|------------------------------------------|
| period   | num | 索引 id   | 从[鸣潮获取资源统计索引](./resource/period/list.md)获取 |
| roleId   | num | 游戏角色 id | 从[取账号绑定的游戏账号信息](../gamer/role/list.md)获取 |
| serverId | str | 游戏区服 id | 从[取账号绑定的游戏账号信息](../gamer/role/list.md)获取  |

### 响应体

#### 类型：JSON

| 字段    | 类型   | 内容 | 备注                         |
| ------- |------|----|----------------------------|
| code    | num  | 响应码 | 220: token 失效<br />200: 成功 |
| msg     | str  | 信息 |                            |
| success | bool | true | token 有效时才有                |
| data    | obj  | 详细信息 | Data结构                     |


### `Data`结构

| 字段    | 类型  | 内容     | 备注          |
| ------- |-----|--------|-------------|
| totalCoin    | num | 总计贝币   |             |
| totalStar    | num | 总计星声   |             |
| coinList    | arr | 贝币获取来源 | Source结构    |
| starList    | arr | 星声获取来源 | Source结构    |
| coinInc    | ?   | 未知     |             |
| starInc    | ?   | 未知     |             |
| copyWriting    | str | 提示文本   |             |
| recommend    | obj | 推荐帖子   | Recommend结构 |

### `Source`结构

| 字段   | 类型  | 内容 | 备注          |
|------|-----|----|-------------|
| type | str | 类型 |             |
| num  | num | 数量 |             |

### `Recommend`结构

| 字段    | 类型  | 内容     | 备注        |
| ------- |-----|--------|-----------|
| postId    | str | 帖子Id   |           |
| postTitle    | str | 帖子标题 | 省略版          |
| content    | str | 帖子内容 | 省略版  |
| picUrl    | str | 封面Url  |   |

### 响应预览(数据已脱敏)

```json
{
  "code":200,
  "msg":"请求成功",
  "data":{
    "totalCoin":0,
    "totalStar":0,
    "coinList":[
      {
        "type":"玩法奖励",
        "num":0
      },
      {
        "type":"活动奖励",
        "num":0
      },
      {
        "type":"日常挑战",
        "num":0
      },
      {
        "type":"任务获取",
        "num":0
      },
      {
        "type":"大世界探索",
        "num":0
      },
      {
        "type":"其他",
        "num":0
      }
    ],
    "starList":[
      {
        "type":"玩法奖励",
        "num":0
      },
      {
        "type":"活动奖励",
        "num":0
      },
      {
        "type":"日常挑战",
        "num":0
      },
      {
        "type":"任务获取",
        "num":0
      },
      {
        "type":"大世界探索",
        "num":0
      },
      {
        "type":"其他",
        "num":0
      }
    ],
    "coinInc":null,
    "starInc":null,
    "copyWriting":"这片大陆的频率，正因你的每一次战斗而重振脉动。",
    "recommend":{
      "postId":"xxxxx",
      "postTitle":"xxxxx",
      "content":"xxxxxx",
      "picUrl":"https://prod-alicdn-community.kurobbs.com/forum/xxxx.png"
    }
  },
  "success":true
}
```

