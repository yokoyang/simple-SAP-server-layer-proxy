# simple SAP server layer proxy

在spring boot 框架中，使用Zuul Proxy代理的方法，将内部接口暴露到外面

**zuul.sslHostnameValidationEnabled=false**

配置使得可以访问证书不安全的网站

## 嵌入式Zuul反向代理
Spring Cloud已经创建了一个嵌入式Zuul代理，以简化UI应用程序想要代理对一个或多个后端服务的呼叫的非常常见的用例的开发。此功能对于用户界面对其所需的后端服务进行代理是有用的，避免了对所有后端独立管理CORS和验证问题的需求。

要启用它，使用@EnableZuulProxy注释Spring Boot主类，并将本地调用转发到相应的服务。按照惯例，具有ID“用户”的服务将接收来自位于/users的代理（具有前缀stripped）的请求。代理使用Ribbon来定位要通过发现转发的实例，并且所有请求都以 hystrix命令执行，所以故障将显示在Hystrix指标中，一旦电路打开，代理将不会尝试联系服务。
