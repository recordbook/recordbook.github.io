---
layout: post
title:  "AWS Lambda Function과 SNS 서비스를 이용한 SMS(문자)보내기"
date:   2019-01-19 12:21:00
categories: AWS-Lambda-SMS
permalink: /archivers/aws/lambda/sms/push/1
---

## 개발 환경
Tool: Visual Studio Code  
Language: Node.js  


## Version 1.0 Code
```javascript
var AWS = require('aws-sdk');
var uuid = require('uuid');

AWS.config.update({region: 'us-east-1'});

var sns = new AWS.SNS();

var params = {
  Message: 'Node.js에서 보내는 AWS-SMS 문자입니다. 테스트.',
  MessageStructure: 'string',
  PhoneNumber: '+8210********'
};

sns.publish(params, function(err, data) {
  if (err) console.log(err, err.stack); // an error occurred
  else     console.log(data);           // successful response
});
```
Version 1.0 Code에서 추가되야 할 점은 AWS Lambda에서 위 코드를 실행시킬 수 있게 변경시켜야 한다는 점 입니다.  

## Version 1.1 Code
Lambda에서 구동될 수 있게 코드를 수정하였다.

## Version 1.2 Code
Lambda에서 구동될 수 있게 코드를 수정하였지만 CallBack 함수 때문에 순차 처리를 할 수 없다는 점이다.
이 점을 해결하기 위해 Async.js를 사용한다.
 * 비동기 처리를 순차적으로 처리하는 방법으로는 Async.js를 사용하거나 Node.js(7~ Version 이상)의 기본 탑재한 async/await 기능을 사용하면 된다.


## Reference
* [AWS SMS - Worldwide SMS Pricing](https://aws.amazon.com/ko/sns/sms-pricing/)  
* [Node.js v8.x Documentation](https://nodejs.org/docs/latest-v8.x/api/)  
* [AWS SDK for JavaScript](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/)  
* [StackOverFlow - How to send SMS using Amazon SNS from a AWS lambda function](https://stackoverflow.com/questions/38588923/how-to-send-sms-using-amazon-sns-from-a-aws-lambda-function)  
* [Loading Credentials in Node.js from a JSON File](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/loading-node-credentials-json-file.html) 
* [Sending SMS Messages with Amazon SNS](https://docs.aws.amazon.com/sdk-for-javascript/v2/developer-guide/sns-examples-sending-sms.html) 
* [Async Docs](http://caolan.github.io/async/docs.html#series)