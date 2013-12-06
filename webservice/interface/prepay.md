# 会员充值
***

## 雇员新增会员充值
## 请求
### POST /bills
```json
{
  "billNumber": 1222212,
  "deviceID": "1548796323a5e6",
  "dealType": "prepay",
  "amount": 30000,
  "discountAmount": 0,
  "cashSettlement": {
    "serialNumber": 1000013,
    "amount": 30000,
    "payType": "cash",
    "status": "closed"
  },
  "memberSettlement": {
    "serialNumber": 10000014,
    "amount": 30000,
    "payType": "prepay",
    "status": "closed",
    "payeeAccount": {
      "name": "李四",
      "accountID": "454545467a4e45"
    }
  },
  "memo": "",
  "createdAt": 1366351844618
}
```
### 必要项目
* billNumber
* deviceID
* dealType - `prepay`
* amount
* discountAmount
* cashSettlement
* memberSettlement
* createdAt

### 备注
* `createdAt` - 时间格式一律为整型值的秒数
* `fee`,`amount`,`discountAmount` - 以分为单位
* `status` - `closed`或`unpaid`

## 响应
### `201` - 添加成功(目前：200)
### `400` - 请求参数错误
### `401` - 权限不够
* 非`cashier`或`owner`雇员

### `409` - 请求冲突(目前：400)

## 雇员查询充值记录
* `查询账单` - 通过查询`dealType`为`prepay`的bill查询充值记录，参见：[bill](bills.md)
