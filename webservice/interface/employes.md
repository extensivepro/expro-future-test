# 雇员：employes
***
## 业主添加雇员
## 请求
### POST /employes
```json
{
  "username": "02584-1452-03",
  "password": "123456",
  "userID": "154d45bc478e475",
  "shopID": "154d454a578e475",
  "name": "张良",
  "role": "cashier",
  "jobNumber": 10086,
  "phone": "15211144452",
  "email": "hello@qq.com",
  "idcard": "320125632541254789",
  "createdAt": 1364804674255
}
```
### 必要项目
* `username`
* `password`
* `shopID`
* `name`
* `role`
* `jobNumber`
* `phone` 和 `email` 两者至少有一项
* `idcard`
* `createdAt`

### 备注
* `status` - 默认值为`active` (共3种状态`active`, `leave`, `suspend`)
* `role` - 允许值为：`owner`, `cashier`

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "154d4534a48e475",
  "username": "02584-1452-03",
  "password": "123456",
  "userID": "15423d4a578e475",
  "shopID": "154ac44a578e475",
  "name": "张良",
  "role": "cashier",
  "jobNumber": 10086,
  "phone": "15211144452",
  "email": "hello@qq.com",
  "idcard": "320125632541254789",
  "status": "suspend",
  "leaveAt": ,
  "createdAt": 1364804674255
}
```
### `400` - 请求参数错误
* `phone`和`email`同时为空
* `phone`, `email`格式不正确

### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 业主查询雇员信息
## 请求
### GET /employes
### 查询条件
* `name` - 雇员姓名；示例：?name=张良
* `role` - 雇员角色；示例：?role=cashier
* `jobNumber` - 雇员工号；示例：jobNumber=10086
* `phone` - 雇员手机号码；示例：?phone=15252522212
* `idcard` - 雇员身份证号码；示例：?idcard=320123199005123210
* `createdAt` - 雇员入职时间；示例：?{"createdAt":{"$gt":1000}}
* `leaveAt` - 雇员离职时间；示例：?{"leaveAt":{"$gt":1000}}
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20

### 默认项目
* `skip` - 0
* `limit` - 20

## 响应
### `200` - 成功返回
```json
[{
  "id": "154d4534a48e475",
  "username": "02584-1452-03",
  "password": "123456",
  "userID": "15423d4a578e475",
  "shopID": "154ac44a578e475",
  "name": "张良",
  "role": "cashier",
  "jobNumber": 10086,
  "phone": "15155522244",
  "email": "hello@qq.com",
  "idcard": "320123199005123210",
  "status": "suspend",
  "leaveAt": ,
  "createdAt": 1364804674255
}]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 业主更新雇员信息
## 请求
### PUT /employes/:id
```json
{
  "password": "123456",
  "name": "张良",
  "role": "cashier",
  "jobNumber": 10086,
  "phone": "15211144452",
  "email": "hello@qq.com",
  "idcard": "320125632541254789",
  "status": "active"
}
```
### 备注
* `userID` - 不能更新
* `shopID` - 不能更新
* `createdAt` - 不能更新
* `leaveAt` - 不能直接更新(雇员再次入职——离职时，服务端自动更新)

## 响应
### `200` - 成功返回
### `400` - 请求参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
***

## 雇员登录
## 请求
### POST /employes/login
```json
{
  "username": "02584-1452-03",
  "password": "123456"
}
```
### 必要项目
* `username`
* `password`

## 响应
### `200` - 成功登录
### `400` - 登录失败
***

## 雇员登出
## 请求
### POST /employes/logout

## 响应
### `200` - 成功登出
***

## 业主将雇员离职
## 请求
### PUT /employes/:id
```json
{
  "status": "leave"
}
```
### 必要项目
* `status`

## 响应
### `200` - 成功返回
### `400` - 请求参数错误
### `401` - 权限不够
* 只有业主有权限

### `409` - 请求冲突(目前：400)
