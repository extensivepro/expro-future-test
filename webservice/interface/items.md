# 商品：items
***

## owner雇员新增商品
## 请求
### POST /items
```json
{
  "merchantID": "15425a25c2d25e2",
  "code": "123456",
  "mnemonicCode": "12-23",
  "name": "老北京鸡肉卷",
  "desc": "源自于老北京的经典美食",
  "price": 500,
  "status": "sale",
  "createdAt": 1365408771288
}
```
### 必要项目
* `merchantID`
* `code`
* `name`
* `price`
* `createdAt`

### 默认项目
* `status` - `"sale"`(有3种状态：`"sale"`，`"desale"`, `"remove"`)
* `商品`对所有商店开放

### 备注
* `code` - 商品编码
* `mnemonicCode` - 商品助记码
* `price` - 以分为单位
* `createdAt` - 时间格式一律为整型值的秒数
* 只有`owner雇员`可以添加、更新商品

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "1545a4548d4848c848e",
  "merchantID": "15425a25c2d25e2",
  "code": "123456",
  "mnemonicCode": "12-23",
  "name": "老北京鸡肉卷",
  "desc": "源自于老北京的经典美食",
  "price": 500,
  "tags": [],
  "images": [],
  "status": "sale",
  "createdAt": 1365408771288
}
```
### `400` - 请求参数错误
* `price`为负值

### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 查询商品
## 请求
### GET /items
### 查询条件
* `code` - 商品编码；示例：?code=123456
* `mnemonicCode` - 商品助记码；示例：mnemonicCode=12-23
* `name` - 商品名称；示例：?name=老北京鸡肉卷
* `createdAt` - 商品新增时间；示例：?{"createdAt":{"$gt":1000}}
* `status` - 商品状态；示例：?status=sale
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20
* `merchantID` - 商品所属商户；？merchantID=234a3cd3c86b2a29
* `tags` - 商品所包含的标签；?{tags:{$in:["phone"]}}

### 默认项目
* `skip` - 0
* `limit` - 10

## 响应
### `200` - 成功返回
```json
[
  {
    "tags": [
      "phone"
    ],
    "merchantID": "c82e1197884d8806",
    "code": "10002000",
    "mnemonicCode": "1020",
    "name": "iPhone 5",
    "price": 450000,
    "desc": "演示商品2",
    "status": "sale",
    "createdAt": 1371570826,
    "model": "港行官方标配黑色三网通行",
    "id": "234a3cd3c86b2a29"
  }
]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* 非`owner雇员`

### `409` - 请求冲突(目前：400)
***

## owner雇员更新商品
## 请求
### PUT /items/:id
```json
{
  "code": "234567",
  "mnemonicCode": "23-45",
  "name": "老北京鸡肉卷",
  "desc": "源自于老北京的经典美食",
  "price": 500,
  "status": "sale"
}
```
## 响应
### `200` - 更新成功
### `400` - 请求参数错误
* `price`为负值

### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## owner雇员下架商品
## 请求
### PUT /items/:id
```json
{
  "status": "desale"
}
```
### 必要项目
* `status` - `"desale"`

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## owner雇员上架商品
## 请求
### PUT /items/:id
```json
{
  "status": "sale"
}
```
### 必要项目
* `status` - `"sale"`

## 响应
### `200` - 更新成功
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
