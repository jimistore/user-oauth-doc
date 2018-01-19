# 第三方系统接入机蜜方案

---
##1.场景时序图
![时序图](https://file.zpmgo.com/api/download/temp/N2NiYzMyOTUtODNkMy00OGQ2LTliNzctYmIwNjVhN2U3ZWY2LnBuZw==)

##2.对接流程
 - 1.第三方系统提供接口列表所示接口；
 - 2.第三方系统提供测试环境进行联调；
 - 3.机蜜提供生产环境服务器白名单给第三方；
 - 4.联调成功后发布上线。

##3.接口列表
###3.1.跳转第三方页面申请授权获取用户信息
用户在第三方系统进入机蜜机蜜页面进行业务流程后，当机蜜需要获取第三方用户信息的时候，会跳转到第三方授权页面申请授权获取用户信息，用户在第三方页面确认或取消授权后，第三方APP主动回调机蜜的URL。

 - 访问方式：get
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|from|回调URL|varchar(200)|Y|用户确认/取消授权后的回调地址|

 - 跳转示例：

```javascript
URL?from=xxx
```

 - 返回说明：

```javascript
成功授权，第三方跳转机蜜URL并传参数“success=true”、用户唯一标识“openId”；
取消授权，第三方跳转机蜜URL并传参数“success=false”。
```
|名称|含义|类型|备注|
|----|:---|:---|--------|
|openId|三方用户openId|varchar(50)|用户在第三方系统的唯一标识|

###3.2.获取三方用户详细信息
此接口仅限白名单服务器访问

 - 访问方式：post
 - 参数格式：application/json
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|openId|openId|varchar(50)|Y|用户在第三方系统的唯一标识|


 - 参数示例：

```javascript
{
    "openId":"xxx"
}
```

 - 返回说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|openId|openId|varchar(50)|Y|用户在第三方系统的唯一标识|
|phone|手机号|varchar(20)|Y|-|
|nickName|昵称|varchar(40)|N|-|
|headUrl|头像|varchar(40)|N|-|
|sex|性别|varchar(2)|N|男/女|
|birthday|出生年月|int|N|-|
|country|收货地址-国|varchar(20)|N|-|
|provice|收货地址-省|varchar(20)|N|-|
|city|收货地址-市|varchar(20)|N|-|
|regoin|收货地址-区县|varchar(20)|N|-|
|address|收货地址-详细地址|varchar(100)|N|-|








