# 第三方系统为机蜜引流，机蜜与第三方账号对接

---
##1.时序图
![时序图](https://file.zpmgo.com/api/download/temp/N2NiYzMyOTUtODNkMy00OGQ2LTliNzctYmIwNjVhN2U3ZWY2LnBuZw==)

##2.对接准备
 - 1.根据文档所示接口列表开发接口；
 - 2.准备测试环境进行联调；
 - 3.机蜜需提供生产环境服务器白名单给第三方；

##3.接口列表
###3.1.跳转第三方页面申请授权获取用户信息
	用户在第三方系统进入机蜜机蜜页面进行业务流程后，当机蜜需要获取第三方用户信息的时候，会跳转到第三方授权页面申请授权获取用户信息，用户在第三方页面确认或取消授权后，第三方APP主动回调机蜜的URL。
	
 - 访问方式：get
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|from|机蜜回调URL|varchar(200)|Y|-|

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
|openId|三方用户openId|varchar(50)|用户在第三方系统唯一标识|

###3.2.获取三方用户详细信息
此接口仅限白名单服务器访问

 - 访问方式：post
 - 参数格式：application/json
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|openId|三方用户openId|varchar(50)|Y|-|


 - 参数示例：

```javascript
{
    "openId":"xxx"
}
```

 - 返回说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|openId|三方用户openId|varchar(50)|Y|用户在第三方系统唯一标识|
|phone|三方用户手机号|varchar(20)|Y|-|
|nickName|三方用户昵称|varchar(40)|N|-|
|headUrl|三方用户头像|varchar(40)|N|-|
|sex|三方用户性别|varchar(2)|N|男|女|
|birthday|三方用户出生年月|int|N|-|
|country|三方用户收货地址-国|varchar(20)|N|-|
|provice|三方用户收货地址-省|varchar(20)|N|-|
|city|三方用户收货地址-市|varchar(20)|N|-|
|regoin|三方用户收货地址-区县|varchar(20)|N|-|
|address|三方用户收货地址-详细地址|varchar(100)|N|-|








