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
  "id": "4545a454e454c4d45",
  "code": "10000",
  "name": "卡罗酒吧",
  "fullName": "南京卡罗酒吧",
  "address": "江宁区胜太路",
  "telephone": "02551234567",
  "zip": "211521",
  "email": "kaluojiuba@qq.com",
  "owner": {
    "id": "e8a69acd47baf94c",
    "displayName": "张业主",
    "phone": "1891234578",
    "idcard": "320103197901011234",
    "male": true,
    "birthday": "19790101",
    "email": "18912345678@189.cn",
  },
  "status": "open",
  "shopIDs": [],
  "itemTags": [],
  "createdAt": "1365402743500"
}
```
#### 备注
`shopIDs` - 所属商店的ID集合
`itemTags` - 商品的标签集合

### `400` - 请求参数错误
* 店铺重名
* 业主身份证缺失
* `email`和`telephone`同时为空
* `code`已经存在

### `401` - 权限不够
### `409` - 请求冲突(暂时：400)
***

## 业主更新商户信息
## 请求
### PUT /merchants/:id
```json
{
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