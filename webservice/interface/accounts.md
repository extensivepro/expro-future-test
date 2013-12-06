# 结算账号：accounts
***

## 添加结算账号(internal api)
## 请求
### POST /accounts
```json
{
  "ownerID": "1452147896a2e",
  "type": "member",
  "name": "张会员",
  "balance": 0,
  "createdAt": 1366351844618
}
```
### 必要项目
* `ownerID`
* `createdAt`

### 默认值
* `type` - `"member"`

### 初始值
* `balance` - `0`

### 备注
* `type` - 当前仅支持`"member"`
* `type`为`"member"`时，`ownerID`即`memberID`
* `balance`为储值金额，单位：`分`
* `createdAt` - 时间格式一律为整型值的秒数

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "32445a458b45e",
  "ownerID": "1452147896a2e",
  "type": "member",
  "name": "张会员",
  "balance": 0,
  "createdAt": 1366351844618
}
```
### `400` - 请求参数错误
### `401` - 权限不够
* 非`internal`

### `409` - 请求冲突(目前：400)
***

## 查询结算账号
## 请求
### GET /accounts

### 查询条件
* `ownerID` - 所有者ID；示例：?ownerID=1452147896a2e
* `type` - 账号类型；示例：?type=member
* `name` - 所有者名称；示例：?name=张会员
* `balance` - 账户余额；示例：?{"balance":{"$lt":1000000}}
* `createdAt` - 创建时间；示例：?{"createdAt":{"$gt":1366351000000}}

### 默认项目
* `skip` - 0
* `limit` - 20

## 响应
### `200` - 成功返回
```json
[{
  "id": "32445a458b45e",
  "ownerID": "1452147896a2e",
  "type": "member",
  "name": "张会员",
  "balance": 0,
  "createdAt": 1366351844618
}]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* `member`的结算账号可供`会员本人`或`所属商店雇员`查询

### `409` - 请求冲突(目前：400)
