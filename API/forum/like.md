# 通用论坛点赞

## 请求地址

> https://api.kurobbs.com/forum/like

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段            | 类型 | 内容  | 备注                                 |
| --------------- | ---- | ----- | ------------------------------------ |
| osversion       | str  | -     | Android                              |
| devcode         | str  | -     | 2fba3859fe9bfe9099f2696b8648c2c6     |
| distinct_id     | str  | -     | 765485e7-30ce-4496-9a9c-a2ac1c03c02c |
| countrycode     | str  | -     | CN                                   |
| ip              | str  |       | 10.0.2.233                           |
| model           | str  |       | 2211133C                             |
| source          | str  |       | android                              |
| lang            | str  |       | zh-Hans                              |
| version         | str  |       | 1.0.9                                |
| versioncode     | str  |       | 1090                                 |
| token           | str  | token |                                      |
| content-type    | str  |       | application/x-www-form-urlencoded    |
| accept-encoding | str  |       | gzip                                 |
| user-agent      | str  |       | okhttp/3.10.0                        |

## 请求体

字符串拼接

| 字段     | 类型 | 内容     | 备注                                                         |
| -------- | ---- | -------- | ------------------------------------------------------------ |
| forumId  | num  | 板块 id  | 战双 推荐=2, 伊甸闲庭=3, 攻略=4, 同人=5<br />鸣潮 推荐=9, 天诚茶馆=10, 同人=11 |
| gameId   | num  | 游戏 id  | 战双 = 2, 鸣潮 = 3                                           |
| likeType | num  | 点赞类型 | 点赞帖子 = 1, 评论 = 2, 楼中楼 = 3          |
| operateType | num  | 点赞操作 | 点赞 = 1, 取消 = 2                             |
| postCommentId | num  | 评论 id | 0, 点赞评论/楼中楼时为评论 id             |
| postCommentReplyId | num  | 楼中楼 id | 0, 点赞楼中楼时为楼中楼 id                        |
| postId | num  | 帖子 id | 1133555470924988416                        |
| postType | num  | (?) | 1                                           |
| toUserId | num  | 点赞对象的发布者 id | 10065669                                   |

## 响应体

json, 即使重复点赞返回也固定

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 | 请求成功                       |
| success | bool | true     | token 有效时才有               |
| data    | obj  | 返回数据 | 成功时才有                     |

### `data` 对象

| 字段    | 类型 | 内容 | 备注 |
| ------- | ---- | ---- | ---- |
| success | bool | true |      |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/forum/like'
const headers = {
    osversion: 'Android',
    devcode: '2fba3859fe9bfe9099f2696b8648c2c6',
    distinct_id: '765485e7-30ce-4496-9a9c-a2ac1c03c02c',
    countrycode: 'CN',
    ip: '10.0.2.233',
    model: '2211133C',
    source: 'android',
    lang: 'zh-Hans',
    version: '1.0.9',
    versioncode: '1090',
    token: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'content-type': 'application/x-www-form-urlencoded',
    'accept-encoding': 'gzip',
    'user-agent': 'okhttp/3.10.0',
}

const formData = new URLSearchParams()
formData.append('forumId', 3)
formData.append('gameId', 2)
formData.append('likeType', 1)
formData.append('operateType', 1)
formData.append('postCommentId', 0)
formData.append('postCommentReplyId', 0)
formData.append('postId', 1133555470924988416)
formData.append('postType', 1)
formData.append('toUserId', 10065669)
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
    "data": {
        "success": true
    },
    "msg": "请求成功",
    "success": true
}
```