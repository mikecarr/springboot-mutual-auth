# Springboot-Mutual-Auth Demo
Demo application showing how to implement SSL and Basic User Authentication 

<!-- TOC -->

- [Springboot-Mutual-Auth Demo](#springboot-mutual-auth-demo)
    - [Introduction](#introduction)
    - [SSL](#ssl)
    - [Test Commands](#test-commands)
    - [References](#references)

<!-- /TOC -->

## Introduction

The password changes for each application restarts and can be found in console.

```console
Using default security password: 78fa095d-3f4c-48b1-ad50-e24c31d5cf35
To add your own layer of application security in front of the defaults,
```

```java
@EnableWebSecurity
public class SecurityConfig {

    @Autowired
    public void configureGlobal(AuthenticationManagerBuilder auth) throws Exception {
        auth
            .inMemoryAuthentication()
                .withUser("user").password("password").roles("USER");
    }
}
```

or if you just want to change password you could override default with,

application.xml

```text
security.user.password=new_password
```
or

```text
application.properties

spring.security.user.name=<>
spring.security.user.password=<>
```

## SSL

```
keytool -genkey -alias tomcat -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 3650 
```

## Test Commands
```
$ curl -k --request GET --url https://localhost:8443/secured

{"timestamp":"2018-10-11T21:19:09.835+0000","status":401,"error":"Unauthorized","message":"Unauthorized","path":"/secured"}
```

```
$ curl -k --request GET --url https://localhost:8443/secured --user user:password

Hello user !!! : Thu Oct 11 14:19:12 PDT 2018
```

## References
* https://howtodoinjava.com/spring-boot