---
title:  "[Practice] Java의 다형성"
excerpt: "Java의 다형성"

categories:
  - Core

toc: true
toc_sticky: true

date: 2023-05-28
last_modified_at: 2023-05-28

---
## 단순한 Java Project 만들기
`설계`
- SMS 발송하는 프로그램 개발  
![diagram](/assets/images/file/polymorphism_practice_diagram.png)

`요구사항`
1. [Spring Framework 프로젝트 생성 실습](https://yeeeeo.github.io/core/spring_framework_project_create_practice/)
에서 생성한 프로젝트에 com.nhnacademy.edu.springframework.messagesender 패키지를 생성한다. 
2. Main.java, User.java 클래스를 생성한다.
3. main() , sendSmsMessage(), sendEmailMessage() 를 구현한다.
  - sendSmsMessage 메소드는 단순히 System.out.println 으로 "SMS Message Sent to ${phoneNumber} : ${message}"를 콘솔에 텍스트를 표시한다.
  - sendEmailMessage 메소드는 단순히 System.out.println 으로 "Email Message Sent ${email} : ${message}"를 콘솔에 텍스트를 표시한다.
4. main 메소드에서는 sendSmsMessage() 를 호출한다.

`Main.java`
```java
public class Main {
    public static void main(String[] args) {
        new Main().sendSmsMessage(new User("email@email.com", "010-1234-1234"), "sms message");
    }

    public void sendSmsMessage(User user, String message){
        System.out.println("SMS Message Sent to "+ user.getPhoneNumber() + ": " + message);
    }

    public void sendEmailMessage(User user, String message){
        System.out.println("Email Message Sent to "+ user.getEmail() + ": " + message);
    }
}
```

`User.java`
```java
public class User {
    private final String email;
    private final String phoneNumber;

    public User(String email, String phoneNumber){
        this.email = email;
        this.phoneNumber = phoneNumber;
    }

    public String getEmail() {
        return email;
    }

    public String getPhoneNumber() {
        return phoneNumber;
    }
}
```

`결과`  
![result](/assets/images/file/polymorphism_practice_code_result1.png)

## 다형성을 이용하여 리팩토링 하기
`설계`
- java 의 다형성을 활용하기 위하여 MessageSender 인터페이스를 선언하고 각각의 기능을 그 구현체로 구현한다.  
![diagram](/assets/images/file/polymorphism_practice_diagram2.png)

`요구사항`
1. MessageSender 인터페이스 선언
2. Main 메소드의 sendSmsMessage, sendEmailMessage 메소드를 MessageSender 상속하여 개발
3. Main 메소드에서 SmsMessageSender 를 사용하도록 결정
4. MessageSendService는 컴파일시에 어떤 MessageSender를 사용할지 결정하지 않음

`Main.java`
```java
public class Main {
    public static void main(String[] args) {
        MessageSendService service = new MessageSendService(new SmsMessageSender());
        service.doSendMessage();
    }
}
```

`MessageSendService.java`
```java
public class MessageSendService {
    private final MessageSender messageSender;

    public MessageSendService(MessageSender messageSender) {
        this.messageSender = messageSender;
    }

    public void doSendMessage(){
        messageSender.sendMessage(new User("email@email.com", "010-1234-1234"), "message");
    }
}
```

`MessageSender.java`
```java
public interface MessageSender {
    void sendMessage(User user, String message);
}

```

`SmsMessageSender.java`
```java
public class SmsMessageSender implements MessageSender{
    @Override
    public void sendMessage(User user, String message) {
        System.out.println("SMS Message Sent to "+ user.getPhoneNumber() + ": " + message);
    }
}
```

`EmailMessageSender.java`
```java
public class EmailMessageSender implements MessageSender{
    @Override
    public void sendMessage(User user, String message) {
        System.out.println("Email Message Sent to "+ user.getEmail() + ": " + message);
    }
}
```