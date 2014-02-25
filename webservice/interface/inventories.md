盘点: Inventories
===

##雇员添加盘点

###请求 POST /inventories
```json
{
  "shopID": "87245a458b45e",
  "sinceAt": 1388505600,
  "createdAt": 1391184000,
  "agent": {
    "name": "???",
    "id": "124ac87da56e"
  },
  "items": [
    {
      "id": "abcdefg",
      "inputQuantity": 0,
      "outputQuantity": 0,
      "priorQuantity": 200,
      "realQuantity": 198,
      "memo": "unknown",
      "item": {
        "id": "1546a4546b456c4",
        "name": "老北京鸡肉卷"
      }
    }
  ]
}
```
####必要项目
* `shopID` 指明商店
* `beginDate`
* `endDate` - 截至时间 同时也是盘点时间
* `employeeID`
* `items`
* `items` -> `inputQuantity` 盘点账期入库数量
* `items` -> `outputQuantity` 盘点账期出库数量
* `items` -> `priorQuantity` 上次盘点剩余数量
* `items` -> `realQuantity` 本次盘点剩余数量
* `items` -> `memo` 备忘
* `items` -> `itemID` 对应的商品

###响应
####`201` - 添加成功(目前：200)
```json
{
  "message": "success",
  "inventoryID": "adasavagqtfvasv"
}
```

#### `400` - 请求参数错误
* `itemID` - 查找不到 item
* `shopID` - 查找不到 shop
* `employeeID` - 查找不到 employee

#### `401` - 权限不够
* 非`cashier`或`owner`雇员

#### `409` - 请求冲突(目前：400)

##雇员查询盘点
###请求 GET /inventories
#### QueryString
* `shopID` - 锁定商店
* `endDate` - 锁定盘点

###响应
####`200` - 成功返回
```json
{
  "id": "adasavagqtfvasv",
  "shopID": "87245a458b45e",
  "sinceAt": 1388505600,
  "createdAt": 1391184000,
  "agent": {
    "name": "???",
    "id": "124ac87da56e"
  },
  "items": [
    {
      "id": "abcdefg",
      "inputQuantity": 0,
      "outputQuantity": 0,
      "priorQuantity": 200,
      "realQuantity": 198,
      "memo": "unknown",
      "item": {
        "id": "1546a4546b456c4",
        "name": "老北京鸡肉卷"
      }
    }
  ]
}
```
#### `204` - 无内容(目前：200)
#### `304` - not modified(目前：200)
#### `400` - 请求参数错误
#### `401` - 权限不够
* 非`商店雇员`

### `409` - 请求冲突(目前：400)
