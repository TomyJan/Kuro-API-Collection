# 取access_token用来获取地址

更新时间: 2024.7.1

## 请求地址

> https://user-zone-api.kurogame.com/logistics/delivery-address/list.lg

## 请求方式
**GET**

## 认证方式
**access_token**

## 请求头

| 字段             | 类型 | 内容                                                                                                      | 备注                        |
|------------------|------|-----------------------------------------------------------------------------------------------------------|-----------------------------|
| Host             | str  | user-zone-api.kurogame.com                                                                                |                             |
| Accept           | str  | \*/\*                                                                                                     |                             |
| Kr-Ver           | str  | 1.1.0                                                                                                     |                             |
| baggage          | str  | sentry-environment=production,sentry-release=1.1.0,sentry-transaction=Select,sentry-public_key=1111111111111111111111111111,sentry-trace_id=AAAAAAAAAAA,sentry-sample_rate=0.5 |可不填 |
| Sec-Fetch-Site   | str  | cross-site                                                                                                |                             |
| accessToken      | str  | 1111111111111111111111111111111111111                                                                     | 需替换为实际的 access_token |
| Accept-Language  | str  | zh-Hans,zh-CN                                                                                             |  可不填                           |
| Sec-Fetch-Mode   | str  | cors                                                                                                      |                             |
| sentry-trace     | str  | AAAAAAAAAAA-BBBBBBBBBBBB-1                                                      |  前半段同sentry-trace_id                           |
| Origin           | str  | https://web-static.kurobbs.com                                                                            |                             |
| Referer          | str  | https://web-static.kurobbs.com/                                                                           |                             |
| User-Agent       | str  | Mozilla/5.0 (iPhone; CPU iPhone OS 17_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko)  KuroGameBox/2.2.1 | |
| Accept-Encoding  | str  | gzip, deflate, br                                                                                         |                             |
| Connection       | str  | keep-alive                                                                                                |                             |
| Content-Type     | str  | application/x-www-form-urlencoded;charset=UTF-8                                                           |                             |
| Sec-Fetch-Dest   | str  | empty                                                                                                     |                             |

## 请求体

**无**

## 响应体

**json**

### 根对象

| 字段    | 类型 | 内容     | 备注                                      |
|---------|------|----------|-------------------------------------------|
| code    | num  | 返回值   | 220: token 失效<br>200: 成功               |
| data    | arr  | 详细信息 | 成功时才有，未绑定时为空数组               |
| traceId | str  | 追踪ID   |                                           |

### `data`成员对象

| 字段        | 类型 | 内容       | 备注       |
|-------------|------|------------|------------|
| id          | num  | 地址ID     |            |
| uid         | num  | 用户ID     |            |
| name        | str  | 收件人姓名 |            |
| tel         | str  | 电话号码   |            |
| province    | str  | 省份       |            |
| city        | str  | 城市       |            |
| district    | str  | 区         |            |
| fullAddress | str  | 完整地址   |            |
| isDefault   | bool | 是否默认地址 |            |
| createTime  | str  | 创建时间   |            |
| updateTime  | str  | 更新时间   |            |
| area        | str  | 地区       | 可选       |
| areaCode    | str  | 地区编码   | 可选       |
| postCode    | str  | 邮政编码   | 可选       |

## 示例

### 请求示例

```python
import requests

def get_address_by_accesstoken(access_token):
    url = "https://user-zone-api.kurogame.com/logistics/delivery-address/list.lg"
    headers = {
        "Host": "user-zone-api.kurogame.com",
        "Accept": "*/*",
        "Kr-Ver": "1.1.0",
        "Sec-Fetch-Site": "cross-site",
        "accessToken": access_token,
        "Accept-Language": "zh-Hans,zh-CN",
        "Sec-Fetch-Mode": "cors",
        "Origin": "https://web-static.kurobbs.com",
        "Referer": "https://web-static.kurobbs.com/",
        "User-Agent": "Mozilla/5.0 (iPhone; CPU iPhone OS 17_3 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) KuroGameBox/2.2.1",
        "Accept-Encoding": "gzip, deflate, br",
        "Connection": "keep-alive",
        "Content-Type": "application/x-www-form-urlencoded;charset=UTF-8",
        "Sec-Fetch-Dest": "empty"
    }
    try:
        res = requests.get(url, headers=headers)
        print(res.text)
    except Exception as e:
        print(f"获取地址失败: {e}")

# 示例调用
access_token = "替换为实际的 access_token"
get_address_by_accesstoken(access_token)
```

### 示例响应

```json
{
  "code": 200,
  "data": [
    {
      "id": 111111,
      "uid": 11111,
      "name": "Name",
      "tel": "15912345678",
      "province": "浙江省",
      "city": "天津市",
      "district": "崇明区",
      "fullAddress": "翻斗花园",
      "isDefault": false,
      "createTime": "1970-01-01T00:00:00",
      "updateTime": "1970-00-00T00:00:00",
      "area": null,
      "areaCode": null,
      "postCode": null
    }
  ],
  "traceId": "111111111111111"
}
```