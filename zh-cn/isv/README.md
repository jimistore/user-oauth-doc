# 机蜜为第三方系统引流，第三方与机蜜账号对接

---
##1.时序图
![时序图](https://file.zpmgo.com/api/download/temp/ZWFmMWJhZjgtYjI0ZC00MjJiLWFiMzctOTAyMDBmYTM1Nzg3LnBuZw==)

##2.流程说明
 - 1.机蜜添加第三方系统入口，用户点击三方系统入口；
 - 2.跳转三方系统，进行三方业务流程，需要用户登录信息；
 - 3.三方系统获取机蜜用户信息，跳转机蜜授权页面；
 - 4.机蜜平台判断用户是否登录，促使用户登录；
 - 5.机蜜平台获取当前用户信息；
 - 6.机蜜平台回调第三方系统URL并传参数用户唯一标识“jimiOpenId”及授权“authKey”；
 - 7.第三方系统根据用户唯一标识“jimiOpenId”及授权“authKey”向机蜜平台查询用户信息；
 - 8.机蜜平台返回用户手机号等详细信息；
 - 9.第三方系统获取到用户信息，根据用户信息静默注册登录。

##3.接口说明
###3.1.机蜜平台为第三方系统分配appId和secret
	机蜜平台会为每一个对接的第三方系统分配唯一对应的appId及secret。

###3.2.第三方系统更新secret
	为了安全起见，三方secret应该定时进行更新。

 - 访问方式：post
 - 参数格式：application/json
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|appId|三方appId|varchar(50)|Y| |
|timestamp|时间戳|varchar(20)|Y| |
|sign|加密参数|varchar(50)|Y|sign=MD5(appId=xxx&secret=xxx&timestamp=xxx)|

 - 参数示例：

```javascript
{
    "appId":"xxx",
    "sign":"xxx",
    "timestamp":"xxx"
}
```

 - 返回说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|appId|三方appId|varchar(50)|Y| |
|secret|新的三方secret|varchar(50)|Y| |

###3.3.获取用户信息，跳转机蜜授权页面
	第三方系统需要登录的用户的信息的时候，需要跳转机蜜授权页面进行授权。
	打开机蜜授权页面时，需要将appId，from，sign作为参数添加在URL后面。
	
 - 访问方式：get
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|appId|三方appId|varchar(50)|Y| |
|from|三方回调URL|varchar(200)|Y| |
|sign|加密参数|varchar(50)|Y|sign=MD5(appId=xxx&secret=xxx&from=xxx)|

 - 跳转示例：

```javascript
jimiURL?appId=xxx&from=xxx&sign=xxx
```

 - 返回说明：

```javascript
成功授权，机蜜跳转三方URL并传参数“success=true”、用户唯一标识“jimiOpenId”及授权“authKey”；
取消授权，机蜜跳转三方URL并传参数“success=false”。
```
|名称|含义|类型|备注|
|----|:---|:---|--------|
|jimiOpenId|机蜜用户jimiOpenId|varchar(50)|用户在机蜜平台唯一标识|
|authKey|机蜜用户授权key|varchar(50)| |

###3.4.第三方系统获取用户详细信息

 - 访问方式：post
 - 参数格式：application/json
 - 参数说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|appId|三方appId|varchar(50)|Y| |
|sign|加密参数|varchar(50)|Y|sign=MD5(jimiOpenId=xxx&authKey=xxx&appId=xxx&secret=xxx)|
|jimiOpenId|机蜜用户jimiOpenId|varchar(50)|Y| |
|authKey|机蜜用户授权key|varchar(50)|Y| |

 - 参数示例：

```javascript
{
    "appId":"xxx",
    "sign":"xxx",
    "jimiOpenId":"xxx",
    "authKey":"xxx"
}
```

 - 返回说明：

|名称|含义|类型|必填|备注|
|----|:---|:---|:--:|--------|
|jimiOpenId|机蜜用户jimiOpenId|varchar(50)|Y| |
|phone|机蜜用户手机号|varchar(20)|Y| |

