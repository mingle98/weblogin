
**前端必备工具（免费图床、API、chatAI等）推荐网站LuckyCola:**
[https://luckycola.com.cn/](https://luckycola.com.cn/)
# 一、产品介绍

 - 自己开发一套**登录注册功能**耗时耗力成本巨大,这里介绍如何接入《**[开放登录平台](http://luckycola.com.cn/public/dist/#/allLoginPage)**》,使自己的网站无需开发就可以快速拥有强大的登录注册功能
 - 《**[LuckyCola开放登录平台](http://luckycola.com.cn/public/dist/#/allLoginPage)**》是一个稳定高效的,免开发、多功能、稳定的登录系统,可以接入到Pc端和移动端的网站或者h5应用
![在这里插入图片描述](https://img-blog.csdnimg.cn/fc8eb71467694002aaaf08cf0271b44f.png#pic_center)

# 二、开始使用
**重要提示:所有请求建议使用https协议,当https协议无法使用时再尝试使用http协议**
## 1、如何判断用户是否登录?
在需要用户登录的业务场景,我们需要先判断当前用户是否已经登录?如果没有登录在引导用户前往登录

**[《登录登录平台](http://luckycola.com.cn/public/dist/#/allLoginPage)》提供了“检测用户登录态”的API:**

```
请求方式: GET
请求参数:无需参数
```

```js
http(s)://luckycola.com.cn/checkLoginStatus
```

*返回示例及说明:*
```js
{ 
 	// 接口请求成功
     code: 0,
 	// 登录状态提示
     msg: '已登录,登录态有效'  或 ’未登录或登录态无效',
	 // 用户登录状态 值是0或1 ,1表示用户已经登录 0表示用户未登录
      status: 1
}
```

通过API检测到用户未登录时,您可以在您的应用展示“登录入口”引导用户进行登录


## 2、如何让用户登录?

当您展示“登录入口”引导用户进行登录后,用户点击“入口”,您通过Url跳转“《开放登录平台》”即可

**注意:跳转“《开放登录平台》”的Url配置如下:**

```js
// 跳转开放登录平台的url 
// 注意 u参数必须进行encodeURIComponent()编码处理,并且跳转域名需要申请加入白名单否则无法携带用户信息
http(s)://luckycola.com.cn/public/dist/#/allLoginPage?u=encodeURIComponent(登录成功后的回跳地址)

```



**参数说明:**

| 序号 | 参数 | 是否必须|说明 |
|--|--|--|--|
| 1 |u  |是 | 登录后跳转的回调地址,登录成功后会在这个url上拼接有用户参数(这个url请encodeURIComponent)处理|

#### 举个例子:
如果我我的网站地址是“**http://test.com**”,我需要引导用户进行登录,就直接跳转下面这个“登录开放平台”的地址即可(注意:**u是经过encodeURIComponent**处理的)

```js
https://luckycola.com.cn/public/dist/#/allLoginPage?u=http%3A%2F%2Ftest.com
```

跳转成功至“**《开放登录平台》**”后用户就可以自行选择登录的方式或者注册


## 3、登录成功后如何拿到用户数据?
当用户在“[《开放登录平台》](http://luckycola.com.cn/public/dist/#/allLoginPage)”完成登录后,平台将会自动跳转回您的回调地址(u参数),并且在您的回调地址上拼接上“**登录状态**”、“**用户名**”等


**参数,具体参数如下**
| 序号 | 参数 | 说明 |
|--|--|---|
| 1 |isLoginOk  |用户登录是否成功,值是1或者0(1表示成功,0表示失败)|
| 2 |uid  |登录用户的唯一id,您可以自己存储这个id处理更多的业务场景|
| 3 |usrname  |登录用户的用户名|
| 4 |userInfoUrl  | 查看登录用户更多信息的url地址|

*举个例子:*
如果我通过下面这个url跳转[《登录开放平台》](http://luckycola.com.cn/public/dist/#/allLoginPage)
```js
https://luckycola.com.cn/public/dist/#/allLoginPage?u=http%3A%2F%2Ftest.com
```
并且用户登录成功了,那么跳回您的回调地址是这样的:
```js
http://test.com?isLoginOk=1&uid=(用户唯一标识)&usrname=(用户名称)&userInfoUrl=(经过encodeURIComponent后的查看用户信息的地址)
```

所以在您的网站或者应用通过获取url上的这些参数即可

## 4、如何维护用户的登录态?
当用户登录成功后您就可以获取用户的相关信息,自行维护登录态,同时您再通过API检测用户登录态,《登录开放平台》登录态的保持时间是15天,如果登录态过期,再次引导用户进行登录即可


**《登录开放平台》也提供一个主动退出登录的API:**

```c
请求方式: GET
参数: cuid(用户id,前往官网http://luckycola.com.cn个人中心获取)
```

```js
https://luckycola.com.cn/user/logout?cuid=12..
```

# 二、注意点
 1、处于安全性考虑,如果您需要接入[《开放登录平台》](http://luckycola.com.cn/public/dist/#/allLoginPage),请您登录[LuckCola官网](http://luckycola.com.cn)后进入[**个人中心**]点击[**开放登录平台域名申请**]进行申请,申请结果平台将以邮件形式回复即可接入使用啦~

 ----
**重要的事情说三遍**
 - u参数跳转地址的域名需要申请加入白名单否则无法携带用户信息
 - u参数跳转地址的域名需要申请加入白名单否则无法携带用户信息
 - u参数跳转地址的域名需要申请加入白名单否则无法携带用户信息
[**个人中心**]----[**开放登录平台域名申请**]----进行申请
![在这里插入图片描述](https://img-blog.csdnimg.cn/86c05c33102943569a7601661213133f.png#pic_center)


