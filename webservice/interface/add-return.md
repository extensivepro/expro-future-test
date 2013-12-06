# 添加退货

## 雇员添加退货
## 请求
### POST /add-return
```json
{
  "shopID": "87245a458b45e",
  "dealID": "32445a458b45e",
  "dealSerialNumber": 201303231009,
  "serialNumber": 201304231038,
  "deviceID": "254456784d5e4a4",
  "quantity": 3,
  "fee": 3000,
  "memo": "",
  "items": [{
		"id": "1546a4546b456c4",
    "returnPrice": 1000,
    "quantity": 3,
    "dealItem": {
      "id": "1546a4546b456c4",
      "dealPrice": 1000,
	    "quantity": 3,
			"item": {
				"id": "1546a4546b456c4",
	      "name": "老北京鸡肉卷",
	      "price": 1000
			}
    }
  }],
  "bill": {
    "billNumber": 1000012,
    "deviceID": "45454584a15d44e",
    "dealType": "return",
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
      "payeeAccount": {
        "name": "张三",
        "accountID": "454545467a4e45",
      }
    },
    "memo": "",
    "createdAt": 1366351844618
  },
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
* `serialNumber`
* `deviceID`
* `quantity`
* `fee`
* `items`
* `returnItem` -> `dealPrice`
* `returnItem` -> `quantity`
* `returnItem` -> `returnPrice`
* `returnItem` -> `returnQuantity`
* `returnItem` -> `item` -> `id`
* `returnItem` -> `item` -> `name`
* `returnItem` -> `item` -> `price`
* `operator`
* `operator` -> `name`
* `operator` -> `employeeID`
* `bill` - 参见：[bill](bills.md)
* `createdAt`

### 备注
* `dealID` - 之前交易的`id`
* `serialNumber`与`deviceID`，并非之前交易的`serialNumber`与`deviceID`
* `createdAt` - 时间格式一律为整型值的秒数
* `dealType` - `return`
* `amount` - 以分为单位
* `payType` - `cash`或`prepay`
* `status` - `closed`或`unpaid`
* `createdAt` - 时间格式一律为整型值的秒数

## 响应
### `201` - 添加成功(目前：200)

### `400` - 请求参数错误
* `quantity` - 为`负值`或`0`
* `fee` - 为`负值`或`0`
* `payType` - 非`cash`或`prepay`
* `itemID` - 查找不到item
* `shopID` - 查找不到shop

### `401` - 权限不够
* 非`cashier`或`owner`雇员

### `409` - 请求冲突(目前：400)
