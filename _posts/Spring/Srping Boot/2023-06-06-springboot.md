---
title:  "[Spring Boot] 스프링 부트 프레임워크"
excerpt: "스프링 부트 프레임워크"

categories:
- Spring Boot

toc: true
toc_sticky: true

date: 2023-06-06
last_modified_at: 2023-06-06

---
## 스프링 부트 프레임워크
> 모든 스프링 프로젝트는 스프링 프레임워크를 반드시 포한한다. 하지만 스프링 부트 프로젝트의 목적은 스프링 프로젝트와 완전히 다르다.
> 스프링 부트는 가능한 빠르게 애플리케이션을 개발하고 서비스하는 것을 우선시한다.
> 그래서 스프링 부트 프로젝트에서는 가장 보편적으로 많이 사용하는 형태로 스프링 애플리케이션을 미리 설정해 놓았다.
> 그리고 직접 설정하는 것보다 관례(CoC: Convention over Configuration)에 맞게 코드를 작성하면 미리 설정된 형태로 애플리케이션을 개발할 수 있다.  
> 스프링 부트의 장점은 설정 없이 관례에 따라 바로 애플리케이션을 개발할 수 있고 단점으로는 관례에 벗어난 코드는 동작하지 않으므로 미리 이 관례를 잘 알고 있어야 한다.

![relation](/assets/images/file/springboot/boot3.png)  
위 그림은 스프링 부트와 스프링 프레임워크의 관계를 표현한 것이다. 스프링 부트는 스프링 프레임워크의 범위를 포함한다.

## 스프링 부트가 제공하는 기능
1. 단독 실행 가능한 스프링 애플리케이션  
스프링 부트 프로젝트는 빌드 플러그인을 제공하고, 이를 실행하면 단독 실행 가능한 `JAR` 파일을 만들 수 있다.
그리고 java 명령어와 -jar 옵션을 사용하면 간단하게 애플리케이션을 실행할 수 있다.
매우 간단하고 빠르게 배포할 수 있는 장점이 있다. 특히 클라우드 서비스를 사용하는 경우 이 기능과 시너지 효과를 일으킬 수 있다.
JDK가 설치된 VM에 JAR만 배포하면 빠르게 스케일아웃할 수 있다.


2. 간편한 설정을 위한 `스타터` 의존성 제공  
스프링 부트 프로젝트는 기능별로 라이브러리 의존성을 포함한 스타터를 제공한다.
스타터 내부에 라이브러리 의존성 설정을 포함하고 있어 기능을 사용하는 데 필요한 모든 라이브러리를 한 번에 추가할 수 있다.
또한 라이브러리들의 버전은 상호 호환 검증되어 사용자가 쉽게 사용할 수 있다.
기본으로 제공하는 다양한 스타터가 있지만, 개발자가 직접 스타터를 만들 수도 있다.
생성한 스타터는 직접 배포가 가능하다.


3. 스프링 기능을 자동 설정하는 `자동 구성` 제공  
스프링 부트는 자동 구성 기능을 제공한다. 그래서 특정 조건들이 충족되면 미리 설정된 자바 설정 클래스가 동작하고 애플리케이션을 구성한다.


4. 모니터링 지표, 헬스 체크를 위한 `액추에이터`  
스프링 부트를 이용해서 애플리케이션을 개발했다면 기본 모리터링 지표와 헬스 체크 기능을 기본으로 제공한다.
그래서 모니터링 솔루션을 이용해서 각 서버들의 상태와 지표를 수집하기 매우 쉽다.


5. XML 설정을 위한 일이 필요 없음  
스프링 프레임워크 3.0부터 Java 클래스를 이용하여 설정 가능한 자바 설정 기능을 제공한다.
스프링 부트도 자바 설정을 기본으로 사용하며, 자동 구성을 이용하여 이미 많은 기능이 미리 설정되어 있다.


6. 애플리케이션에 내장된 WAS  
스프릉 부트의 spring-boot-starter-web 스타터를 이용하여 웹 어플리케이션을 개발한 경우 톰캣이 내장되어 있다. 
톰캣 대신 다른 WAS, 즉 제티(Jetty)나 언더토우(UnderTow)로 교체도 가능하다.

