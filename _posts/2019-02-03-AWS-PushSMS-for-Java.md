---
layout: post
title:  "AWS-SDK를 이용하여 SMS 보내기(Java)"
date:   2019-02-03 22:53:00
categories: AWS-SDK-Java
permalink: /archivers/java/aws/sdk/sns/1
---

내 기준으론 Amazon 공식 문서는 그다지 친절하지 않은 것 같다.
공식 문서를 봐도 이미 예전에 작성된 글이라 변경된 부분이 반영되지 않아 구글 검색을 계속 하게 된다.

한국 블로그에도 없는 내용들도 많고 해서 보통 대부분 영어로 검색하게 되고 찾은 내용을 토대로 코드를 작성하게 된다.  

```xml
<!-- https://mvnrepository.com/artifact/com.amazonaws/aws-java-sdk-sns -->
<dependency>
    <groupId>com.amazonaws</groupId>
    <artifactId>aws-java-sdk-sns</artifactId>
    <version>1.11.490</version>
</dependency>
```  

  

```java
// https://aws.amazon.com/ko/blogs/developer/client-constructors-now-deprecated/
AmazonSNS sns = new AmazonSNSClient();
```
위의 코드는 AWS-SDK의 1.11.84 버전에서 작동하던 SNS Client를 선언 방식이다.

하지만 현재(2019년 2월 3일 기준) 최신 버전은 1.11.490으로 저렇게 코드를 작성하게 되면
AmazonSNSClient 부분에 deprecated 표시가 되고 **The constructor AmazonSNSClient() is deprecated** 이와 같이 설명이 뜬다.

그럼 어떻게 사용해야 되는 것 일까? 궁금증이 생겨 AmazonSNSClient.clsss 소스를 들어가봤다.

```java
/**
     * Constructs a new client to invoke service methods on Amazon SNS. 
     * A credentials provider chain will be used that
     * searches for credentials in this order:
     * <ul>
     * <li>Environment Variables - AWS_ACCESS_KEY_ID and AWS_SECRET_KEY</li>
     * <li>Java System Properties - aws.accessKeyId and aws.secretKey</li>
     * <li>Instance profile credentials delivered through the Amazon EC2 metadata service</li>
     * </ul>
     *
     * <p>
     * All service calls made using this new client object are blocking, 
     * and will not return until the service call completes.
     *
     * @see DefaultAWSCredentialsProviderChain
     * @deprecated use {@link AmazonSNSClientBuilder#defaultClient()}
     */
    @Deprecated
    public AmazonSNSClient() {
        this(DefaultAWSCredentialsProviderChain.getInstance(), configFactory.getConfig());
    }
```
AmazonSNSClient.class에 들어가보니 **@deprecated use {@link AmazonSNSClientBuilder#defaultClient()}**이 부분을 발견할 수 있었다. 

class의 주석에 명시된대로 AmazonSNSClientBuilder를 사용하면 되겠구나 싶어서 다시 검색을 시도하여 아래와 같은 결과를 도출하였다.

```java
BasicAWSCredentials awsCreds = new BasicAWSCredentials(AccessKey, SecretKey);

AmazonSNSClientBuilder builder = AmazonSNSClientBuilder.standard();

AmazonSNS sns = builder.withRegion(Regions.US_EAST_1)
                        .withCredentials(new AWSStaticCredentialsProvider(awsCreds))
                        .build();
```
builder를 통해 위와 같은 형태로 구성하면 된다.  

이제 SMS(문자)를 발송하기 위해 아래와 같이 사용하면 됩니다.

```java
public static void main(String[] args) {

    BasicAWSCredentials awsCreds = 
        new BasicAWSCredentials(AccessKey, SecretKey);
    
    AmazonSNSClientBuilder builder = AmazonSNSClientBuilder.standard();

    AmazonSNS sns = builder.withRegion(Regions.US_EAST_1)
                            .withCredentials(
                                new AWSStaticCredentialsProvider(awsCreds)
                            )
                            .build();
    
    Map<String, MessageAttributeValue> smsAttributes = 
        new HashMap<String, MessageAttributeValue>();
    
    smsAttributes.put("AWS.SNS.SMS.SenderID", 
        new MessageAttributeValue()
            .withStringValue("mySenderId")
            .withDataType("String")
    );
    smsAttributes.put("AWS.SNS.SMS.MaxPrice", 
        new MessageAttributeValue()
        .withStringValue("0.50")
        .withDataType("String")
    );
    smsAttributes.put("AWS.SNS.SMS.SMSType", 
        new MessageAttributeValue()
        .withStringValue("Promotional")
        .withDataType("String")
    );
    
    sendSMSMessage(sns, "발송할 메시지", "+국가번호핸드폰번호", smsAttributes);
    
    
}

public static void sendSMSMessage(AmazonSNS sns
    , String message
    , String phoneNumber, Map<String, MessageAttributeValue> smsAttributes) 
{
    PublishResult result = sns.publish(new PublishRequest()
        .withMessage(message)
        .withPhoneNumber(phoneNumber)
        .withMessageAttributes(smsAttributes)
        );
    
    System.out.println(result); // result ex) {MessageId: 7ace45e4-31wr-5353-b2f2-17759c45d913}
}
```




## Reference  
* [AWS SDK for Java API Reference - 1.11.483](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/)
* [AWS 자격 증명 작업](https://docs.aws.amazon.com/ko_kr/sdk-for-java/v1/developer-guide/credentials.html)
* [AWSCredentialsProvider Example](https://www.programcreek.com/java-api-examples/index.php?api=com.amazonaws.auth.AWSCredentialsProvider)
* [AmazonSNSClientBuilder Example](https://www.programcreek.com/java-api-examples/index.php?api=com.amazonaws.services.sns.AmazonSNSClientBuilder)
* [SMS 메시지 전송](https://docs.aws.amazon.com/ko_kr/sns/latest/dg/sms_publish-to-phone.html)
