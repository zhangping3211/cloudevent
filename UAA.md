1、什么是uaa
github：https://github.com/cloudfoundry/uaa <br>
docs：https://github.com/cloudfoundry/uaa/tree/develop/docs <br>
官方介绍： <br>
UAA是一个多租户身份管理服务，在Cloud Foundry中使用，但也可以作为一个独立的OAuth2服务器。 <br>
它的主要角色是OAuth2提供者，为代表云计算用户的客户端应用程序颁发令牌。 <br>
它还可以使用用户的Cloud Foundry凭据进行身份验证，并可以使用这些凭据(或其他凭据)充当SSO服务。 <br>
它拥有用于管理用户帐户和注册OAuth2客户端的端点，以及其他各种管理功能。 <br>
理解：  <br>
UAA 是 User Account and Authentication 首字母的缩写， 是 CloudFoundry（一个 PaaS 服务供应商）开源的用户帐号和身份认证服务，可用于搭建 OAuth2 认证授权服务器。(什么是oath2后面有文档介绍) <br>

UAA 是 OAuth2 授权服务器。在应用程序获取访问令牌之前，开发人员必须执行一次性注册过程才能在 UAA 中创建客户端。 <br>
uaa旨在方便管理授权证明。
2、uaa 架构图
![img](https://github.com/zhangping3211/cloudevent/blob/main/img/uaa1.png)

3、uaa 支持的协议




4、uaa 认证流程
使用登录服务器的可扩展身份验证
1. 用户未被授权访问应用。应用程序将用户重定向到授权服务器以请求授权。
2. 用户验证并批准释放包含授权证明的令牌。
   3.用户被重定向回客户端应用程序与授权代码。
4. 客户端为访问和刷新令牌兑换认证代码。 <br>
   备注：“uaa db”的鉴权方式不支持用户名和密码。 <br>
   支持cloudfoundry的图形和品牌，而不是uaa中的通用接口。 <br>
   登录服务器可以支持saml, ldap, openid2(谷歌)，oauth 1.1 (twitter)， facebook等。 <br>
   一些登录服务器代理oauth2令牌端点到uaa。 <br>
   我们正在努力使登录服务器上的/info端点可用:oauth2令牌和授权，scim用户和组，openid连接userinfo等。 <br>
   ![img](https://github.com/zhangping3211/cloudevent/blob/main/img/uaa2.png)

https://github.com/cloudfoundry/uaa/blob/develop/docs/UAA-Overview.rst#openid-connect-and-oauth2
<br/> 
认证服务：  <br>
https://github.com/cloudfoundry/uaa/blob/develop/docs/UAA-Overview.rst#openid-connect-and-oauth2
<br/>
4.1 使用 oauth2 标准授权访问。 <br>
UAA 可用作授权服务器，它允许客户端应用程序使用四个标准的 OAuth2 授权授予流来代表用户与资源进行交互， 
以获取访问令牌： <br>
Authorization code：授权码  <br>
Implicit：隐含式（授权码隐含式）  <br>
Resource owner password credentials：资源所有者密码凭据  <br>
Client credentials：客户端凭据  <br>
UAA 用户是 OAuth2 协议的资源所有者。 <br>
颁发给用户的访问令牌包含范围位于请求客户端允许的范围和用户的组成员资格的交集。 <br>
 <br/>
4.2 客户端
UAA 是 OAuth2 授权服务器。 <br>
在应用程序获取访问令牌之前，开发人员必须执行一次性注册过程才能在 UAA 中创建客户端。  <br>
客户端通常代表具有自己的一组权限和配置的应用程序。客户端受简单的凭据（例如客户端 ID 和机密）保护，应用程序使用这些凭据对 UAA 进行身份验证以获得令牌。 <br>
客户有两种类型：  <br>
·  客户端访问资源并向 UAA 请求令牌以执行此操作  <br>
·  代表资源并接受和验证访问令牌的客户端  <br>
通过客户端注册在 UAA 中创建客户端。您可以使用 UAA 配置文件在 UAA 中定义客户端，也可以使用 UAA API 创建客户端。
 <br/>

4.3. 选择授权授予类型
要创建客户端，开发人员必须指定使用其客户端应允许的授权类型。 <br>
授予类型决定了您的客户如何与 UAA 进行交互。  <br>
每种授权类型都对应于 OAuth2 2.0 授权框架中定义的四种不同的授权流之一。  <br>
UAA 上可用的授权类型包括：  <br>
· authorization_code：授权码  <br>
· password：密码  <br>
· implicit：隐含式  <br>
· client_credentials：客户端凭据  <br>
为了提高安全性，请仅使用您的应用所需的授权类型。但是，如有必要，您可以将多种授权类型分配给一个客户端。 <br>
<br/>
4.4 授权码 流程  <br>
官方示例： <br>

![img](https://github.com/zhangping3211/cloudevent/blob/main/img/uaa3.png)
 <br/>
![img](https://github.com/zhangping3211/cloudevent/blob/main/img/uaa4.png)

5、优缺点  <br/>
优点：服务代码单独部署，java语言开发，修改方便，支持协议多。 <br/>
缺点：
需要单端分离部署，前端部署文档缺少，操作困难。

<br/>