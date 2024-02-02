# 取任务进度

更新时间: unrecorded

## 请求地址

> https://api.kurobbs.com/encourage/level/getTaskProcess

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

| 字段   | 类型 | 内容    | 备注              |
| ------ | ---- | ------- | ----------------- |
| gameId | num  | 固定为0 | 不是游戏 id, 迷惑 |
| userId | num  | 用户 id | 10065669          |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token<br />失效 200: 成功 |
| msg     | str  | 提示信息 | 请求成功                       |
| success | bool | true     | token 有效时才有               |
| data    | obj  | 详细信息 | 成功时才有                     |

### `data` 对象

| 字段             | 类型 | 内容                   | 备注             |
| ---------------- | ---- | ---------------------- | ---------------- |
| currentDailyGold | num  | 今日已获取库洛币数量   | 0-80             |
| maxDailyGold     | num  | 每日最多获取库洛币数量 | 目前固定为 80   |
| growTask         | arr  | 一次性任务信息         |   |
| dailyTask        | arr  | 每日任务信息           |         |

### `data`中的 `growTask` 和 `dailyTask` 成员对象

| 字段             | 类型 | 内容                   | 备注             |
| ---------------- | ---- | ---------------------- | ---------------- |
| completeTimes | num  | 已完成次数   |              |
| needActionTimes | num  | 最多完成次数 |     |
| process  | num  | 任务进度   | 0.00-1.00 |
| remark  | str  | 任务名称     |         |
| gainGold | num  | 任务奖励库洛币数量 |         |
| skipType | num  | (?)        | 0-6, 和任务的对应关系见 [响应示例](#响应) |
| times   | num  | (?)        | 1 |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/encourage/level/getTaskProcess'
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
formData.append('gameId', 0)
formData.append('userId', 10065669)
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
        "currentDailyGold": 80,
        "growTask": [
            {
                "completeTimes": 1,
                "gainGold": 120,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "修改头像",
                "skipType": 1,
                "times": 1
            },
            {
                "completeTimes": 1,
                "gainGold": 60,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "修改个性签名",
                "skipType": 2,
                "times": 1
            },
            {
                "completeTimes": 1,
                "gainGold": 240,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "关注3名用户",
                "skipType": 3,
                "times": 1
            },
            {
                "completeTimes": 1,
                "gainGold": 200,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "累积社区浏览3分钟",
                "skipType": 4,
                "times": 1
            },
            {
                "completeTimes": 1,
                "gainGold": 80,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "首次兑换奖励",
                "skipType": 5,
                "times": 1
            }
        ],
        "dailyTask": [
            {
                "completeTimes": 1,
                "gainGold": 30,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "用户签到",
                "skipType": 6,
                "times": 1
            },
            {
                "completeTimes": 3,
                "gainGold": 20,
                "needActionTimes": 3,
                "process": 1.00,
                "remark": "浏览3篇帖子",
                "skipType": 0,
                "times": 1
            },
            {
                "completeTimes": 5,
                "gainGold": 20,
                "needActionTimes": 5,
                "process": 1.00,
                "remark": "点赞5次",
                "skipType": 0,
                "times": 1
            },
            {
                "completeTimes": 1,
                "gainGold": 10,
                "needActionTimes": 1,
                "process": 1.00,
                "remark": "分享1次帖子",
                "skipType": 0,
                "times": 1
            }
        ],
        "maxDailyGold": 80
    },
    "msg": "请求成功",
    "success": true
}
```