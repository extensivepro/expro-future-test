# 商户：merchants
***

## 创建商户
## 请求
### POST /merchants
```json
{
  "code": "10000",
  "name": "卡罗酒吧",
  "fullName": "南京卡罗酒吧",
  "weixin": {
    "originID":"gh_af0c5d6c7b66"  
  },
  "telephone": "02551234567",
  "email": "kaluojiuba@qq.com",
  "address": "江宁区胜太路",
  "zip": "211521",
  "status": "open"
}
```
### 必要项目
* `code`
* `name`
* `fullName`
* `telephone` - `email`：两者至少有一个
* `createdAt`

### 默认项目
* `status` - "open" 。(共3种状态`open`, `suspend`, `closed`)

### 备注
* `code` - 全局唯一

## 响应
### `201` - 添加成功(暂时：200)
```json
{
  "address": "jl",
  "createdAt": 1386235335,
  "email": "",
  "fullName": "泛盈信息科技有限公司",
  "newestDeviceCode": 100001,
  "name": "泛盈科技",
  "owner": {
    "createdAt": 1386235335,
    "displayName": "泛盈科技运营",
    "email": "owner@fankahui.com",
    "id": "af968c00fcaf8b0a",
    "idcard": "432828198307052525",
    "male": true,
    "name": "泛盈科技运营",
    "phone": "18912345678",
    "roles": [
      "user"
    ],
    "username": "18912345678"
  },
  "shopIDs": [
    "903d6f6ce857a9eb"
  ],
  "pointRule": {
    "newMember": {
      "type": "fixed",
      "amount": "100"
    },
    "consumption": {
      "type": "ratio",
      "ratio": "1"
    },
    "referrer": {
      "type": "fixed",
      "amount": "100"
    }
  },
  "weixin": {
    "originID": "gh_af0c5d6c7b65",
    "devToken": {
      "appid": "wxdff210e6548a2eab",
      "secret": "66333b7b129109dc145d5b16330f1c9a"
    }
  },
  "status": "open",
  "telephone": "02586861234",
  "zip": ""
}
```
#### 备注
`shopIDs` - 所属商店的ID集合  
`itemTags` - 商品的标签集合  
`pointRule` - 积分规则，有定额和比例奖励两张类型  
  - `.newMember` - 新会员积分奖励，定额积分奖励  
  - `.comsumption` - 消费将来，然消费额兑换比例计算  
  - `.referrer` - 推荐积分奖励，定额奖励  

### `400` - 请求参数错误
* 店铺重名
* 业主身份证缺失
* `email`和`telephone`同时为空
* `code`已经存在
* `weixin.originID` - exist originID of weixin

### `401` - 权限不够
### `409` - 请求冲突(暂时：400)
***

## 业主更新商户信息
## 请求
### PUT /merchants/:id
```json
{
  "weixin": {
    "originID":"gh_af0c5d6c7b66"  
  },
  "logo":{
    id:"abc123 is LogoID"
    name: "file name"
  },
  "address": "江宁区胜太路",
  "telephone": "02551234567",
  "zip": "211521",
  "email": "kaluojiuba@qq.com",
  "status": "open"
}
```
### 备注
* `code` - 不能更新
* `name` - 不能更新
* `fullName` - 不能更新
* `createdAt` - 不能更新
* `shopIDs` - 不能由客户端请求更新，由服务器根据相关操作处理(比如：业主新开店)

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
* `telephone`或`email`格式错误
* 更换业主时，新业主身份证缺失
* `weixin.originID` - exist originID of weixin

### `401` - 权限不够
### `409` - 请求冲突(暂时：400)

## 更新商户商品的标签
## 请求
### PUT /merchants/:id
```json
{
	"itemTags": {$pushAll: ['凉菜', '炒菜']}
}
```

#### 备注
`$push` - 新增一个
`$pushAll` - 新增多个
`$pull` - 清除一个
`$pullAll` - 清除多个

## 响应
### `200` - 成功
### `401` - 权限不够
