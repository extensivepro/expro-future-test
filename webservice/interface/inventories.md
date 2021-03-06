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
* `sinceAt` 起始时间
* `createdAt` 截至时间 同时也是盘点时间
* `agent` 盘点人员
* `agent` -> `name` 盘点人员姓名
* `agent` -> `id` 盘点人员 id
* `items` 某商品的盘点记录(inventoryItem)
* `items` -> `id` 客户端生成的 inventoryItem 的 id
* `items` -> `item` 对应的商品
* `items` -> `item` ->  `id` 商品 id
* `items` -> `item` -> `name` 商品名

###响应
####`201` - 添加成功(目前：200)
```json
{
  "id": "adasavagqtfvasv"
}
```

#### `400` - 请求参数错误
* `shopID is required`
* `sinceAt is required`
* `createdAt is required`
* `agent`
    * `is required`
    * `.name is required`
    * `.id is required`
* `items`
    * `is required`
    * `.id is required`
    * `.id is duplicated`
    * `.inputQuantity is required`
    * `.outputQuantity is required`
    * `.priorQuantity is required`
    * `.realQuantity is required`
    * `.item is required`
    * `.item.id is required`
    * `.item.name is required`

#### `401` - 权限不够
* 非`cashier`或`owner`雇员

#### `409` - 请求冲突(目前：400)

##雇员查询盘点
###请求 GET /inventories
#### QueryString
* `shopID` - 锁定商店
* `createdAt` - 锁定盘点

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
