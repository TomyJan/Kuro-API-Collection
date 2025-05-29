# 鸣潮获取资源统计索引

更新时间: 2025.05.29

### 请求地址

> https://api.kurobbs.com/aki/resource/period/list

### 请求方式

GET

### 认证方式

token

### 请求头(最简)

| 字段      | 类型  | 内容 | 备注                                         |
|---------|-----|----|--------------------------------------------|
| source  | str | 平台 | android                                    |
| token   | str | 令牌 | 从[验证码登录 APP 端](../../../user/sdkLogin.md)获取 |
| devCode | str | 自定 | 随机生成即可                                     |

### 请求体

无

### 响应体

#### 类型：JSON

| 字段    | 类型   | 内容 | 备注                         |
| ------- |------|----|----------------------------|
| code    | num  | 响应码 | 220: token 失效<br />200: 成功 |
| msg     | str  | 信息 |                            |
| success | bool | true | token 有效时才有                |
| data    | obj    | 详细信息 | Data结构                     |


### `Data`结构

| 字段    | 类型  | 内容 | 备注      |
| ------- |-----|----|---------|
| weeks    | obj | 周  | Index结构 |
| months    | obj | 月  | Index结构        |
| versions    | obj | 版本 | Index结构        |

### `Index`结构

| 字段     | 类型  | 内容   | 备注  |
|--------|-----|------|-----|
| title  | str | 标题   |  |
| index | num | 索引Id |     |

### 响应预览(数据已脱敏)

```json
{
  "code":200,
  "msg":"请求成功",
  "data":{
    "weeks":[
      {
        "title":"4月28日~5月4日",
        "index":202518
      },
      {
        "title":"5月5日~5月11日",
        "index":202519
      },
      {
        "title":"5月12日~5月18日",
        "index":202520
      },
      {
        "title":"5月19日~5月25日",
        "index":202521
      },
      {
        "title":"5月26日~6月1日",
        "index":202522
      }
    ],
    "months":[
      {
        "title":"3月",
        "index":202503
      },
      {
        "title":"4月",
        "index":202504
      },
      {
        "title":"5月",
        "index":202505
      }
    ],
    "versions":[
      {
        "title":"2.3版本",
        "index":20300
      },
      {
        "title":"2.2版本",
        "index":20200
      }
    ]
  },
  "success":true
}
```