# 设备 devices

## 新增设备
### 请求 
### POST /devices

``` json
{
    "code": 100001, 
    "createdAt": 1386235335, 
    "name": "expro's iPad Air", 
    "shop": {
        "id": "903d6f6ce857a9eb",
        "merchant":{
            "id": "c82e1197884d8806",
            "owner": {
                "id": "af968c00fcaf8b0a"
            }
        }
    }, 
    "udid": "FFFF3cac05dd2f8bed64c4d11c6077742bce974c128a", 
    "updateAt": 1386235335
}
```

#### 备注
* `code` - 系统自增,不可编辑。

### 响应

#### `200` - 添加成功
``` json
{
    "_id": "b076516ea444189f", 
    "code": 100001, 
    "createdAt": 1386235335, 
    "name": "expro's iPad Air", 
    "shop": {
        "id": "903d6f6ce857a9eb",
        "merchant":{
            "id": "c82e1197884d8806",
            "owner": {
                "id": "af968c00fcaf8b0a"
            }
        }
    }, 
    "udid": "FFFF3cac05dd2f8bed64c4d11c6077742bce974c128a", 
    "updateAt": 1386235335
}
```

#### `400` - 参数错误
* `udid` - `is required`
  - `is duplicated`
* `shop` - `is required`
  - `.id is required`
  - `.merchant.id is required`
  - `.merchant.owner.id is required`

#### `401` - 未登录
#### `403` - 权限错误

## 设备登记
将平台中的设备登记到当前用户的账户下的商店中，这样让设备共享账户下的基础信息。
### 请求
### POST /device-register
```json
{
  "udid": "FFFF3cac05dd2f8bed64c4d11c6077742bce974c128a",
  "code": "10002",
  "name": "总店2号收银台-iPad4"，
  "registerShopID": "903d6f6ce857a9eb"
}
```
#### 备注
`registerShopID` - 可选，没有指定的时候将设备所属的商户挂载到当前用户下面

### 响应
#### `200` OK
#### `400` - 参数错误
* `udid` - `is required`
  - `is not exist`

#### `401` - 未登录
