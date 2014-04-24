# 订单：orders
***

* 订单不等同于交易单，其可以作为交易单的来源，多条订单可以汇总形成一条交易单。
* 适用于交易环节持续时间较长的业态，例如餐饮服务业等。


订单状态|顾客||门店|备注  
:--|:--:|:--:|--:|:--:  
placed|已下单|---->||  
accepted||<----|已接受|  
rejected||<----|已拒绝|  
executed||<----|已出品|商户打印出品单，并进行出品，快捷模式下新增一笔交易  
canceled|已取消|---->||  
paid|已支付|---->||商户打印结算单，并新增一笔交易  

订单类型|说明
-----|-----    
booking|预订    
deliver|外送


***
## 提交订单
### 请求
### POST /orders
```json
{
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "placed",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "type": "booking",
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ],
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "phone": "18912345678",
    "merchants": [
      { 	
        "merchantID" : "e20dccdf039b3874",
        "memberID" : "087442b616a1e8dc",
        "merchantName" : "泛盈科技", 
        "balance" : 40, 
        "point" : 0, 
        "level" : "会员"
      }
    ]
  },
  "receipt": {
    "name": "顾客李四",
    "phone": "13987654321",
    "address": "",
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "2834910281d26a76",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```

### 响应
#### 200 - 成功
```json
{
  "id": "2834910281d26a76",
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "placed",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "type": "booking",
  "fee": 1600,
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ],
  "quantity": 1,
  "sequenceNumber": 1,
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "address": "江宁区胜太路68号408"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "2834910281d26a76",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```
##### 备注
`status` - 订单状态
`type` - 订单类型

#### 400 - 参数错误
#### 401 - 未登录
#### 403 - 权限错误


## 查询订单
### 请求
### GET /orders
#### 查询条件

#### 默认项目

### 响应
#### 200 - 成功
```json
{
  "id": "2834910281d26a76",
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "placed",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "type": "booking",
  "fee": 1600,
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ],
  "quantity": 1,
  "sequenceNumber": 1,
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "address": "江宁区胜太路68号408"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "2834910281d26a76",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```

#### 400 - 参数错误
#### 401 - 未登录
#### 403 - 权限错误

## 更新订单
### 请求
### PUT /orders/:id
```json
{
  "status": "accepted",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    }
  ],
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ]
}
```

### 响应
#### 200 - 成功
```json
{
  "id": "2834910281d26a76",
  "createdAt": 1387529885,
  "updateAt": 1387529885,
  "status": "accepted",
  "memo": [
    {
      "name": "顾客张三",
      "createdAt": 1387529885,
      "message": "提交了订单，不要加辣椒"
    },
    {
      "name": "泛盈总店",
      "createdAt": 1387529885,
      "message": ""
    }
  ],
  "type": "booking",
  "fee": 1600,
  "items": [
    {
      "item": {
        "id": "221f47e56134f82c",
        "name": "盖浇饭",
        "price": 1600
      },
      "id": "E7BC77BA-61CD-47EF-8639-321E760BBC88",
      "dealPrice": 1600,
      "quantity": 1
    }
  ],
  "quantity": 1,
  "sequenceNumber": 1,
  "customer": {
    "id": "6d97c241f56a8873",
    "name": "顾客张三",
    "address": "江宁区胜太路68号408"
  },
  "agent": {
    "id": "6d97c241f56a8873",
    "name": "泛盈微信订餐"
  },
  "shop": {
    "id": "2834910281d26a76",
    "name": "泛盈总店",
    "address": "胜太路68号3层",
    "phone": "025-58679066"
  }
}
```

#### 400 - 参数错误
#### 401 - 未登录
#### 403 - 权限错误
