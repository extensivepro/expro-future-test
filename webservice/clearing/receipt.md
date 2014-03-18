# 收据 receipts

## 提交收据
iOS客户端提交应用内购的收据和设备信息到清算服务，经Apple验证过以后将验证的结果返回客户端。

### POST /receipts

```json
{
  "udid": "C75DAEFD-7442-4FDB-B2AC-FF28E3E4F272",
  "data": "receipt data base64 encode"
}
```

#### 备注
* `udid` - 泛盈定义的设备的唯一标识
* `data` - 收据数据，经过base64编码

### 响应
#### 201 - 创建成功
- 发布收据登记成功事件

#### 400 - 参数错误

* `udid` - `is required`  
  - `is not found`  
* `data` - `is required`
  - `is incorrect`

#### 401 - 未登陆
