# deal
## #610 雇员添加的交易中商品为下架商品  
### 前置条件
**服务已经运行，雇员身份**  
### 操作步骤  
* **步骤1：**   
下面条件中的商品已经下架，以：  
{  
  "shopID": "87245a458b45e",  
  "serialNumber": 201304231002,  
  "deviceID": "2584a5c4d5e4a4",  
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
      "name": "某下架商品",  
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

### 预期结果
* **预期1：**  
返回代码400，请求参数错误   
***   
  
## #611 雇员添加交易中会员结算的会员是过期会员  
### 前置条件
**服务已经运行，雇员身份**  
### 操作步骤  
* **步骤1：**   
下面条件中的会员已经过期，以：  
{  
  "shopID": "87245a458b45e",  
  "serialNumber": 201304231002,  
  "deviceID": "2584a5c4d5e4a4",  
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
        "name": "某过期会员",  
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
    
### 预期结果
* **预期1：**  
返回代码400，请求参数错误   
***  
## #612 雇员添加交易中会员结算的会员是暂停状态    
### 前置条件
**服务已经运行，雇员身份**  
### 操作步骤  
* **步骤1：**   
下面条件中的会员是暂停状态，以：  
{  
  "shopID": "87245a458b45e",  
  "serialNumber": 201304231002,  
  "deviceID": "2584a5c4d5e4a4",  
  "billID": "87245a458b347",  
  "quantity": 3,  
  "fee": 3000,  
  "memo": "",  
  "items": [{  
    "itemID": "12487dc8a56e",  
    "name": "面包",  
    "price": 1000,  
    "dealPrice": 1000,  
    "quantity": 3  
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
        "name": "停用会员",  
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
 
### 预期结果
* **预期1：**  
返回代码400，请求参数错误   
***   