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
* 如果`amount`=`discountAmount`，`cashSettlement`与`memberSettlement`可以均为空
* `cashSettlement`与`memberSettlement`如果存在，则数据必须完备
* `payType` - `cashSettlement` -> `cash`；`memberSettlement` -> `prepay`
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
