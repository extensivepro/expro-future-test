# 退货：returns
***

## 雇员查询退货
## 请求
### GET /returns
### 查询条件
* `dealSerialNumber` - 根据先前交易的流水单号查询；示例：?dealSerialNumber=201303231009
* `shopID` - 根据商店ID查询商店退货；示例：?shopID=87245a458b45e
* `serialNumber` - 根据流水编号查询退货；示例：?serialNumber=201304231002
* `deviceID` - 根据设备编号查询退货；示例：?deviceID=2584a5c4d5e4a4
* `createdAt` - 根据退货时间查询退货；示例：?{"createdAt":{"$gt":1000}}
* `quantity` - 根据退货总数量查询退货；示例：?{"quantity":{"$lt":1000}}
* `fee` - 根据退款金额查询退货；示例：?{"fee":{"$lt":10025}}
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20
* `id` - 根据`id`进行查询；示例：/32445a458b45e

#### 注：当用id查询时，得到的是单个json而非json数组，且查询不到时返回`404`
### 默认项目
* `skip` - 0
* `limit` - 20

## 响应
### `200` - 成功返回(非`id`查询)
```json
[{
  "id": "32445a458b45e",
  "shopID": "87245a458b45e",
  "dealID": "32445a458b45e",
  "billID": "45465a454d454",
  "dealSerialNumber": 201303231009,
  "serialNumber": 201304231038,
  "deviceID": "254456784d5e4a4",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [{
    "dealPrice": 1000,
    "dealQuantity": 3,
    "returnPrice": 1000,
    "returnQuantity": 3,
    "sku": {
      "skuID": "468754a4534e4b5",
      "shopID": "1548a4345d5e5a5",
      "itemID": "1546a4546b456c4",
      "name": "老北京鸡肉卷",
      "price": 1000
    }
  }],
  "operator": {
    "name": "张三",
    "employeeID": "124ac87da56e"
  },
  "customer": {
    "memberID": "12487dc8a56e",
    "code": "123456789",
    "name": "李四"
  },
  "createdAt": 1366351844618
}]
```
### `200` - 成功返回(`id`查询)
```json
{
  "id": "32445a458b45e",
  "shopID": "87245a458b45e",
  "dealID": "32445a458b45e",
  "billID": "45465a454d454",
  "dealSerialNumber": 201303231009,
  "serialNumber": 201304231038,
  "deviceID": "254456784d5e4a4",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [{
    "dealPrice": 1000,
    "dealQuantity": 3,
    "returnPrice": 1000,
    "returnQuantity": 3,
    "sku": {
      "skuID": "468754a4534e4b5",
      "shopID": "1548a4345d5e5a5",
      "itemID": "1546a4546b456c4",
      "name": "老北京鸡肉卷",
      "price": 1000
    }
  }],
  "operator": {
    "name": "张三",
    "employeeID": "124ac87da56e"
  },
  "customer": {
    "memberID": "12487dc8a56e",
    "code": "123456789",
    "name": "李四"
  },
  "createdAt": 1366351844618
}
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* 非`商店雇员`

### `409` - 请求冲突(目前：400)
***

## 添加退货(internal api)
## 请求
### POST /returns
```json
{
  "shopID": "87245a458b45e",
  "dealID": "32445a458b45e",
  "billID": "45465a454d454",
  "dealSerialNumber": 201303231009,
  "serialNumber": 201304231038,
  "deviceID": "254456784d5e4a4",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [{
    "dealPrice": 1000,
    "dealQuantity": 3,
    "returnPrice": 1000,
    "returnQuantity": 3,
    "sku": {
      "skuID": "468754a4534e4b5",
      "shopID": "1548a4345d5e5a5",
      "itemID": "1546a4546b456c4",
      "name": "老北京鸡肉卷",
      "price": 1000
    }
  }],
  "operator": {
    "name": "张三",
    "employeeID": "124ac87da56e"
  },
  "customer": {
    "memberID": "12487dc8a56e",
    "code": "123456789",
    "name": "李四"
  },
  "createdAt": 1366351844618
}
```
### 必要项目
* `shopID`
* `dealID`
* `billID`
* `serialNumber`
* `deviceID`
* `quantity`
* `fee`
* `items`
* `item` -> `dealPrice`
* `item` -> `quantity`
* `item` -> `returnPrice`
* `item` -> `returnQuantity`
* `item` `sku` -> `skuID`
* `item` `sku` -> `shopID`
* `item` `sku` -> `itemID`
* `item` `sku` -> `name`
* `item` `sku` -> `price`
* `operator`
* `operator` -> `name`
* `operator` -> `employeeID`
* `createdAt`

### 备注
* `dealID`为之前交易的`id`
* `serialNumber`与`deviceID`，并非之前交易的`serialNumber`与`deviceID`
* `createdAt`的时间格式一律为整型值的秒数

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "32445a458b45e",
  "shopID": "87245a458b45e",
  "dealID": "32445a458b45e",
  "billID": "45465a454d454",
  "dealSerialNumber": 201303231009,
  "serialNumber": 201304231038,
  "deviceID": "254456784d5e4a4",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [{
    "dealPrice": 1000,
    "dealQuantity": 3,
    "returnPrice": 1000,
    "returnQuantity": 3,
    "sku": {
      "skuID": "468754a4534e4b5",
      "shopID": "1548a4345d5e5a5",
      "itemID": "1546a4546b456c4",
      "name": "老北京鸡肉卷",
      "price": 1000
    }
  }],
  "operator": {
    "name": "张三",
    "employeeID": "124ac87da56e"
  },
  "customer": {
    "memberID": "12487dc8a56e",
    "code": "123456789",
    "name": "李四"
  },
  "createdAt": 1366351844618
}
```
### `400` - 请求参数错误
* `quantity` - 为 `负值` 或 `0`
* `fee` - 为 `负值` 或 `0`
* `payType` - 非 `cash` 或 `prepay`
* `itemID` - 查找不到item
* `shopID` - 查找不到shop

### `401` - 权限不够
* 非`internal`

### `409` - 请求冲突(目前：400)
