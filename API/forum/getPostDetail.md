# 取帖子详情

## 请求地址

> https://api.kurobbs.com/forum/getPostDetail

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

| 字段            | 类型 | 内容     | 备注                                            |
| --------------- | ---- | -------- | ----------------------------------------------- |
| isOnlyPublisher | num  | (?)      | 0                                               |
| postId          | num  | 帖子 id  | 1133555470924988416                             |
| showOrderType   | num  | (?)      | 2                                               |

## 响应体

json

### 根对象

| 字段    | 类型 | 内容         | 备注                           |
| ------- | ---- | ------------ | ------------------------------ |
| code    | num  | 返回值       | 220: token 失效<br />200: 成功 |
| msg     | str  | 提示信息     | 请求成功                       |
| success | bool | true         | token 有效时才有               |
| data    | obj  | 帖子详情内容 | 成功时才有                     |

### `data` 对象

| 字段       | 类型 | 内容     | 备注               |
| ---------- | ---- | -------- | ------------------ |
| gameId     | num  | 游戏 id  | 战双 = 2, 鸣潮 = 3 |
| isFollow   | num  | (?)      | 0                  |
| isLike     | num  | 是否赞过 | 0                  |
| postDetail | obj  | 帖子详情 |                    |
| isCollect  | num  | (?)      | 0                  |
| comment    | arr  | 评论数组 | 成员都是一级评论   |

### `postDetail` 对象

| 字段            | 类型 | 内容               | 备注                                                         |
| --------------- | ---- | ------------------ | ------------------------------------------------------------ |
| appealing       | bool | (?)                | false                                                        |
| browseCount     | str  | 浏览量             | 3                                                            |
| collectionCount | num  | (?)                | 0                                                            |
| commentCount    | num  | 评论数             | 2                                                            |
| gameForumId     | num  | 板块 id            | 战双 推荐=2, 伊甸闲庭=3, 攻略=4, 同人=5<br />鸣潮 推荐=9, 天诚茶馆=10, 同人=11 |
| gameForumVo     | obj  | (?)                |                                                              |
| gameId          | num  | 游戏 id            | 战双 = 2, 鸣潮 = 3                                           |
| gameName        | str  | 游戏名             | 战双帕弥什                                                   |
| headCodeUrl     | str  | 头像图片直链       | https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg |
| id              | str  | 帖子 id            | 1133555470924988416                                          |
| isCopyright     | bool | 是否原创           | true                                                         |
| isElite         | num  | (?)                | 0                                                            |
| isLock          | num  | (?)                | 0                                                            |
| isMine          | num  | 是否自己的帖子     | 1                                                            |
| isOfficial      | num  | (?)                | 0                                                            |
| isRecommend     | num  | (?)                | 1                                                            |
| isTop           | num  | (?)                | 0                                                            |
| likeCount       | num  | 点赞数             | 0                                                            |
| postContent     | arr  | 帖子内容数组       | 每段内容一个成员                                             |
| postH5Content   | str  | 帖子 H5 格式的内容 | 下面的示例有几乎所有的类型                                   |
| postTime        | str  | 人类易读的发帖时间 | 刚刚/3分钟前/07-25                                           |
| postTitle       | str  | 帖子标题           | 测试标题                                                     |
| postType        | num  | (?)                | 1                                                            |
| postUserId      | str  | 发帖人 id          | 10065669                                                     |
| reviewStatus    | num  | 审核状态?          | 1                                                            |
| topicList       | arr  | 话题数组           |                                                              |
| userHeadCode    | str  | 发帖人头像 id      | 35                                                           |
| userLevel       | num  | 发帖人等级         | 都是 0 级别看了                                              |
| userName        | str  | 发帖人昵称         | TomyJan                                                      |

### `postDetail` 中的 `gameForumVo` 对象

| 字段              | 类型 | 内容     | 备注                                                         |
| ----------------- | ---- | -------- | ------------------------------------------------------------ |
| forumDataType     | num  | (?)      | 3                                                            |
| forumListShowType | num  | (?)      | 1                                                            |
| forumType         | num  | (?)      | https://prod-alicdn-community.kurobbs.com/forum/1690302277218520029.jpg |
| forumUiType       | num  | (?)      | 1728                                                         |
| id                | num  | 板块 id  | 3, 见 [postDetail 对象](#postDetail-对象)                    |
| isOfficial        | num  | (?)      | 0                                                            |
| isSpecial         | num  | (?)      | 0                                                            |
| name              | str  | 板块名称 | 伊甸闲庭                                                     |
| sort              | num  | (?)      | 3                                                            |

### `postDetail` 中的 `postContent` 成员对象

| 字段        | 类型 | 内容         | 备注                                                         |
| ----------- | ---- | ------------ | ------------------------------------------------------------ |
| content     | str  | 文本内容     | contentType=1 时才有, 纯文本不带任何样式信息. 开头会多一个空格 |
| contentLink | obj  | 链接内容对象 | contentType=3 时才有                                         |
| contentType | num  | 内容类型     | 1 = 文本, 2 = 图片, 3 = 链接, 4 = 分隔符(实际是一个图片)     |
| imgHeight   | num  | 图片高       | contentType=2 或 4 时为图片高度, 否则为0                     |
| imgWidth    | num  | 图片宽       | contentType=2 或 4 时为图片宽度, 否则为0                     |
| isCover     | num  | (?)          | 0                                                            |
| topicFlag   | num  | (?)          | 0                                                            |
| url         | str  | 图片直链     | contentType=4 时才有, 分隔符图片的直链                       |

### `postDetail` 中的 `postContent` 中的 `contentLink` 对象

| 字段          | 类型 | 内容         | 备注                                                         |
| ------------- | ---- | ------------ | ------------------------------------------------------------ |
| iconUrl       | str  | 链接图标直链 | https://prod-alicdn-community.kurobbs.com/icon/1675408874807512191.png |
| isCustomTitle | bool | (?)          | false                                                        |
| isDelete      | bool | (?)          | false                                                        |
| nickName      | str  | (?)          | 空                                                           |
| title         | str  | 链接文本     | 测试链接文本                                                 |
| url           | str  | 链接地址     | https://vov.moe                                              |

### `postDetail` 中的 `topicList` 成员对象

| 字段      | 类型 | 内容          | 备注                |
| --------- | ---- | ------------- | ------------------- |
| postId    | str  | 这个帖子的 id | 1133555470924988416 |
| topicId   | num  | 话题 id       | 80                  |
| topicName | str  | 话题名称      | 测试服              |

### `comment` 对象

| 字段            | 类型 | 内容               | 备注                                                         |
| --------------- | ---- | ------------------ | ------------------------------------------------------------ |
| commentContent | arr | 评论内容数组            | 见 [postDetail 中的 postContent 成员对象](#postDetail-中的-postContent-成员对象) |
| commentId | str | 评论 id             | 1133555624024195072                                     |
| commentTime | str | 人类易读的评论时间       | 刚刚/3分钟前/07-25                                           |
| floor  | num | 楼层                | 1                                                        |
| isLike | num | 是否赞过       | 0                                                        |
| isMine | num | 是否自己发布的        | 1                                                        |
| isOfficial | num | (?)             | 0                                                        |
| isPublisher | num | 是否发布者     | 1                                                        |
| likeCount | num | 点赞数                | 0                                                        |
| replyCount | num | 评论的回复数             | 1                                                        |
| replyVos | arr | 评论的楼中楼评论数组 |                                                         |
| reviewStatus | num | 审核状态?               | 1                                                        |
| userHeadCode | str | 评论人头像 id     | 35                                                       |
| userHeadUrl | str | 评论人头像图片直链       | https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg |
| userId | str | 评论人 id           | 10065669                                                |
| userLevel | num | 评论人等级        | 都是 0 级别看了                                               |
| userName | str | 评论人昵称      | TomyJan                                                      |

### `comment` 中的 `replyVos` 成员对象

| 字段            | 类型 | 内容               | 备注                                                         |
| --------------- | ---- | ------------------ | ------------------------------------------------------------ |
| createTime | num | 回复 13 位时间戳 | 1690302357000 |
| isLike | str | 是否赞过       | 0 |
| isMine | str | 是否自己发表的     | 1 |
| isOfficial | str | (?)         | 0 |
| isPublisher | str | 是否发布者  | 1 |
| likeCount | str | 回复点赞数         | 0 |
| postCommentId | str | 回复的评论 id      | 1133555624024195072 |
| postCommentReplayId | str | 回复的楼中楼 id     | 0 |
| replyContentStr | str | 回复内容文本      | 开头会多一个空格 |
| replyId | str | 回复 id         | 1133555777264369664 |
| replyTime | str | 人类易读的回复时间   | 刚刚/3分钟前/07-25 |
| reviewStatus | num | 审核状态?         | 1 |
| toUserId | str | 回复的评论者 id    | 10065669 |
| toUserName | str | (?)       | 空 |
| userHeadCode | str | 回复者头像 id      | 35 |
| userHeadUrl | str | 回复者头像图片直链       | https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg |
| userId | str | 回复者 id        | 10065669                                                |
| userLevel | num | 回复者等级     | 都是 0 级别看了                                               |
| userName | str | 回复者昵称   | TomyJan                                                      |

## 示例

### 请求

```js
const url = 'https://api.kurobbs.com/forum/getPostDetail'
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
formData.append('isOnlyPublisher', 0)
formData.append('postId', 1133555470924988416)
formData.append('showOrderType', 2)
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
        "gameId": 2,
        "isFollow": 0,
        "isLike": 0,
        "postDetail": {
            "appealing": false,
            "browseCount": "3",
            "collectionCount": 0,
            "commentCount": 2,
            "gameForumId": 3,
            "gameForumVo": {
                "forumDataType": 3,
                "forumListShowType": 1,
                "forumType": 1,
                "forumUiType": 1,
                "id": 3,
                "isOfficial": 0,
                "isSpecial": 0,
                "name": "伊甸闲庭",
                "sort": 3
            },
            "gameId": 2,
            "gameName": "战双帕弥什",
            "headCodeUrl": "https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg",
            "id": "1133555470924988416",
            "isCopyright": true,
            "isElite": 0,
            "isLock": 0,
            "isMine": 1,
            "isOfficial": 0,
            "isRecommend": 1,
            "isTop": 0,
            "likeCount": 0,
            "postContent": [
                {
                    "content": " 测试文本内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试 h2 内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试 h1 内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试加粗内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试斜体内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试下划线内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试居中内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 测试居右内容",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " 红色 绿色",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " ",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "contentLink": {
                        "iconUrl": "https://prod-alicdn-community.kurobbs.com/icon/1675408874807512191.png",
                        "isCustomTitle": false,
                        "isDelete": false,
                        "nickName": "",
                        "title": "测试链接文本",
                        "url": "https://vov.moe"
                    },
                    "contentType": 3,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " ",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "contentType": 4,
                    "imgHeight": 30,
                    "imgWidth": 345,
                    "isCover": 0,
                    "topicFlag": 0,
                    "url": "https://prod-alicdn-community.kurobbs.com/postBanner/1676361604531109644.png"
                },
                {
                    "content": " ",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "contentType": 4,
                    "imgHeight": 30,
                    "imgWidth": 345,
                    "isCover": 0,
                    "topicFlag": 0,
                    "url": "https://prod-alicdn-community.kurobbs.com/postBanner/1676361707594208503.png"
                },
                {
                    "content": " ",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "content": " ",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                },
                {
                    "contentType": 2,
                    "imgHeight": 1080,
                    "imgWidth": 1728,
                    "isCover": 0,
                    "topicFlag": 0,
                    "url": "https://prod-alicdn-community.kurobbs.com/forum/1690302277218520029.jpg"
                },
                {
                    "content": " ",
                    "contentType": 1,
                    "imgHeight": 0,
                    "imgWidth": 0,
                    "isCover": 0,
                    "topicFlag": 0
                }
            ],
            "postH5Content": "\n <p><font color=\"#292b2f\">测试文本内容</font></p>\n <p><font color=\"#292b2f\" size=\"4\">测试 h2 内容</font></p>\n <p><font color=\"#292b2f\" size=\"5\">测试</font><font color=\"#292b2f\" size=\"4\"> </font><font color=\"#292b2f\" size=\"5\">h1</font><font color=\"#292b2f\" size=\"4\"> </font><font color=\"#292b2f\" size=\"5\">内容</font></p>\n <p><font size=\"4\"><b style=\"color: rgb(41, 43, 47);\">测试加粗内容</b></font></p>\n <p><font size=\"4\" color=\"#292b2f\"><b style=\"\"><i>测试斜体内容</i></b></font></p>\n <p><font size=\"4\" color=\"#292b2f\"><b style=\"\"><i><u>测试下划线内容</u></i></b></font></p>\n <p style=\"text-align: center;\"><font size=\"4\" color=\"#292b2f\"><b style=\"\"><i><u>测试居中内容</u></i></b></font></p>\n <p style=\"text-align: right;\"><font size=\"4\" color=\"#292b2f\"><b style=\"\"><i><u>测试居右内容</u></i></b></font></p>\n <p><font color=\"#ff3f4c\">红色&nbsp;</font><font color=\"#10c286\">绿色</font></p>\n <div class=\"w-e_link-card\" card-des=\"https://vov.moe,&amp;,测试链接文本\" data-module-name=\"link-card\" has-delete=\"true\" contenteditable=\"false\">\n  <div class=\"w-e_link-card_link-wrap\">\n   <img class=\"w-e_link-card_img\" src=\"https://prod-alicdn-community.kurobbs.com/icon/1675408874807512191.png\">\n   <div class=\"w-e_link-card_detail\">\n    <span class=\"w-e_link-card_title w-e_hide-font--nowrap\" custom-title=\"false\">测试链接文本</span>\n    <span class=\"w-e_link-card_address w-e_hide-font--nowrap\">https://vov.moe</span>\n   </div>\n  </div>\n </div>\n <div class=\"w-e_line-card\" data-module-name=\"line-card\" has-delete=\"true\" contenteditable=\"false\">\n  <img class=\"w_e_line_image\" img-des=\"345,30,https://prod-alicdn-community.kurobbs.com/postBanner/1676361604531109644.png\" width=\"100%\" src=\"https://prod-alicdn-community.kurobbs.com/postBanner/1676361604531109644.png\">\n </div>\n <div class=\"w-e_line-card\" data-module-name=\"line-card\" has-delete=\"true\" contenteditable=\"false\">\n  <img class=\"w_e_line_image\" img-des=\"345,30,https://prod-alicdn-community.kurobbs.com/postBanner/1676361707594208503.png\" width=\"100%\" src=\"https://prod-alicdn-community.kurobbs.com/postBanner/1676361707594208503.png\">\n </div>\n <p><br></p>\n <div class=\"w-e_img-card\" data-module-name=\"img-card\" has-delete=\"true\" contenteditable=\"false\">\n  <img class=\"w_e_network_image\" img-des=\"1728,1080,https://prod-alicdn-community.kurobbs.com/forum/1690302277218520029.jpg\" listen-img-load=\"true\" src=\"https://prod-alicdn-community.kurobbs.com/forum/1690302277218520029.jpg\">\n </div>\n <p><br></p>\n",
            "postTime": "2分钟前",
            "postTitle": "测试标题",
            "postType": 1,
            "postUserId": "10065669",
            "reviewStatus": 1,
            "topicList": [
                {
                    "postId": "1133555470924988416",
                    "topicId": 80,
                    "topicName": "测试服"
                }
            ],
            "userHeadCode": "35",
            "userLevel": 0,
            "userName": "TomyJan"
        },
        "isCollect": 0,
        "comment": [
            {
                "commentContent": [
                    {
                        "content": " 测试评论_[/库街区-爱你]",
                        "contentType": 1,
                        "imgHeight": 0,
                        "imgWidth": 0,
                        "isCover": 0,
                        "topicFlag": 0
                    }
                ],
                "commentId": "1133555624024195072",
                "commentTime": "1分钟前",
                "floor": 1,
                "isLike": 0,
                "isMine": 1,
                "isOfficial": 0,
                "isPublisher": 1,
                "likeCount": 0,
                "replyCount": 1,
                "replyVos": [
                    {
                        "createTime": 1690302357000,
                        "isLike": 0,
                        "isMine": 1,
                        "isOfficial": 0,
                        "isPublisher": 1,
                        "likeCount": 0,
                        "postCommentId": "1133555624024195072",
                        "postCommentReplayId": "0",
                        "replyContentStr": " 测试楼中楼",
                        "replyId": "1133555777264369664",
                        "replyTime": "1分钟前",
                        "reviewStatus": 1,
                        "toUserId": "10065669",
                        "toUserName": "",
                        "userHeadCode": "35",
                        "userHeadUrl": "https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg",
                        "userId": "10065669",
                        "userLevel": 0,
                        "userName": "TomyJan"
                    }
                ],
                "reviewStatus": 1,
                "userHeadCode": "35",
                "userHeadUrl": "https://prod-alicdn-community.kurobbs.com/forum/1690015964827463788.jpg",
                "userId": "10065669",
                "userLevel": 0,
                "userName": "TomyJan"
            }
        ]
    },
    "msg": "请求成功",
    "success": true
}
```