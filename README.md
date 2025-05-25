# Kuro-API-Collection

库街区 API 收集

目前只收集了项目需要用到的 API, 算是挖坑吧

目前所整理 API, 除非特别说明, 全部为 APP 端

`2024.05.24` 之后整理的 API 已在名称后面注明更新时间, API 具体请求和响应可能会有所改变, 如非已经发现的破坏性改动, 将不会积极更新, 请自行测试

API 请求头大致相同, 具体请见 [参数总结](/PARAMS.md) 

~~**注意, 库洛在 2024.06.28 暗改了部分 API 域名 (主要为网页内容类, 即请求头为浏览器环境的, 变更为 `event.kurobbs.com` ), 并且新增一个获取 IP 的接口用于在请求的 devCode 里上报, 虽然这些接口大多在旧域名下依然可用, 但是建议尽快更新!**~~
6.29 下午又改回来了 (除了 IP 接口), 幽默牢库

## 目录

### [用户](/API/user)

- [发送验证码 APP 端](/API/user/getSmsCode.md) 2024.06.17
- [验证码登录 APP 端](/API/user/sdkLogin.md)
- [验证码登录 Web 端](/API/user/sdkLoginForH5.md)
- [取个人信息 V2](/API/user/mineV2.md)
- [取绑定游戏账号列表](/API/user/role/findRoleList.md)
- [更新头像链接](/API/user/updateHeadUrl.md)
- ~~[是否社区签到](/API/user/haveSignIn.md)~~ 此 API 已弃用, 建议使用下面的
- [社区签到信息](/API/user/signIn/info.md) 2024.06.24
- [社区签到](/API/user/signIn.md) 2024.08.05
- [关注用户](/API/user/followUser.md)

### [玩家](/API/gamer)

- [取账号绑定的游戏账号信息](/API/gamer/role/list.md) 2024.06.03
- [鸣潮游戏角色基础数据](/API/gamer/roleBox/aki/baseData.md) 2024.06.19
- [鸣潮游戏角色声骸收集数据](/API/gamer/roleBox/aki/calabashData.md) 2024.06.19
- [鸣潮游戏角色探索数据](/API/gamer/roleBox/aki/exploreIndex.md) 2024.06.19
- [战双小组件数据](/API/gamer/widget/game2/getData.md) 2025.01.13
- [鸣潮小组件数据](/API/gamer/widget/game3/getData.md) 2025.01.13

### [奖励](/API/encourage)

- [取游戏签到信息 V2](/API/encourage/signIn/initSignInV2.md) 2024.06.29
- [游戏签到 V2](/API/encourage/signIn/v2.md) 2024.06.25
- [取游戏签到记录 V2](/API/encourage/signIn/queryRecordV2.md) 2024.06.29
- [社区分享任务](/API/encourage/level/shareTask.md)
- [取任务进度](/API/encourage/level/getTaskProcess.md)
- [取库洛币总数](/API/encourage/gold/getTotalGold.md)

### [论坛](/API/forum)

- [图片上传](/API/forum/uploadForumImg.md)
- [取帖子列表](/API/forum/list.md)
- [取帖子详情](/API/forum/getPostDetail.md)
- [通用论坛点赞](/API/forum/like.md)

### [鸣潮](/API/aki/roleBox/akiBox)

- [[新] 鸣潮游戏角色基础数据](API/aki/roleBox/akiBox/baseData.md) 2025.05.25
- [[新] 鸣潮游戏角色声骸收集数据](API/aki/roleBox/akiBox/calabashData.md) 2025.05.25
- [[新] 鸣潮游戏角色探索数据](API/aki/roleBox/akiBox/exploreIndex.md) 2025.05.25

### [活动](/API/activity)

此分组下的 API 应该均已过期, 待后续更新

- [取活动绑定游戏角色信息](/API/activity/gamer/role/getBindRoleInfo.md)
- [活动绑定游戏角色](/API/activity/gamer/role/bindRole.md)
- [取活动任务详情](/API/activity/task/getList.md)
- [完成活动任务](/API/activity/task/complete.md)
- [领取活动任务奖励](/API/activity/task/receive.md)

## 相关项目

- [Yunzai-Kuro-Plugin](https://github.com/TomyJan/Yunzai-Kuro-Plugin) Yunzai-Bot 插件

