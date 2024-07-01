

# 取access_token用来获取地址

更新时间: 24.7.1

## 请求地址

> https://api.kurobbs.com/encourage/order/beforeCreate

## 请求方式
POST

## 认证方式
token

## 请求头

| 字段            | 类型 | 内容  | 备注                                             |
| --------------- | ---- | ----- | ------------------------------------------------ |
| osversion       | str  | -     | Android                                          |
| devcode         | str  | -     | 设备码                 |
| countrycode     | str  | -     | CN                                               |
| ip              | str  |       | 10.0.2.233                                       |
| model           | str  |       | 2211133C                                         |
| source          | str  |       | android                                          |
| lang            | str  |       | zh-Hans                                          |
| version         | str  |       | 1.0.9                                            |
| versioncode     | str  |       | 1090                                             |
| token           | str  | token |                                                  |
| content-type    | str  |       | application/x-www-form-urlencoded; charset=utf-8 |
| accept-encoding | str  |       | gzip                                             |
| user-agent      | str  |       | okhttp/3.10.0                                    |

## 请求体

None

## 响应体

json

### 根对象

| 字段    | 类型 | 内容     | 备注                           |
| ------- | ---- | -------- | ------------------------------ |
| code    | num  | 返回值   | 220: token 失效<br />200: 成功 |
| success | bool | true     | token 有效时才有               |
| data    | arr  | 详细信息 | 成功时才有, 没绑定就是空数组   |

### `data`成员对象

| 字段      | 类型 | 内容         | 备注       |
| --------- | ---- | ------------ | ---------- |
| permitToken | str | accesstoken | uuid格式   |
| cprojectId | str | 未知         |            |

## 示例

### 请求

```python
import requests

def get_accesstoken_by_token(token, devcode):
    url = "https://api.kurobbs.com/encourage/order/beforeCreate"
    headers = {
        "Host": "api.kurobbs.com",
        "source": "ios",
        "lang": "zh-Hans",
        "User-Agent": "KuroGameBox/48 CFNetwork/1492.0.1 Darwin/23.3.0",
        "Ip": "127.0.0.1",
        "channelId": "1",
        "channel": "appstore",
        "distinct_id": "1111111111111111111111111111111111111111",
        "version": "2.2.1",
        "Content-Length": "0",
        "devCode": devcode,
        "token": token,
        "Connection": "keep-alive",
        "Accept-Language": "zh-CN,zh-Hans;q=0.9",
        "model": "iPhone15,2",
        "osVersion": "17.3",
        "Accept": "*/*",
        "Content-Type": "application/x-www-form-urlencoded; charset=utf-8",
        "Accept-Encoding": "gzip, deflate, br"
    }

    res = requests.post(url, headers=headers)
    try:
        access_token = res.json()["data"]["permitToken"]
        return access_token
    except Exception as e:
        print(res.json())
        print(f"Error: {e}")
        return None
```

### 示例响应

```json
{
  "code": 200,
  "data": {
    "permitToken": "b1a1a1a1-0c11-11aa-1111-d111111dac1",
    "projectId": "G111"
  },
  "msg": "请求成功",
  "success": true
}
```