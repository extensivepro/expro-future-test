# 结算账单：bills
***

## 添加结算账单
## 请求
### POST /bills
```json
{
  "billNumber": 1000012,
  "deviceID": "45454584a15d44e",
  "dealID": "45647478a464d45",
  "dealType": "deal",
  "amount": 18000,
  "discountAmount": 8000,
  "cashSettlement": {
    "serialNumber": 1000058,
    "amount": 5000,
    "payType": "cash",
    "status": "closed"
  },
  "memberSettlement": {
    "serialNumber": 1000068,
    "amount": 5000,
    "payType": "prepay",
    "status": "closed",
    "payerAccount": {
      "name": "张三",
      "accountID": "454545467a4e45",
    }
  },
  "memo": "",
  "agentID": "45647478a464d45",
  "shopID": "45647478a464d45",
  "merchantID": "45647478a464d45",
  "createdAt": 1366351844618
}
```
### 必要项目
* `billNumber`
* `deviceID`
* `dealID`
* `dealType`
* `amount`
* `discountAmount`
* `createdAt`

### 备注
* `dealType` 
	* `deal` - 销售
	* `return` - 退货
	* `prepay` - 充值，dealID为空
	* `writedown` - 减记储值，dealID为空
* `amount` - 以分为单位
* `discountAmount` - 以分为单位，不能为负值
* 如果`amount`==`discountAmount`，`cashSettlement`与`memberSettlement`可以均为空
* `cashSettlement`与`memberSettlement`如果存在，则数据必须完备
* `cashSettlement` - 现金结算
  * `payType` - `cash` 现金
* `memberSettlement` - 会员账户结算
  * `payType` -`prepay` 会员储值
* `status` - `closed`或`unpaid`(`cashSettlement`的`status`由客户端上传，`memberSettlement`的`status`由服务端设置)
* `memberSettlement`中，`deal` -> `payerAccount`扣款，`return` -> `payeeAccount`充值，两者必仅有其一
* `createdAt` - 时间格式一律为整型值的秒数
* `merchantID` - 商户的ID
* `shopID` - 商店的ID
* `agentID` - 经手人ID

## 响应
### `201` - 添加成功(目前：200)
```json
{
  "id": "32445a458b45e",
  "billNumber": 1000012,
  "deviceID": "45454584a15d44e",
  "dealID": "45647478a464d45",
  "dealType": "deal",
  "amount": 18000,
  "discountAmount": 8000,
  "cashSettlement": {
    "serialNumber": 1000058,
    "amount": 5000,
    "payType": "cash",
    "status": "closed"
  },
  "memberSettlement": {
    "serialNumber": 1000068,
    "amount": 5000,
    "payType": "prepay",
    "status": "closed",
    "payerAccount": {
      "name": "张三",
      "accountID": "454545467a4e45",
    }
  },
  "memo": "",
	"agentID": "45647478a464d45",
	"shopID": "45647478a464d45",
	"merchantID": "45647478a464d45",
  "createdAt": 1366351844618
}
```
### `400` - 请求参数错误
* `memberSettlement` -> `payerAccount`的`balance`不足

### `401` - 权限不够
* 非`cashier`或`owner`雇员

### `409` - 请求冲突(目前：400)
***

## 查询结算账单
## 请求
### GET /bills

* `withall` - 包含deal、return的全部信息    

## 响应
### `200` - 成功返回
```json
[{
  "id": "32445a458b45e",
  "billNumber": 1000012,
  "deviceID": "45454584a15d44e",
  "dealID": "45647478a464d45",
  "dealType": "deal",
  "amount": 18000,
  "discountAmount": 8000,
  "cashSettlement": {
    "serialNumber": 1000058,
    "amount": 5000,
    "payType": "cash",
    "status": "closed"
  },
  "memberSettlement": {
    "serialNumber": 1000068,
    "amount": 5000,
    "payType": "prepay",
    "status": "closed",
    "payerAccount": {
      "name": "张三",
      "accountID": "454545467a4e45",
    }
  },
  "deal":{
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
    "id": "f649a6f4622a0aa6"
  },
  "return": {
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
    "deal":{
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
      "id": "f649a6f4622a0aa6"
    },
    "createdAt": 1366351844618
  }
  "memo": "",
  "createdAt": 1366351844618
}]
```
### `204` - 无内容(目前：200)
### `304` - not modified(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* 非`cashier`或`owner`雇员

### `409` - 请求冲突(目前：400)
