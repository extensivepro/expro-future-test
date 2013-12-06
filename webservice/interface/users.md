# 用户 - Users
***

## 用户注册
## 请求
### POST /users
```json
{
  "name": "张三真名",
  "displayName": "张业主",
  "phone": "1891234578",
  "idcard": "320103197901011234",
  "male": true,
  "birthday": "19790101",
  "email": "18912345678@189.cn",
  "username": "18912345678",
  "password": "123456"
}
```
### 必要项目
* `username`
* `passowrd`
* `phone` - 与 **email** 有其一即可
* `email` - 与 __phone__ 有其一即可

### 默认项目
* `male` - true

### 备注
* `roles` - 初始值：["user"]
* `roles` - 由服务器根据业务流程自动增加，共4种值：`user`, `employee`, `owner`, `administrator`

## 响应
### `201` - 创建成功(目前：200)
```json
{
  "id": "154d4534a48e475",
  "name": "张三真名",
  "displayName": "张业主",
  "phone": "1891234578",
  "idcard": "320103197901011234",
  "male": true,
  "birthday": "19790101",
  "email": "18912345678@189.cn",
  "username": "18912345678",
  "createdAt": 1367461659852
}
```
### `400` - 请求参数错误
### `409` - 用作用户名的电话号码或电子邮件已经被注册过。(目前：400)
***

## 用户登录
## 请求
### POST /users/login
```json
{
  "username": "18912345678",
  "password": "123456"
}
```
### 必要项目
* `username`
* `password`

## 响应
### `200` - 登录成功
### `400` - 登录失败
***

## 用户登出
## 请求
### POST /users/logout
## 响应
### `200` - 登出成功
***

## 以`id`查询一个用户
## 请求
### GET /users/:id
### 授权角色
* 用户本人
* 泛商汇管理员
* 内部调用

## 响应
### `200` - 成功
```json
{
  "id": "154d4534a48e475",
  "username": "18912345678",
  "displayName": "张业主",
  "phone": "1891234578",
  "idcard": "320103197901011234",
  "male": true,
  "birthday": "19790101",
  "email": "18912345678@189.cn",
  "roles": ["user"]
}
```
### `401` - 权限不够
***

## 查询一批用户
## 请求
### GET /users
### 授权角色
* 泛商汇管理员
* 内部调用

### 查询条件
* `name` - 姓名；示例：?name=张良
* `phone` - 手机号码；示例：?phone=15252522212
* `idcard` - 身份证号码；示例：?idcard=320123199005123210
* `createdAt` - 注册时间；示例：?{"createdAt":{"$gt":1000}}
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20

### 默认项目
* `skip` - 0  
* `limit` - 20  

## 响应
### `200` - 成功
```json
[{
  "id": "154d4534a48e475",
  "username": "18912345678",
  "name": "张三真名",
  "displayName": "张业主",
  "phone": "1891234578",
  "idcard": "320103197901011234",
  "male": true,
  "birthday": "19790101",
  "email": "18912345678@189.cn",
  "roles": ["user"]
}]
```
### `401` - 权限不够
***

## 更新用户信息
## 请求
### PUT /users/:id
```json
{
  "password": "123456",
  "name": "张三真名",
  "displayName": "张业主",
  "phone": "1891234578",
  "email": "18912345678@189.cn",
  "idcard": "320103197901011234",
  "male": true,
  "birthday": "19790101"
}
```
### 备注
* `createdAt` - 不能更新
* `roles` - 不能更新，只能由服务器根据相关操作更新(比如：用户创建商户)

## 响应
### `200` - 更新成功
### `400` - 参数错误
### `401` - 权限不够
### `409` - 请求冲突(目前：400)
