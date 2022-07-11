红帽 redhat 单点登录
中文文档：https://keycloak.org.cn/documentation.htm

1、下载安装包
https://www.keycloak.org/getting-started/getting-started-zip


1、什么是 keycloak





本地安装测试：
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














