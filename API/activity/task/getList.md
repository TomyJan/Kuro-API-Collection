# 取活动任务详情

## 请求地址

> https://api.kurobbs.com/activity/task/getList

## 请求方式

POST

## 认证方式

token

## 请求头

| 字段             | 类型 | 内容  | 备注                                                         |
| ---------------- | ---- | ----- | ------------------------------------------------------------ |
| pragma           | str  | -     | no-cache                                                     |
| cache-control    | str  | -     | no-cache                                                     |
| accept           | str  | -     | application/json, text/plain, \*/\*                          |
| source           | str  | -     | android                                                      |
| user-agent       | str  | UA    | Mozilla/5.0 (Linux; Android 13; 2211133C Build/TKQ1.220905.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/114.0.5735.131 Mobile Safari/537.36 Kuro/1.0.9 KuroGameBox/1.0.9 |
| token            | str  | token | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| content-type     | str  |       | application/x-www-form-urlencoded                            |
| origin           | str  |       | https://web-static.kurobbs.com                               |
| x-requested-with | str  |       | com.kurogame.kjq                                             |
| sec-fetch-site   | str  |       | same-site                                                    |
| sec-fetch-mode   | str  |       | cors                                                         |
| sec-fetch-dest   | str  |       | empty                                                        |
| accept-encoding  | str  |       | gzip, deflate, br                                            |
| accept-language  | str  |       | zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7                          |

## 请求体

字符串拼接

| 字段   | 类型 | 内容        | 备注     |
| ------ | ---- | ----------- | -------- |
| userId | num  | 库洛账号 id | 10065669 |

## 响应体

json

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: cookie过期<br />200: 成功 |
| message | str  | 提示信息 | success, 貌似和 msg 一样       |
| msg     | str  | 提示信息 | success                        |
| data    | obj  | 详细信息 | 成功时才有                     |

### `data` 对象

| 字段              | 类型     | 内容                 | 备注 |
| ----------------- | -------- | -------------------- | ---- |
| taskList          | arr      | 活动任务详情列表     |      |
| taskMilestoneList | num/null | 任务积分累计奖励列表 |      |
| currentIntegral   | num/null | 当前积分             | 120  |

### `data` 的 `taskList` 成员对象

| 字段        | 类型 | 内容                       | 备注                                                         |
| ----------- | ---- | -------------------------- | ------------------------------------------------------------ |
| taskId      | str  | 任务 id                    | 六位数字字母                                                 |
| taskName    | str  | 任务名称                   |                                                              |
| taskProcess | num  | 任务进度, 和下面的限制对应 |                                                              |
| taskLimit   | num  | 任务上限                   |                                                              |
| status      | num  | 任务状态                   | 0 = 未完成, 1 = 已完成待领取, 2 = 已领取                     |
| type        | num  | 任务类型                   | 1 = 分享查询类任务, 2 = 游戏类任务, 3 = 关注类任务, 4 = 浏览类任务, 5 = 签到类任务<br />其中 3 和 4 不可通过完成接口完成, 2 不可手动完成 |
| remark      | str  | 任务说明                   |                                                              |

### `data` 的 `taskMilestoneList` 成员对象

| 字段           | 类型 | 内容         | 备注            |
| -------------- | ---- | ------------ | --------------- |
| taskId         | str  | 任务 id      | 同上面的 taskId |
| prizeName      | str  | 奖励名称     |                 |
| prizeType      | num  | 奖励类型(?)  | 1!5!            |
| prizeAmount    | num  | 奖励数量     |                 |
| milestoneCount | num  | 需求积分数量 |                 |
| status         | num  | 任务状态     | 同上面的 status |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/activity/task/getList'
const headers = {
    pragma: 'no-cache',
    'cache-control': 'no-cache',
    accept: 'application/json, text/plain, */*',
    source: 'android',
    'user-agent': 'Mozilla/5.0 (Linux; Android 13; 2211133C Build/TKQ1.220905.001; wv) AppleWebKit/537.36 (KHTML, like Gecko) Version/4.0 Chrome/114.0.5735.131 Mobile Safari/537.36 Kuro/1.0.9 KuroGameBox/1.0.9',
    token: 'eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA',
    'content-type': 'application/x-www-form-urlencoded',
    origin: 'https://web-static.kurobbs.com',
    'x-requested-with': 'com.kurogame.kjq',
    'sec-fetch-site': 'same-site',
    'sec-fetch-mode': 'cors',
    'sec-fetch-dest': 'empty',
    'accept-encoding': 'gzip, deflate, br',
    'accept-language': 'zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7',
}

const formData = new URLSearchParams()
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
  "message": "success",
  "msg": "success",
  "data": {
    "taskList": [
      {
        "taskId": "VQkfQ5",
        "taskName": "登录游戏",
        "taskProcess": 1,
        "taskLimit": 1,
        "status": 1,
        "type": 2,
        "remark": "每日登录账号进入游戏，即可获得15积分"
      },
      {
        "taskId": "VJuWYn",
        "taskName": "游戏活跃值达到100",
        "taskProcess": 100,
        "taskLimit": 100,
        "status": 1,
        "type": 2,
        "remark": "每日本活动绑定角色在游戏内活跃值达到100，即可获得20积分"
      },
      {
        "taskId": "RJdVwv",
        "taskName": "分享本活动页面",
        "taskProcess": 1,
        "taskLimit": 1,
        "status": 1,
        "type": 1,
        "remark": "每日完成一次活动页面分享，即可获得15积分"
      },
      {
        "taskId": "TKkzym",
        "taskName": "摇篮游行内容浏览",
        "taskProcess": 0,
        "taskLimit": 1,
        "status": 0,
        "type": 4,
        "remark": "每日浏览摇篮游行版本热门内容，即可获得10积分"
      },
      {
        "taskId": "CJSfpe",
        "taskName": "活动签到",
        "taskProcess": 1,
        "taskLimit": 1,
        "status": 2,
        "type": 5,
        "remark": "每日点击右侧完成签到，即可获得10积分"
      },
      {
        "taskId": "6RNLqL",
        "taskName": "查询囚笼数据",
        "taskProcess": 1,
        "taskLimit": 1,
        "status": 2,
        "type": 1,
        "remark": "活动期间完成一次囚笼数据查询，即可获得10积分"
      },
      {
        "taskId": "rC8h5G",
        "taskName": "关注赛利卡",
        "taskProcess": 1,
        "taskLimit": 1,
        "status": 2,
        "type": 3,
        "remark": "活动期间关注赛利卡，即可获得15积分"
      },
      {
        "taskId": "fU2JRF",
        "taskName": "关注战双帕弥什",
        "taskProcess": 1,
        "taskLimit": 1,
        "status": 2,
        "type": 3,
        "remark": "活动期间关注战双帕弥什，即可获得15积分"
      }
    ],
    "taskMilestoneList": [
      {
        "taskId": "LrKhfD",
        "prizeName": "螺母",
        "prizeType": 1,
        "prizeAmount": 5000,
        "milestoneCount": 50,
        "status": 2
      },
      {
        "taskId": "XwZRgY",
        "prizeName": "补给券",
        "prizeType": 5,
        "prizeAmount": 1,
        "milestoneCount": 100,
        "status": 2
      },
      {
        "taskId": "cDh7wJ",
        "prizeName": "螺母",
        "prizeType": 1,
        "prizeAmount": 15000,
        "milestoneCount": 200,
        "status": 0
      },
      {
        "taskId": "ChyxWn",
        "prizeName": "角色研发券",
        "prizeType": 1,
        "prizeAmount": 200,
        "milestoneCount": 300,
        "status": 0
      },
      {
        "taskId": "XrSeBk",
        "prizeName": "补给券",
        "prizeType": 5,
        "prizeAmount": 2,
        "milestoneCount": 400,
        "status": 0
      },
      {
        "taskId": "zpsVHG",
        "prizeName": "角色研发券",
        "prizeType": 1,
        "prizeAmount": 250,
        "milestoneCount": 500,
        "status": 0
      }
    ],
    "currentIntegral": 120
  }
}
```