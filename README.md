# Kuro-API-Collection

库街区 API 收集

目前只收集了项目需要用到的 API, 算是挖坑吧

目前所整理 API, 除非特别说明, 全部为 APP 端

API 请求头大致相同, 具体请见 [参数总结](/PARAMS.md) 

## 目录

### [用户](/API/user)

- ~~[发送验证码](#)~~ (麻烦还要极验)
- [验证码登录 APP 端](/API/user/sdkLogin.md)
- [验证码登录 Web 端](/API/user/sdkLoginForH5.md)
- [取个人信息 V2](/API/user/mineV2.md)
- [取绑定游戏账号列表](/API/user/role/findRoleList.md)
- [更新头像链接](/API/user/updateHeadUrl.md)
- [是否社区签到](/API/user/haveSignIn.md)
- [社区签到](/API/user/signIn.md)
- [关注用户](/API/user/followUser.md)

### [玩家](/API/gamer)

- [取账号绑定的游戏账号信息](/API/gamer/role/list.md)

### [奖励](/API/encourage)

- [取游戏签到信息 V2](/API/encourage/signIn/initSignInV2.md) 2024.06.02
- [游戏签到 V2](/API/encourage/signIn/v2.md) 2024.05.24
- [取游戏签到记录 V2](/API/encourage/signIn/queryRecordV2.md) 2024.06.02
- [社区分享任务](/API/encourage/level/shareTask.md)
- [取任务进度](/API/encourage/level/getTaskProcess.md)
- [取库洛币总数](/API/encourage/gold/getTotalGold.md)

### [论坛](/API/forum)

- [图片上传](/API/forum/uploadForumImg.md)
- [取帖子列表](/API/forum/list.md)
- [取帖子详情](/API/forum/getPostDetail.md)
- [通用论坛点赞](/API/forum/like.md)

### [活动](/API/activity)

- [取活动绑定游戏角色信息](/API/activity/gamer/role/getBindRoleInfo.md)
- [活动绑定游戏角色](/API/activity/gamer/role/bindRole.md)
- [取活动任务详情](/API/activity/task/getList.md)
- [完成活动任务](/API/activity/task/complete.md)
- [领取活动任务奖励](/API/activity/task/receive.md)

## 相关项目

- [Yunzai-Kuro-Plugin](https://github.com/TomyJan/Yunzai-Kuro-Plugin) Yunzai-Bot 插件

