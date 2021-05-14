---
layout: post
title: 스프링 메일링 기능 간단하고 빠르게 구현하기
date: 2021-02-25
Author: soreal 
tags: [Spring, Java]
comments: true
toc: true
---


스프링 메일링 기능 간단하고 빠르게 구현하기


# 1. yml (properties) 파일에 SMTP 서버 설정


보통 해당 메일 서버에 잘 설명되어있습니다. 설정해주세요.

````
 mail:
    host: 호스트 주소
    port: 587 (포트 다를 수 있음)
    username: 본인서버
    password: 비번
    properties:
      mail:
        smtp:
          auth: 
          starttls:
            enable: 

`````


# 2. 서비스 단에 EmailService를 선언


````
    private JavaMailSender javaMailSender;

    @Value("${spring.mail.username}")
    public String sender;

    public EmailService(JavaMailSender javaMailSender) {
        this.javaMailSender = javaMailSender;
    }

````

JavamailSender 선언해서 끌어와주시고 (간단하게 메일 보내줌)

저 @Value에서 고생을 많이했는데 저는 애초에 사용자 어레이를 받아와서 메일을 보내려고 했거든요.

근데 Spring에서는 기본적으로 설정의 @Value를 가져올때 어레이로 정상적으로 가져오지 못하고 에러를 뿜어냅니다. 이거때문에 며칠간 삽질을 좀 했습니다.



````

public void sendMail(String subject, String message, String to ) {

        SimpleMailMessage mailMessage = new SimpleMailMessage();

        // team email 분리 작업 ;
        // 주의 : spring yaml @value의 문제로 array값 못 불러옴. (꼭 확인 할 것 무한 삽질이 시작됨)
        String[] teamEmail = to.split(",");

`````

보이시죠?ㅋㅋㅋㅋㅋㅋ


그외엔 try-catch 문으로 간단히 메일을 보내시면 되겠습니다.


````
try {
            mailMessage.setSubject(subject);
            mailMessage.setText(message);
            mailMessage.setTo(teamEmail);
            mailMessage.setFrom("알람 메일<"+ sender +">");
            javaMailSender.send(mailMessage);
        } catch (Exception e) {
            log.error("메일 발송 오류 발생");
            e.printStackTrace();
        }
        log.info("#메일 발송 완료");

````


