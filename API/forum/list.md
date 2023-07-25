# 取帖子列表

## 请求地址

> https://api.kurobbs.com/forum/list

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

| 字段       | 类型 | 内容     | 备注                                                         |
| ---------- | ---- | -------- | ------------------------------------------------------------ |
| forumId    | num  | 板块 id  | 战双 推荐=2, 伊甸闲庭=3, 攻略=4, 同人=5<br />鸣潮 推荐=9, 天诚茶馆=10, 同人=11 |
| gameId     | num  | 游戏 id  | 战双 = 2, 鸣潮 = 3                                           |
| pageIndex  | num  | 页码     | 1                                                            |
| pageSize   | num  | 每页帖数 | 20                                                           |
| searchType | num  | 排序方式 | 最新发布=1, 最新回复=2, 推荐板块无此选项, 默认2              |
| timeType   | num  | (?)      | 0                                                            |
| topicId    | num  | 话题 id  | 不筛选话题默认 0                                             |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容         | 备注                           |
| ------- | ---- | ------------ | ------------------------------ |
| code    | num  | 返回值       | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息     | 请求成功                       |
| success | bool | true         | token 有效时才有               |
| data    | obj  | 帖子信息内容 | 成功时才有                     |

### `data` 对象

| 字段      | 类型 | 内容                 | 备注                         |
| --------- | ---- | -------------------- | ---------------------------- |
| postList  | arr  | 帖子信息列表数组     |                              |
| topList   | arr  | 置顶帖子简单信息数组 |                              |
| hasNext   | num  | 是否有下一页?        | 1                            |
| hotTopics | arr  | 热门帖子列表?        | 空的, 我也不知道会有什么内容 |

### `postList` 成员对象

| 字段         | 类型 | 内容                 | 备注                   |
| ------------ | ---- | -------------------- | ---------------------- |
| browseCount  | str  | 浏览量               | 6                      |
| commentCount | num  | 评论数               | 2                      |
| gameForumId  | num  | 板块 id              | 见 [请求体](#请求体) |
| gameId       | num  | 游戏 id              | 见 [请求体](#请求体) |
| gameName     | str  | 游戏名称             | 战双帕弥什             |
| identifyClassify | num  | 身份认证的类型    | 没认证的没这个键, 1=蓝色星星, 2=黄色V |
| identifyNames | str  | 身份认证的名称      | 没认证的没这个键, 战双版主/搬砖工一枚，请轻拍！ |
| imgContent   | arr  | 帖子正文中的图片列表数组 |                        |
| imgCount | num  | 帖子正文中的图片数量, 和`imgContent`对应 | 1                     |
| isElite | num  | (?)          | 0                     |
| isFollow | num  | (?)          | 0                     |
| isLike | num  | 是否赞过    | 0                     |
| isLock | num  | (?)          | 0                     |
| isOfficial | num  | (?)          | 0                     |
| isPublisher | num  | (?)          | 0                     |
| likeCount | num  | 点赞量             | 2                     |
| postContent | str  | 帖子文本, 用于预览吧 | 好像会截取到非文本内容就停止, 纯文本, 并且不知道什么状态下会在开头加一个空格 |
| postCover | str  | (?)  | 空的, 看起来并没用到的参数, 帖子封面? |
| postCoverVo | obj  | (?)          | 对象包含两个键值对, 不分开写了, imgHeight=0, imgWidth=0 |
| postId | str  | 帖子 id          | 1133555470924988416  |
| postTitle | str  | 帖子标题           | 测试标题                 |
| postType | num  | (?)          | 1                     |
| recentlyReplayTime | str  | 人类易读的最近回复时间 | 刚刚/3分钟前/07-25        |
| showTime | str  | 人类易读的发帖时间?   | 刚刚/3分钟前/07-25        |
| topicList | arr  | 帖子带的话题数组 |                      |
| userHeadUrl | str  | 发帖人头像链接 | https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg |
| userId | str  | 发帖人 id       | 10065669             |
| userLevel | num  | 发帖人等级       | 都是 0 级别看了           |
| userName | str  | 发帖人昵称         | TomyJan              |

### `postList` 中的 `imgContent` 成员对象

| 字段      | 类型 | 内容     | 备注                                                         |
| --------- | ---- | -------- | ------------------------------------------------------------ |
| imgHeight | num  | 图片高   | 1080                                                         |
| imgWidth  | num  | 图片宽   | 1728                                                         |
| url       | str  | 图片链接 | https://prod-alicdn-community.kurobbs.com/forum/1690302277218520029.jpg |

### `postList` 中的 `topicList` 成员对象

| 字段      | 类型 | 内容          | 备注                |
| --------- | ---- | ------------- | ------------------- |
| postId    | str  | 这个帖子的 id | 1133555470924988416 |
| topicId   | num  | 话题 id       | 80                  |
| topicName | str  | 话题名称      | 测试服              |

### `topList` 成员对象

| 字段      | 类型 | 内容      | 备注                                   |
| --------- | ---- | --------- | -------------------------------------- |
| postId    | str  | 帖子 id   | 1079855462044229632                    |
| postTitle | num  | 帖子标题  | 库街区使用及管理规则（战双帕弥什版区） |
| userId    | str  | 发帖人 id | 10002006                               |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/forum/list'
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
formData.append('pageIndex', 1)
formData.append('pageSize', 20)
formData.append('searchType', 2)
formData.append('timeType', 0)
formData.append('topicId', 0)
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
        "postList": [
            {
                "browseCount": "12863",
                "commentCount": 311,
                "gameForumId": 3,
                "gameId": 2,
                "gameName": "战双帕弥什",
                "identifyClassify": 2,
                "identifyNames": "战双版主",
                "imgContent": [
                    {
                        "imgHeight": 1008,
                        "imgWidth": 1920,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1689926195890913564.png"
                    },
                    {
                        "imgHeight": 397,
                        "imgWidth": 1077,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1690167753184277483.jpg"
                    },
                    {
                        "imgHeight": 794,
                        "imgWidth": 1080,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1690167761281730620.jpg"
                    }
                ],
                "imgCount": 3,
                "isElite": 0,
                "isFollow": 0,
                "isLike": 0,
                "isLock": 0,
                "isOfficial": 0,
                "isPublisher": 0,
                "likeCount": 4979,
                "postContent": " ",
                "postCover": "",
                "postCoverVo": {
                    "imgHeight": 0,
                    "imgWidth": 0
                },
                "postId": "1131979032270684160",
                "postTitle": "【摇篮游行】版本答疑活动",
                "postType": 1,
                "recentlyReplayTime": "刚刚",
                "showTime": "07-21",
                "topicList": [
                    {
                        "postId": "1131979032270684160",
                        "topicId": 77,
                        "topicName": "拉弥亚"
                    },
                    {
                        "postId": "1131979032270684160",
                        "topicId": 78,
                        "topicName": "摇篮游行"
                    }
                ],
                "userHeadUrl": "https://prod-alicdn-community.kurobbs.com/headCode/akianke.png",
                "userId": "10008770",
                "userLevel": 0,
                "userName": "小丛雨的凌飒"
            },
            {
                "browseCount": "6",
                "commentCount": 2,
                "gameForumId": 3,
                "gameId": 2,
                "gameName": "战双帕弥什",
                "imgContent": [
                    {
                        "imgHeight": 1080,
                        "imgWidth": 1728,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1690302277218520029.jpg"
                    }
                ],
                "imgCount": 1,
                "isElite": 0,
                "isFollow": 0,
                "isLike": 0,
                "isLock": 0,
                "isOfficial": 0,
                "isPublisher": 0,
                "likeCount": 2,
                "postContent": " 测试文本内容",
                "postCover": "",
                "postCoverVo": {
                    "imgHeight": 0,
                    "imgWidth": 0
                },
                "postId": "1133555470924988416",
                "postTitle": "测试标题",
                "postType": 1,
                "recentlyReplayTime": "3分钟前",
                "showTime": "5分钟前",
                "topicList": [
                    {
                        "postId": "1133555470924988416",
                        "topicId": 80,
                        "topicName": "测试服"
                    }
                ],
                "userHeadUrl": "https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg",
                "userId": "10065669",
                "userLevel": 0,
                "userName": "TomyJan"
            },
            {
                "browseCount": "24",
                "commentCount": 1,
                "gameForumId": 3,
                "gameId": 2,
                "gameName": "战双帕弥什",
                "identifyClassify": 2,
                "identifyNames": "战双版主",
                "imgContent": [
                    {
                        "imgHeight": 540,
                        "imgWidth": 960,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1690301337524944324.jpg"
                    },
                    {
                        "imgHeight": 1004,
                        "imgWidth": 1399,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1690301338246355763.jpg"
                    }
                ],
                "imgCount": 2,
                "isElite": 0,
                "isFollow": 0,
                "isLike": 0,
                "isLock": 0,
                "isOfficial": 0,
                "isPublisher": 0,
                "likeCount": 7,
                "postContent": " 原图",
                "postCover": "",
                "postCoverVo": {
                    "imgHeight": 0,
                    "imgWidth": 0
                },
                "postId": "1133552063524290560",
                "postTitle": "群友需求•拉弥亚登录界面",
                "postType": 1,
                "recentlyReplayTime": "5分钟前",
                "showTime": "18分钟前",
                "topicList": [],
                "userHeadUrl": "https://prod-alicdn-community.kurobbs.com/headCode/Yayu2.png",
                "userId": "10009113",
                "userLevel": 0,
                "userName": "憨露喵"
            },
            {
                "browseCount": "17466",
                "commentCount": 67,
                "gameForumId": 3,
                "gameId": 2,
                "gameName": "战双帕弥什",
                "identifyClassify": 1,
                "identifyNames": "搬砖工一枚，请轻拍！",
                "imgContent": [
                    {
                        "imgHeight": 12547,
                        "imgWidth": 1920,
                        "url": "https://prod-alicdn-community.kurobbs.com/forum/1689933712773792834.jpg"
                    }
                ],
                "imgCount": 1,
                "isElite": 0,
                "isFollow": 0,
                "isLike": 0,
                "isLock": 0,
                "isOfficial": 0,
                "isPublisher": 0,
                "likeCount": 4896,
                "postContent": "各位指挥官~库街区兑换商城实物周边上新喽，不知道大家有没有准备好库洛币呢？指挥官可在兑换商城查看新上架周边商品，7月30日12:00兑换开启不见不散~更多实物周边和游戏道具还将不定期上架，敬请期待。",
                "postCover": "",
                "postCoverVo": {
                    "imgHeight": 0,
                    "imgWidth": 0
                },
                "postId": "1132017910732800000",
                "postTitle": "兑换商城上新，7月30日开放兑换！",
                "postType": 1,
                "recentlyReplayTime": "12分钟前",
                "showTime": "07-21",
                "topicList": [],
                "userHeadUrl": "https://prod-alicdn-community.kurobbs.com/headCode/bricks.jpg",
                "userId": "10009758",
                "userLevel": 0,
                "userName": "库街区搬砖工"
            }
        ],
        "topList": [
            {
                "postId": "1079855462044229632",
                "postTitle": "库街区使用及管理规则（战双帕弥什版区）",
                "userId": "10002006"
            },
            {
                "postId": "1131979032270684160",
                "postTitle": "【摇篮游行】版本答疑活动",
                "userId": "10008770"
            },
            {
                "postId": "1131636559180120064",
                "postTitle": "【有奖活动】「摇篮游行」2.6版本剧情讨论活动",
                "userId": "10002006"
            }
        ],
        "hasNext": 1,
        "hotTopics": []
    },
    "msg": "请求成功",
    "success": true
}
```