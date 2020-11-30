## Tomcat配置

```xml
server.port=8081
server.error.path=/error
server.servlet.session.timeout=30m
server.servlet.context-path=/chapter02
server.tomcat.uri-encoding=utf-8
server.tomcat.threads.max=500
#server.tomcat.basedir= Tomcat 运行日志和临时文件目录，不配置则使用默认
```

## HTTPS 配置

java 提供的 keytool 工具生成数字证书

```
keytool -genkey -alias tomcathttps -keyalg RSA -keysize 2048 -keystore hzh.p12 -validity 365
```

配置文件中添加

```xml
server.ssl.key-store=hzh.p12
server.ssl.key-alias=tomcathttps
server.ssl.key-store-password=123456  # 命令中输入的密码
```

```java
package top.huzhenhao.chapter02.config;

import org.apache.catalina.Context;
import org.apache.catalina.connector.Connector;
import org.apache.tomcat.util.descriptor.web.SecurityCollection;
import org.apache.tomcat.util.descriptor.web.SecurityConstraint;
import org.springframework.boot.web.embedded.tomcat.TomcatServletWebServerFactory;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
public class TomcatConfig {
    //将http重定向至https
    @Bean
    public TomcatServletWebServerFactory tomcatServletWebServerFactory() {
        TomcatServletWebServerFactory factory =
                new TomcatServletWebServerFactory() {
                @Override
                protected void postProcessContext(Context context) {
                    //SecurityConstraint必须存在，可以通过其为不同的URL设置不同的重定向策略。
                    SecurityConstraint securityConstraint = new SecurityConstraint();
                    securityConstraint.setUserConstraint("CONFIDENTIAL");
                    SecurityCollection collection = new SecurityCollection();
                    collection.addPattern("/*");
                    securityConstraint.addCollection(collection);
                    context.addConstraint(securityConstraint);
                }
            };
        factory.addAdditionalTomcatConnectors(createHttpConnector());
        return factory;
    }

    private Connector createHttpConnector() {
        Connector connector = new Connector("org.apache.coyote.http11.Http11NioProtocol");
        connector.setScheme("http");
        connector.setSecure(false);
        connector.setPort(8080);
        connector.setRedirectPort(8081);
        return connector;
    }
}
```

访问：

https://localhost:8081/chapter02/hello

http://localhost:8080/chapter02/hello