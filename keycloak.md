红帽 redhat 单点登录
中文文档：https://keycloak.org.cn/documentation.htm
<br>
1、下载安装包
https://www.keycloak.org/getting-started/getting-started-zip
<br>

1、什么是 keycloak
keycloak是一个开源的进行身份认证和访问控制的软件。是由Red Hat基金会开发的，我们可以使用keycloak方便的向应用程序和安全服务添加身份认证，非常的方便。基于 Java 开发，支持多种数据库。<br>
2、主要功能：
SSO
单点登录（Single-Sign On），支持 OpenID Connect、OAuth 2.0、SAML 2.0 标准协议。
Identity Brokering and Social Login
通过配置，可实现对不同身份认证服务的集成，通过这些身份认证服务登录应用。如 GitHub、Google 等，开源社区也有人提供了微信集成方案。
User Federation
用户联合，提供了对 LDAP、Active Directory、Kerberos 的集成方案。
Client Adapters
不同平台多种语言的支持，Java、Python、Go、Node.js、Spring、Quarkus 等。
后台管理
提供了多种语言的后台管理界面，如果想偷懒的话改改图标定制个主题就能拿来用。同时还有 CLI 、SDK 和 RESTful API。
授权服务
提供基于 RBAC、ABAC、UBAC 等多种策略的授权功能。
其他常用功能
密码策略、暴力检测、MFA、日志审计。
<br>



3、本地安装测试：
https://www.jianshu.com/p/2275ae26bcd1  详细安装记录

红帽 redhat 单点登录
中文文档：https://keycloak.org.cn/documentation.htm

1、下载安装包
https://www.keycloak.org/getting-started/getting-started-zip

2、
首次登录可以创建账号，很友好。
Admin / 1234 
![avatar](/Users/zhangping/Documents/szx/soft/keycloak/imag/注册.jpg)




3、创建自己的领域/应用 my-realm001



4、创建成功  my-realm001 之后，切换到  my-realm001 
给  my-realm001 空间创建一个用户





可以给新增的用户设置密码，在 Credentials 菜单。


Temporary ： 是临时用户，用户首次登录之后会通知修改密码。

5、用新创建的用户登录  my-realm001  空间。
   链接：http://localhost:8080/realms/my-realm001/account/#/personal-info
  注意url链接中的空间名称。

6、测试登录
Keycloak网站上有一个SPA测试应用程序。
打开https://www.keycloak.org/app/，单击Save，使用默认配置。
现在，您可以单击Sign in，使用前面启动的Keycloak服务器对该应用程序进行身份验证。

测试链接  https://www.keycloak.org/app/  空间修改为自己的创建的空间名称。



测试登录效果
https://www.keycloak.org/app/#url=http://localhost:8080&realm=my-realm001&client=myclient














