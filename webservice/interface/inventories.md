盘点: Inventories
===

##雇员添加盘点

###请求 POST /inventories
```json
{
  "shopID": "87245a458b45e",
  "createdAt": 1391184000,
  "beginDate": 1388505600,
  "endDate": 1391184000,
  "agent": {
    "name": "???",
    "employeeID": "124ac87da56e"
  },
  "items": [
    {
      "inQuantity": 0,
      "outQuantity": 0,
      "lastQuantity": 200,
      "realQuantity": 198,
      "reason": "unknown",
      "item": [
        {
          "id": "1546a4546b456c4",
          "name": "老北京鸡肉卷",
          "price": 1000
        }
      ]
    }
  ]
}
```
####必要项目
* `shopID` 指明商店
* `createdAt`
* `beginDate`
* `endDate`
* `agent`
* `agent` -> `employeeID`
* `items`
* `items` -> `inQuantity` 盘点账期入库数量
* `items` -> `outQuantity` 盘点账期出库数量
* `items` -> `lastQuantity` 上次盘点剩余数量
* `items` -> `realQuantity` 本次盘点剩余数量
* `items` -> `reason` 偏差原因
* `items` -> `item` -> `id` 对应的商品

###响应
####`201` - 添加成功(目前：200)
```json
{
  "message": "success",
  "inventoryID": "adasavagqtfvasv"
}
```

#### `400` - 请求参数错误
* `itemID` - 查找不到item
* `shopID` - 查找不到shop

#### `401` - 权限不够
* 非`cashier`或`owner`雇员

#### `409` - 请求冲突(目前：400)

##雇员查询盘点
###请求 GET /inventories
* `shopID` - 锁定商店
* `createdAt` - 锁定盘点

###响应
####`200` - 成功返回
```json
{
  "shopID": "87245a458b45e",
  "createdAt": 1391184000,
  "beginDate": 1388505600,
  "endDate": 1391184000,
  "agent": {
    "name": "???",
    "employeeID": "124ac87da56e"
  },
  "items": [
    {
      "inQuantity": 0,
      "outQuantity": 0,
      "lastQuantity": 200,
      "realQuantity": 198,
      "reason": "unknown",
      "item": [
        {
          "id": "1546a4546b456c4",
          "name": "老北京鸡肉卷",
          "price": 1000
        }
      ]
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
