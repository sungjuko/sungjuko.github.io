---
layout: post
title: 스프링 메일링 방법 (spring email service)
date: 2021-02-25
Author: soreal 
tags: [Spring, Java]
comments: true
toc: true
---




스프링으로 이메일 서비스 하는 법

본 포스팅은 https://www.baeldung.com/spring-email 을 참조, 번역했습니다.



# 1. 들어가기 전에 

여기서 우리는 순수 바닐라 스프링 어플리케이션(javaMamil 라이브러리 사용)과 스프링부트 어플리케이션(spring-boot-starter-email dependency 사용)으로 이메일을 보내는 방법을 찬찬히 배워본다. 



# 2. Maven dependency

디펜던시를 pom.xml에 각각 추가해줍니다. 

## 2-1. Spring

````
<dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-context-support</artifactId>
    <version>5.2.8.RELEASE</version>
</dependency>
````



## 2-2. Spring boot

````
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
    <version>2.3.4.RELEASE</version>
</dependency>

````

# 3. 메일 서버 속성 Properties

Spring에서 Java 메일 지원을 위한 클래스오 인터페이스들은 다음과 같습니다. 

    ### 1. MailSender interface 
    
    : 간단한 메일 전송 위한 기본 기능 제공하는 최상위 인터페이스
    
    ### 2. JavaMailSender interface 
    
    : MailSender의 서브 인터페이스. MIME 메세지들과 Mime 메세지의 생성을 위한 헬퍼 클래스와 함께 사용. MimeMessagePreparator 매커니즘과 함께 사용하는 것을 추천함.
    
    ### 3. JavaMailSenderImpl class  
    
    : JavaMailSender의 인터페이스 구현체. MimeMessage와 SimpleMailMessage를 지원함.
    
    ### 4. SimpleMailMessage class

    : 수신자, 발송인, 추친, 제목 및 내용 등을 포함한 간단한 메일 메시지를 생성하는데 사용함. 
    
    ### 5. MimeMessagePreparator interface

    :  MIME 메세지의 준비에 있어 콜백 인터페이스를 제공함. 

    ### 6. MimeMessgeHelper class

    : MIME 메세지를 만드는 헬퍼 클래스. 이미지 지원을 제공하고, 형식적인 메일 첨부물과 HTML 레이아웃의 텍스트 컨텐츠를 제공합니다. 

다음으로 이 인터페이스와 클래스들이 어떻게 쓰이는지 보겠습니다. 



## 3.1 Spring Mail Server Properties


빈 등록 옵션은 대략 다음과 같이 하시면 됩니다.

````
@Bean
public JavaMailSender getJavaMailSender() {
    JavaMailSenderImpl mailSender = new JavaMailSenderImpl();
    mailSender.setHost("smtp.gmail.com");
    mailSender.setPort(587);
    
    mailSender.setUsername("my.gmail@gmail.com");
    mailSender.setPassword("password");
    
    Properties props = mailSender.getJavaMailProperties();
    props.put("mail.transport.protocol", "smtp");
    props.put("mail.smtp.auth", "true");
    props.put("mail.smtp.starttls.enable", "true");
    props.put("mail.debug", "true");
    
    return mailSender;
}
````



## 3.2 Spring Boot Mail Server Properties


메일 보내려면 보내는 사람의 서버 주소 설정, 아이디 비번이 필요하겠죠? 넣어주시면 됩니다. 프로퍼티스나 yml 파일에요


````
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=<login user to smtp server>
spring.mail.password=<login password to smtp server>
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
````



# 4. 메일 보내기


우린 이젠 JavaMailSender를 통해 메일을 보낼 수 있습니다. 스프링 버전이나 스프링부트 버전이나 또이또이 하니 작은 차이 부분은 무시해도 된다는 군요.




## 4.1 기본 메일 보내기



메일을 보냅니다.


````
@Component
public class EmailServiceImpl implements EmailService {

    @Autowired
    private JavaMailSender emailSender;

    public void sendSimpleMessage(
      String to, String subject, String text) {
        ...
        SimpleMailMessage message = new SimpleMailMessage(); 
        message.setFrom("noreply@baeldung.com");
        message.setTo(to); 
        message.setSubject(subject); 
        message.setText(text);
        emailSender.send(message);
        ...
    }
}
````

누가, 누구에게, 제목을, 내용을 메세지에 담아서 이메일 샌더로 보내는 단순한 구조입니다.


## 4.2 첨부자료가 추가된 메일 보내기



심플 메일이 아니라 첨부파일 메일을 보내고 싶다면 자바메일 라이브러리의 MIME multipart 메세지를 심플메일메세지 대신 써야합니다.

스프링은 org.springframework.mail.javamail.MimeMessageHelper class 로 자바 메일 라이브러리를 제공합니다.


다음은 예제 소스 입니다.


````
@Override
public void sendMessageWithAttachment(
  String to, String subject, String text, String pathToAttachment) {
    // ...
    
    MimeMessage message = emailSender.createMimeMessage();
     
    MimeMessageHelper helper = new MimeMessageHelper(message, true);
    
    helper.setFrom("noreply@baeldung.com");
    helper.setTo(to);
    helper.setSubject(subject);
    helper.setText(text);
        
    FileSystemResource file 
      = new FileSystemResource(new File(pathToAttachment));
    helper.addAttachment("Invoice", file);

    emailSender.send(message);
    // ...
}
`````


## 4.3 간단한 이메일 템플릿

SimpleMailMessage 클래스는 텍스트 포맷팅을 지원합니다. 우리는 이메일을 위한 템플릿을 빈 설정을 통해 만들 수 있습니다.


````
@Bean
public SimpleMailMessage templateSimpleMessage() {
    SimpleMailMessage message = new SimpleMailMessage();
    message.setText(
      "This is the test email template for your email:\n%s\n");
    return message;
}
````


이제 이 템플릿으로 언제든 메일을 쉽게 보낼 수 있습니다.


````
@Autowired
public SimpleMailMessage template;
...
String text = String.format(template.getText(), templateArgs);  
sendSimpleMessage(to, subject, text);

`````


# 5. 에러 핸들링


JavaMail은 SendFailedException을 제공하여 메시지를 보낼 수없는 상황을 처리합니다. 그러나 잘못된 주소로 전자 메일을 보내는 동안이 예외가 발생하지 않을 수 있습니다. 그 이유는 다음과 같습니다.

RFC 821의 SMTP 프로토콜 사양은 잘못된 주소로 이메일을 보내려고 할 때 SMTP 서버가 반환해야하는 550 반환 코드를 지정합니다. 그러나 대부분의 공용 SMTP 서버는이를 수행하지 않고 대신 "배달 실패 ”상자로 이메일을 보내거나 피드백을 제공하지 마십시오.

예를 들어 Gmail SMTP 서버는 "전송 실패"메시지를 보내고 프로그램에 예외가 없습니다.

따라서이 경우를 처리하기 위해 사용할 수있는 몇 가지 옵션이 있습니다.

1. 던질 수없는 SendFailedException을 잡아라
2. 일정 기간 동안 "배달 실패"메시지에서 보낸 사람 사서함을 확인합니다. 이것은 간단하지 않으며 기간이 결정되지 않았습니다.
3. 메일 서버가 피드백을 전혀 제공하지 않으면 아무것도 할 수 없습니다.


# 6. 결론.

번역은 어렵다.

구현은 간단하다.

