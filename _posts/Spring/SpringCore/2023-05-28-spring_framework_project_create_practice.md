---
title:  "[Practice] Spring Framework 프로젝트 생성 실습"
excerpt: "Spring Framework 프로젝트 생성 실습"

categories:
- Core

toc: true
toc_sticky: true

date: 2023-05-28
last_modified_at: 2023-05-28

---
## Maven 프로젝트 생성
- IntelliJ에서 New Project -> Build system: Maven으로 지정
![spring_framework_project_create_1](/assets/images/file/practice_spring_framework_project_create_1.png)

## spring-framework-bom 사용
- pom.xml 파일에 dependencyManagement 추가
```xml
<project>
    ...
    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-framework-bom</artifactId>
                <version>5.3.17</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>
    ...
</project>
```

## Maven 적용
- IntelliJ 가 다시 maven 설정을 적용하도록 Load Maven Changes 버튼 클릭
![maven_load](/assets/images/file/maven_load.png)
