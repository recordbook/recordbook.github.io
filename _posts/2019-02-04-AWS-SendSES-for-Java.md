---
layout: post
title:  "AWS-SDK를 이용하여 Email 보내기(Java)"
date:   2019-02-04 15:23:00
categories: AWS-SDK-Java
permalink: /archivers/java/aws/sdk/ses/1
---

SES또한 SNS와 동일한 방법으로 메일을 보낼 수 있다.

```xml
<!-- https://mvnrepository.com/artifact/com.amazonaws/aws-java-sdk-ses -->
<dependency>
    <groupId>com.amazonaws</groupId>
    <artifactId>aws-java-sdk-ses</artifactId>
    <version>1.11.490</version>
</dependency>
```  
위와 같이 pom.xml에 종속성을 추가한다.

아래와 같이 소스코드를 작성하면 된다.

```java
public static void main(String[] args) {
		
    String from = "보내는 사람";
    String to = "받는 사람";
//	String configSet = "ConfigSet"; // Optional
    String subject = "Amazon SES test (AWS SDK for Java)";
    String htmlBody = "<h1>Amazon SES test (AWS SDK for Java)</h1>"
                + "<p>This email was sent with <a href='https://aws.amazon.com/ses/'>"
                + "Amazon SES</a> using the <a href='https://aws.amazon.com/sdk-for-java/'>" 
                + "AWS SDK for Java</a>";
    String textBody = "This email was sent through Amazon SES "
                + "using the AWS SDK for Java.";
    
    AWSCredentials awsCreds = new BasicAWSCredentials(AccessKey, SecretKey);
    
    AmazonSimpleEmailServiceClientBuilder builder = AmazonSimpleEmailServiceClientBuilder.standard();
    
    AmazonSimpleEmailService ses = builder.withRegion(Regions.US_EAST_1)
                                .withCredentials(new AWSStaticCredentialsProvider(awsCreds))
                                .build();
    
    try {
        SendEmailRequest request = new SendEmailRequest()
                .withDestination(new Destination().withToAddresses(to))
                .withMessage(new Message().withBody(
                            new Body()
                                .withHtml(new Content("UTF-8").withData(htmlBody))
                                .withText(new Content("UTF-8").withData(textBody))
                                )
                            .withSubject(new Content().withCharset("UTF-8").withData(subject))
                            )
                .withSource(from);
//					.withConfigurationSetName(configSet); // Optional
        
        ses.sendEmail(request);
        System.out.println("Email sent!");
    } catch (Exception e) {
        e.getMessage();
    }

}
```




## Reference  
* [AWS SDK for Java API Reference - 1.11.483](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/)
* [AWS 자격 증명 작업](https://docs.aws.amazon.com/ko_kr/sdk-for-java/v1/developer-guide/credentials.html)
* [AWS SDK for Java를 사용하여 이메일 전송](https://docs.aws.amazon.com/ko_kr/ses/latest/DeveloperGuide/send-using-sdk-java.html)
