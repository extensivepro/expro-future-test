# 交易：deals
***

## 雇员查询交易
## 请求
### GET /deals
### 查询条件
* `shopID` - 根据商店ID查询商店交易；示例：?shopID=87245a458b45e
* `serialNumber` - 根据流水编号查询交易；示例：?serialNumber=201304231002
* `deviceID` - 根据设备编号查询交易；示例：?deviceID=2584a5c4d5e4a4
* `createdAt` - 根据交易时间查询交易；示例：?{"createdAt":{"$gt":1000}}
* `quantity` - 根据交易总数量查询交易；示例：?{"quantity":{"$lt":1000}}
* `fee` - 根据交易金额查询交易；示例：?{"fee":{"$lt":10025}}
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20
* `withall` - 查询返回包括device和bill的详细信息；示例：?withall=1

### 默认项目
* `skip` - 0
* `limit` - 20

## 响应
### `200` - 成功返回
```json
[
  {
    "billID": "8d216b34db1628ed",
    "createdAt": 1387529885,
    "deviceCode": 1,
    "deviceID": "3E7C2A07-D5AD-429F-9801-9C941A19655D",
    "fee": 379000,
    "items": [
      {
        "item": {
          "id": "221f47e56134f82c",
          "name": "iPhone 4S",
          "price": 379000
        },
        "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
        "dealPrice": 379000,
        "quantity": 1
      }
    ],
    "quantity": 1,
    "seller": {
      "employeeID": "6d97c241f56a8873",
      "name": "新业主"
    },
    "serialNumber": 1000003,
    "shopID": "2834910281d26a76",
    "id": "f649a6f4622a0aa6",
    "bill": {
      "billNumber": 1000004,
      "deviceID": "3E7C2A07-D5AD-429F-9801-9C941A19655D",
      "dealID": "f649a6f4622a0aa6",
      "dealType": "deal",
      "amount": 379000,
      "discountAmount": 0,
      "cashSettlement": {
        "status": "closed",
        "serialNumber": 409222694,
        "settledAt": "1387529895",
        "amount": 380000,
        "payType": "cash"
      },
      "createdAt": 1387529892,
      "agentID": "6d97c241f56a8873",
      "shopID": "2834910281d26a76",
      "id": "8d216b34db1628ed"
    },
    "device": {
      "code": 1,
      "createdAt": 1386926594,
      "shop": {
        "id": "146e1ae24ff818e8",
        "merchant": {
          "id": "e20dccdf039b3874",
          "owner": {
            "id": "9f4b394aa96de9d2"
          }
        }
      },
      "udid": "3E7C2A07-D5AD-429F-9801-9C941A19655D",
      "updateAt": 1388033986.044,
      "id": "08da4c99af30c84f"
    }
  }
]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* 非`商店雇员`

### `409` - 请求冲突(目前：400)
***

## 添加交易(internal api)
## 请求
### POST /deals
```json
{
  "shopID": "87245a458b45e",
  "serialNumber": 201304231002,
  "deviceID": "2584a5c4d5e4a4",
  "billID": "87245a458b347",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [
    {
      "dealPrice": 1000,
      "quantity": 3,
      "item": {
        "id": "1546a4546b456c4",
        "name": "老北京鸡肉卷",
        "price": 1000
      }
    }
  ],
  "seller": {
    "name": "张三",
    "employeeID": "124ac87da56e"
  },
  "buyer": {
    "memberID": "12487dc8a56e",
    "code": "123456789",
    "name": "李四"
  },
  "createdAt": 1366351844618
}
```
### 必要项目
* `shopID`
* `serialNumber`
* `deviceID`
* `billID`
* `quantity`
* `fee`
* `items`
* `item` -> `dealPrice`
* `item` -> `quantity`
* `item` `sku` -> `skuID`
* `item` `sku` -> `shopID`
* `item` `sku` -> `itemID`
* `item` `sku` -> `name`
* `item` `sku` -> `price`
* `seller`
* `seller` -> `name`
* `seller` -> `employeeID`
* `createdAt`

### 备注
* `createdAt` - 时间格式一律为整型值的秒数

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "32445a458b45e",
  "shopID": "87245a458b45e",
  "serialNumber": 201304231002,
  "deviceID": "2584a5c4d5e4a4",
  "billID": "87245a458b347",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [{
    "dealPrice": 1000,
    "quantity": 3,
    "sku": {
      "skuID": "468754a4534e4b5",
      "shopID": "1548a4345d5e5a5",
      "itemID": "1546a4546b456c4",
      "name": "老北京鸡肉卷",
      "price": 1000
    }
  }],
  "seller": {
    "name": "张三",
    "employeeID": "124ac87da56e"
  },
  "buyer": {
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
* `itemID` - 查找不到item
* `shopID` - 查找不到shop

### `401` - 权限不够
* 非`internal`

### `409` - 请求冲突(目前：400)
