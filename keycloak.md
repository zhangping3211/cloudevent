什么是 keyCloak ？
keycloak是一个开源的进行身份认证和访问控制的软件。是由Red Hat基金会开发的，我们可以使用keycloak方便的向应用程序和安全服务添加身份认证，非常的方便。基于 Java 开发，支持多种数据库。
主要功能：
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

优点：
Redhat 开源，稳定质量可靠，一直在演进和更新。
易开发易扩展，相对 CAS。
功能丰富易用，如果只是要一个简单的 IAM，几乎是开箱即用。
标准实现，易集成，大厂背书。Kubernetes、Grafana、Kibana、Rancher、Vault、Harbor、Jenkins、Activiti 等等天然支持。

缺点：

没进 CNCF，基于 Wildfly 框架，个人感觉挺重，并不适合云原生。Keycloak 官方应该也是意识到这个问题，正在往 Quarkus 转变。
中文并不友好，这也是为啥有 IDaaS Book 这个项目。


架构图：
![img](https://github.com/zhangping3211/cloudevent/blob/main/img/keycloak1.png)

