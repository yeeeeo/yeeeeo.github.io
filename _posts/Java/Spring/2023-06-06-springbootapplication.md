---
title:  "[Spring Boot] @SpringBootApplication"
excerpt: "@SpringBootApplication"

categories:
- Spring

toc: true
toc_sticky: true

date: 2023-06-06
last_modified_at: 2023-06-06

---
## Main Class
```java
@SpringBootApplication
public class SpringTourApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringTourApplication.class, args);
    }
}
```
스프링 이니셜라이저로 생성된 프로젝트는 메인 클래스를 포함해서 자동 생성된다.   
이 클래스의 코드가 스프링 부트 애플리케이션을 실행하는 진입 지점이다.  
`main()` 메서드의 핵심 코드는 `@SpringBootApplication` 애너테이션과 `o.s.boot.SpringApplication` 클래스다.

## @SpringBootApplication
`SpringBootApplication 애너테이션의 소스 코드 일부`
```java
package org.springframework.boot.autoconfigure;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(
    excludeFilters = {@Filter(
    type = FilterType.CUSTOM,
    classes = {TypeExcludeFilter.class}
), @Filter(
    type = FilterType.CUSTOM,
    classes = {AutoConfigurationExcludeFilter.class}
)}
)
public @interface SpringBootApplication {
    // 생략
}
```
### @SpringBootConfiguration
`@SpringBootConfiguration`은 스프링 부트 프로젝트에서 제공하는 애너테이션이다.  
내부에는 스프링 프레임워크에서 제공하는 `@Configuration`을 포함하고 있다.  
`@Configuration` 애너테이션이 정의된 클래스는 자바 설정 클래스라고 한다.  
자바 설정 클래스는 스프링 부트 애플리케이션을 설정할 수 있으며 별도의 스프링 빈을 정의할 수 있다.  
그러므로 `@SpringBootConfiguration`이 정의된 `SpringTourApplication.class`도 자바 설정 클래스이며 스프링 빈 설정을 포함할 수 있다.

### @EnableAutoConfiguration
`@EnableAutoConfiguration`은 스프링 부트 프로젝트에서 제공하는 애너테이션이다.  
`@Configuration` 애너테이션과 같이 사용하면 스프링 부트 프레임워크의 자동 설정 기능을 활성화하는 기능을 제공한다.

### @ComponentScan
`@ComponentScan`은 클래스 패스에 포함되어 있는 `@Configuration`으로 정의된 자바 설정 클래스와 스테레오 타입 애너테이션으로 정의된 클래스를 스캔한다.  
스프링 빈 설정을 스캔하며 찾아낸 것들은 스프링 빈 컨테이너가 스프링 빈으로 로딩하고 관리한다.

## 스프링 애플리케이션 설정 및 실행 예제
### application.properties
```properties
server.port=18000
server.tomcat.threads.min-spare=100
server.tomcat.threads.max=100
```  

`server.port=18000`: 스프링 부트 애플리케이션의 기본 포트는 8080번이다. 기본 포트를 수정하기 위해 server.port 키 값을 변경한다.
`server.tomcat.threads.min-spare=100`: 스프링 부트 애플리케이션의 톰캣 워커 스레드 풀의 최솟값을 설정한다.
`server.tomcat.threads.max=100`: 톰캣 워커 스레드 풀의 최댓값을 설정한다.

### Main Class 수정
```java
@SpringBootApplication
@Slf4j
public class SpringTourApplication {
    public static void main(String[] args) {
        ConfigurableApplicationContext ctx = SpringApplication.run(SpringTourApplication.class, args);

        Environment env = ctx.getBean(Environment.class);
        String portValue = env.getProperty("server.port");
        log.info("Customized Port : {}", portValue);

        String[] beanNames = ctx.getBeanDefinitionNames();
        Arrays.stream(beanNames).forEach(name -> log.info("Bean Name : {}", name));
    }
}
```
`SpringTourApplication.java` 클래스를 실행하면 다음과 같은 실행 결과 로그를 확인할 수 있다.  
![log](/assets/images/file/springboot/boot4.png)  
빨간색 박스의 로그는 임베디드 톰캣 서버가 18000번 포트에서 실행된것을 의미한다.  
노란색 박스의 로그는 `SpringTourApplication.java` 클래스에서 로그를 찍은 결과다.

`SpringTourApplication.java` 예제를 작성하면서 직접 `new` 키워드를 사용하여 TomcatWebServer 객체를 생성하지 않았다.  
하지만 로그 결과를 통해 스프링 부트 애플리케이션처럼 TomcatWebServer 객체가 생성되고 시작하는 것을 확인할 수 있다.  
이 내용으로 스프링 부트 애플리케이션의 '설정보다 관례'와 자동 설정 기능을 확인할 수 있다.