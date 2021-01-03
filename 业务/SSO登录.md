### SSO登录

#### 1.从未登录过sso的系统

* 用户先访问应用系统提供的服务资源
* 跳转到sso服务上进行登录
* 用户身份认证
* SSO认证服务器会生成一个随机的Service Ticket
* SSO服务器验证Service Ticket的合法性，通过验证以后允许客户端的访问服务器
* SSO验证成功后，将认证成功的消息返回给客户端

返回给客户端`cookie`, 之后每次客户端要访问应用服务器资源就带着cookie进行访问，cookie过期以后，就按照上述的步骤在次登陆 （**这里指的是同域名的条件下）**

#### 2. 跨域进行sso登陆：

**不同的域名之间的cookie是不共享的**： 

* 用户访问应用系统的服务资源
* 跳转到SSO的服务器上， SSO服务器也没有登录，所以要输入账号密码进行登录
* SSO服务器登录成功以后， 将登录状态写进SSO的Session中， 浏览器中写入SSO域下的cookie
* SSO服务器会生成一个随机的Service ticket，然后跳转到应用服务器上，作为参数传给的应用系统
* 应用系统的接收到service ticket之后发送请求给SSO服务器，验证service ticket的正确性
* 验证通过过，将登录状态写入应用系统的session中，并设置应用服务器域名下的cookie

#### 3. 用户登出

![sso login.jpg](https://i.loli.net/2021/01/03/aSHtumpKYjJAMPo.jpg)**用户登出：**

1. 清除客户端登录的AuthToken
2. 清楚内存缓存（redis）中的用户登录状态

