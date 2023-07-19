# 取个人信息 V2

## 请求地址

> https://api.kurobbs.com/user/mineV2

## 请求方式
POST

## 认证方式

token + 账号 id

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

| 字段        | 类型 | 内容    | 备注                             |
| ----------- | ---- | ------- | -------------------------------- |
| otherUserId | num  | 账号 id |                                  |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 |                                |
| success | bool | true     | token 有效时才有               |
| data    | obj  | 详细信息 | 成功时才有                     |

### `data`对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| mine    | obj  | 个人信息         |                                                             |

### `mine`对象

| 字段      | 类型 | 内容         | 备注                                                         |
| --------- | ---- | ------------ | ------------------------------------------------------------ |
| collectCount | num  | (?)      | 0 |
| commentCount | num | 评论数       |                                      |
| fansCount | num | 粉丝数 |  |
| fansNewCount | num | 新增粉丝数 |  |
| followCount | num | 关注数     |    |
| gender | num | (?) | 3 |
| goldNum | num | (?) | 0 |
| headUrl | num | 头像图片链接 | https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadLuolannew.png |
| ifCompleteQuiz | num | (?)   | 1 |
| isFollow | num | (?)   | 0 |
| isLoginUser | num | (?) | 1 |
| isMute | num | (?) | 0 |
| levelTotal | num | (?) | 0 |
| likeCount | num | (?) | 0 |
| medalList | arr | (?) | 空的 |
| mobile | num | 打码的手机号 | 188****8888 |
| postCount | num | (?) | 0 |
| registerTime | num | 注册日期 | 2023.07.16 |
| signature | num | 签名 | 这个人很懒，还没有签名。 |
| signatureReviewStatus | num | (?) | 1 |
| status | num | (?) | 0 |
| userId | num | 账号 id | 10065669 |
| userName | num | 昵称 |  |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/user/mineV2'
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
formData.append('otherUserId', 12345678)
try {
    const response = await fetch(url, {
        method: 'POST',
        headers: headers,
        body: formData,
    })

    if (!response.ok) {
        throw new Error('fetch error: ' + response.status)
    }

    const rsp = await response.json()

    if (rsp.code === 200) {
        console.info('fetch rsp:', JSON.stringify(rsp));
    } else {
        console.error('fetch error:', JSON.stringify(rsp));
    }
} catch (error) {
    console.error('fetch error:', error);
}
```

### 响应

```json
{
  code: 200,
  data: {
    gender: 3,
    signature: '这个人很懒，还没有签名。',
    headUrl: '{
    "code": 200,
    "data": {
        "mine": {
            "collectCount": 0,
            "commentCount": 0,
            "fansCount": 0,
            "fansNewCount": 0,
            "followCount": 0,
            "gender": 3,
            "goldNum": 0,
            "headUrl": "https://prod-alicdn-community.kurobbs.com/headCode/RoleHeadLuolannew.png",
            "ifCompleteQuiz": 1,
            "isFollow": 0,
            "isLoginUser": 1,
            "isMute": 0,
            "levelTotal": 0,
            "likeCount": 0,
            "medalList": [
            ],
            "mobile": "188****8888",
            "postCount": 0,
            "registerTime": "2023.07.16",
            "signature": "这个人很懒，还没有签名。",
            "signatureReviewStatus": 1,
            "status": 0,
            "userId": "10065669",
            "userName": "TomyJan"
        }
    },
    "msg": "请求成功",
    "success": true
}
```
