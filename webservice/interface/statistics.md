统计查询

查询销售数据
请求
GET /statistics

QueryString
period - 周期；例如：daily、weekly、monthly、yearly
keyID - 查询数据对象的ID；例如在查询商店日报的时候，ID==shopID
* `skip` - 查询起始位置；示例：?skip=0
* `limit` - 查询长度；示例：?limit=20

## 响应

200 - 成功

```json
[
    {
        "id": "03ade6495d577b91#2013-12-27", 
        "value": {
            "keyID": "03ade6495d577b91", 
            "prepay": {
                "count": 2, 
                "total": 30000
            }, 
            "return": {
                "count": 1, 
                "total": 2000
            }, 
            "sale": {
                "count": 5, 
                "total": 69200
            }, 
            "statAt": 1388073600000
        }
    }
]

```
