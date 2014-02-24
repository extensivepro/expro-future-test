# 库存：skus
***

## 雇员新增库存
## 请求
### POST /skus
```json
{
  "shopID": "87245a458b45e",
  "itemID": "15145a458b45e",
  "name": "老北京鸡肉卷",
  "quantity": 100,
  "operator": {
    "employeeID": "524a5a458b45e",
    "name": "张三"
  },
  "sumPrice": 100000,
  "price": 1000,
  "createdAt": 1366340211946,
  "type": "add"
}
```
### 必要项目
* `shopID`
* `itemID`
* `quantity` - 正数
* `operator` -> `employeeID`
* `sumPrice` - 总价
* `price` - 单价
* `createdAt`
* `type` - `add`

### 备注
* `quantity` - 只允许为正
* `createdAt` - 时间格式一律为整型值的秒数
* `type` `add` - 进货

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "56564455a54c45e",
  "shopID": "87245a458b45e",
  "itemID": "15145a458b45e",
  "name": "老北京鸡肉卷",
  "quantity": 100,
  "operator": {
    "employeeID": "524a5a458b45e",
    "name": "张三"
  },
  "sumPrice": 100000,
  "price": 1000,
  "createdAt": 1366340211046,
  "type": "add"
}
```
### `400` - 请求参数错误
* `quantity` 为 `0`
* `itemID`查找不到item
* `shopID`查找不到shop


### `401` - 权限不够
* 非`商店雇员`
* `employeeID`查找不到employee

### `409` - 请求冲突(目前：400)
***

## 雇员减少库存
## 请求
### POST /skus
```json
{
  "shopID": "87245a458b45e",
  "itemID": "15145a458b45e",
  "name": "老北京鸡肉卷",
  "quantity": 100,
  "operator": {
    "employeeID": "524a5a458b45e",
    "name": "张三"
  },
  "sumPrice": 100000,
  "price": 1000,
  "createdAt": 1366340211946,
  "type": "sub"
}
```
### 必要项目
* `shopID`
* `itemID`
* `quantity` - `正数`
* `operator` -> `employeeID`
* `sumPrice` - 总价
* `price` - 单价
* `createdAt`
* `type` - `sub`

### 备注
* `type` `sub` - 出货


## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "56564455a54c45e",
  "shopID": "87245a458b45e",
  "itemID": "15145a458b45e",
  "name": "老北京鸡肉卷",
  "quantity": 100,
  "operator": {
    "employeeID": "524a5a458b45e",
    "name": "张三"
  },
  "sumPrice": 100000,
  "price": 1000,
  "createdAt": 1366340211946,
  "type": "sub"
}
```
### `400` - 请求参数错误
* `quantity` 为 `0`
* `itemID`查找不到item
* `shopID`查找不到shop

### `401` - 权限不够
* 非`商店雇员`
* `employeeID`查找不到employee

### `409` - 请求冲突(目前：400)
***

## 雇员查询库存
## 请求
### GET /skus
### 查询条件
* `itemID` - 商品ID；示例：?itemID=87245a458b45e
* `shopID` - 商店ID；示例：?shopID=15145a458b45e
* `name` - 商品名称；示例：?name=老北京鸡肉卷
* `createdAt` - 库存创建时间；示例：?{"createdAt":{"$gt":1000}}
* `quantity` - 进出货数量；示例：?{"quantity":{"$lt":1000}}
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20

### 默认项目
* `skip` - 0
* `limit` - 20

## 响应
###`200` - 成功返回
```json
[{
  "id": "56564455a54c45e",
  "shopID": "87245a458b45e",
  "itemID": "15145a458b45e",
  "name": "老北京鸡肉卷",
  "quantity": 100,
  "operator": {
    "employeeID": "524a5a458b45e",
    "name": "张三"
  },
  "sumPrice": 100000,
  "price": 1000,
  "createdAt": 1366340211046,
  "type": "add"
}]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* 非`商店雇员`

### `409` - 请求冲突(目前：400)
