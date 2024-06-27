# 参数总结

记录了现有 API 中一些共有/特殊参数

## 请求头

目前 [取游戏签到信息 V2](/API/encourage/signIn/initSignInV2.md) , [游戏签到 V2](/API/encourage/signIn/v2.md) , `/gamer/roleBox` 和 `/activity` 路由下的请求头和其他不一样, 类似浏览器环境, 可以前往查看, 其他 API 大差不差

特别的, `/gamer/widget`下的请求有两套请求参数, 在库街区内页面展示时使用的类似浏览器环境, 用于更新小组件信息的请求头类似下方

### 共有请求头

| 字段        | 类型 | 内容         | 备注                                     |
| ----------- | ---- | ------------ | ---------------------------------------- |
| devCode     | str  | 必须但不校验 | 073A9EFAC18FC50616DD15808DAE719DBCB904B7 |
| ip          | str  |              | 192.168.102.138                          |
| source      | str  | 必须         | android                                  |
| version     | str  |              | 2.2.0                                    |
| versionCode | str  |              | 2200                                     |
| token       | str  | token        | eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| osVersion       | str  | -            | Android                                  |
| distinct_id     | str  | -            | 96b1567b-b5e6-422f-a1dd-7cb1e58c5db7, UUID 格式 |
| countryCode     | str  | -            | CN                                       |
| model           | str  |              | 23127PN0CC                               |
| lang            | str  |              | zh-Hans                                  |
| channelId       | str  | ? | 2                                        |
| Content-Type    | str  |              | application/x-www-form-urlencoded        |
| Accept-Encoding | str  |              | gzip                                     |
| Cookie | str  |              | user_token=eyJhbGciOiJIUzI1NiJ9.eyJjcmVhdGVkIjoxNjg5NDk4MDkxMjQ1LCJ1c2VySWQiOjEwMDY1NjY5fQ.AAAA_AAAAAAAAAAAAAAAAAAAAAAAAAAA-AAAAAAAAAA |
| User-Agent      | str  |              | okhttp/3.11.0                            |

### 特殊请求头

- [取账号绑定的游戏账号信息](/API/gamer/role/list.md) / [取绑定游戏账号列表](/API/user/role/findRoleList.md) 

这些接口不需要 `distinct_id` 

- [图片上传](/API/forum/uploadForumImg.md) 

content-type: multipart/form-data; boundary=48dc8243-9106-4152-b8d7-27a3aa6cdddd (随机生成)

- [取账号绑定的游戏账号信息](/API/gamer/role/list.md) / [取绑定游戏账号列表](/API/user/role/findRoleList.md) / [取库洛币总数](/API/encourage/gold/getTotalGold.md)

content-type: application/x-www-form-urlencoded; charset=utf-8

- [验证码登录 APP 端](/API/user/sdkLogin.md)

当然没有 token 了

## 请求体

除了 图片上传接口 为 form data 外, 其余均为字符串拼接

## 响应体

目前所记录 API 响应体均为 json

| 字段    | 类型        | 内容       | 备注                                                         |
| ------- | ----------- | ---------- | ------------------------------------------------------------ |
| code    | num         | 返回值     | 220: cookie过期<br />200: 成功<br />其它则为具体业务特定的 code |
| msg     | str         | 提示信息   | 请求成功//用户登录已过期/…                                   |
| success | bool        | true/false | token 有效时才有<br />目前发现签到类请求可能风控, 表现为 code = 220 但有 success = false |
| data    | str/arr/obj | 详细信息   | 请求成功时才有                                               |

注意 `activity` 路由下的请求没有 `success`, 多了一个 `message`, 目前看来其值与 `msg` 相同
