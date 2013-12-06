# 添加交易

## 雇员添加交易
## 请求
### POST /add-deal
```json
{
  "shopID": "87245a458b45e",
  "serialNumber": 201304231002,
  "deviceID": "2584a5c4d5e4a4",
  "memo": "",
  "items": [{
		"id": "1546a4546b456c4",
    "dealPrice": 1000,
    "quantity": 3,
    "item": {
      "id": "1546a4546b456c4",
      "name": "老北京鸡肉卷",
      "price": 1000
    }
  }],
  "bill": {
    "billNumber": 1000012,
    "deviceID": "45454584a15d44e",
    "dealType": "deal",
    "amount": 18000,
    "discountAmount": 8000,
    "cashSettlement": {
      "serialNumber": 1000058,
      "amount": 500,
      "payType": "cash",
      "status": "closed"
    },
    "memberSettlement": {
      "serialNumber": 1000068,
      "amount": 5000,
      "payType": "prepay",
      "status": "closed",
      "payerAccount": {
        "name": "李四",
        "accountID": "454545467a4e45",
      }
    },
    "memo": "",
    "createdAt": 1366351844618
  },
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
* `items`
* `dealItem` -> `dealPrice`
* `dealItem` -> `quantity`
* `dealItem` -> `item` -> `id`
* `dealItem` -> `item` -> `name`
* `dealItem` -> `item` -> `price`
* `seller`
* `seller` -> `name`
* `seller` -> `employeeID`
* `bill` - 参见：[bill](bills.md)
* `createdAt`

### 备注
* `dealType` - `deal`
* `fee` - 以分为单位
* `fee` 和 `quantity` 由服务端计算生成
* `amount` - 以分为单位
* `discountAmount` - 以分为单位
* `payType` - `cash`或`prepay`
* `status` - `closed`或`unpaid`
* 如果`memberSettlement`存在，则`buyer`必须完整存在
* `createdAt` - 时间格式一律为整型值的秒数

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "message": "success",
  "dealID": "d79ff338d56c58c4",
  "billID": "b4e9cf25c09e28e0"
}
```

### `400` - 请求参数错误
* `itemID` - 查找不到item
* `shopID` - 查找不到shop
* `memberSettlement` -> `payerAccount`的`balance`不足

### `401` - 权限不够
* 非`cashier`或`owner`雇员

### `409` - 请求冲突(目前：400)
