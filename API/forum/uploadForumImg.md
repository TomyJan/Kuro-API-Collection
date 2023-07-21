# 图片上传

## 请求地址

> https://api.kurobbs.com/forum/uploadForumImg

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段            | 类型 | 内容  | 备注                                                         |
| --------------- | ---- | ----- | ------------------------------------------------------------ |
| osversion       | str  | -     | Android                                                      |
| devcode         | str  | -     | 2fba3859fe9bfe9099f2696b8648c2c6                             |
| distinct_id     | str  | -     | 765485e7-30ce-4496-9a9c-a2ac1c03c02c                         |
| countrycode     | str  | -     | CN                                                           |
| ip              | str  |       | 10.0.2.233                                                   |
| model           | str  |       | 2211133C                                                     |
| source          | str  |       | android                                                      |
| lang            | str  |       | zh-Hans                                                      |
| version         | str  |       | 1.0.9                                                        |
| versioncode     | str  |       | 1090                                                         |
| token           | str  | token |                                                              |
| content-type    | str  |       | multipart/form-data; boundary=48dc8243-9106-4152-b8d7-27a3aa6cdddd (随机生成) |
| accept-encoding | str  |       | gzip                                                         |
| user-agent      | str  |       | okhttp/3.10.0                                                |

## 请求体

formData, 注意 name 应该固定为 `files` 

## 响应体

json

| 字段    | 类型 | 内容     | 备注                                                         |
| ------- | ---- | -------- | ------------------------------------------------------------ |
| code    | num  | 返回值   | 10000: 没有图片<br />500: 系统异常 ( formData 有问题)<br />220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息 | 请求成功/用户登录已过期/系统异常/请上传图片                  |
| success | bool | true     | token 有效时才有                                             |
| data    | arr  | 图片直链 | 成功时才有                                                   |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/forum/uploadForumImg'
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
    'accept-encoding': 'gzip',
    'user-agent': 'okhttp/3.10.0',
}

const formData = new FormData()
formData.append('files',fs.createReadStream('D:\\1689782876324145905.jpg'))
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
    "code": 200,
    "data": [
        "https://prod-alicdn-community.kurobbs.com/forum/1689790109125345304.jpg"
    ],
    "msg": "请求成功",
    "success": true
}
```