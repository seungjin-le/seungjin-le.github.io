---
title: 'GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 3 )'
author: <author_id>
categories: [ Front, AWS ]
tags: [ Front, AWS,S3,GitHub]
math: true
toc: true
mermaid: true
image: /images/backgrounds/awss3.png
---

### 1. 버킷 엔드 포인트 접속
버킷 웹사이트 엔드 포인트로 접속해보면 이런 페이지가 나옵니다

![1]()

>이 오류는 `AWS S3 버킷에 대한 접근이 거부되었다는 것`을 의미합니다. `403 Forbidden` 상태 코드와 함께 `AccessDenied` 메시지가 표시되어 접근이 거부된 것입니다.  
>  
>이 문제가 발생하는 이유는 `S3 버킷의 접근 제어 설정이 웹 사이트에 대한 공개 접근을 아직 설정하지 않았기 때문입니다`. 이 문제를 해결하려면 `S3 버킷 정책을 수정하여 해당 버킷과 그 안의 객체에 대한 공개 읽기 권한을 부여해야 합니다`.

### 2. 버킷 정책 변경
권한 탭으로 이동 하면 이런 페이지가 나옵니다
![2]()
여기서 순서대로 
  1. 퍼블릭 액세스 차단(버킷 설정)
     - 퍼블릭 액세스 차단이 활성화 되어 있다는건 차단 되있다는것이니 편집하기 버튼을 눌러 편집 페이지로 이동후 `모든 퍼블릭 엑세스 차단`을 풀어줍니다.
     - 그리고 변경사항 저장 버튼을 누른후 확인 모달에 `확인`을 입력후 저장
     - ![3]()
  2. 버킷 정책 작성
     - 퍼블릭 엑세스 차단을 비활성화 했으니 다음은 버킷 정책을 작성해 줍니다.
     - [AWS S3 버킷 정책 작성 예제](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-policy-language-overview.html)링크
     - 위 링크에서 버킷 정책 예제 JSON코드를 복사해서 붙여 넣기 해줍니다.
     ```javascript
     {
       // 이 정책 문서의 버전을 나타냅니다. 여기서는 2012-10-17로 설정되어 있습니다.
       "Version": "2012-10-17",
       // 정책의 고유 식별자입니다. 여기서는 ExamplePolicy01로 설정되어 있습니다.
       "Id": "ExamplePolicy01",
       // 정책에 대한 하나 이상의 선언을 포함하는 배열입니다. 각 선언은 특정 주체에 대한 액세스 권한을 지정합니다.
       "Statement": [
         {
           // 선언의 고유 식별자입니다. 여기서는 ExampleStatement01로 설정되어 있습니다.
           "Sid": "ExampleStatement01",
           // 선언의 효과로, 이 선언이 사용자에게 권한을 허용할지(Allow) 아니면 거부할지(Deny)를 결정합니다. 여기서는 Allow로 설정되어 있습니다.
           "Effect": "Allow",
           // 이 선언이 적용되는 주체를 지정합니다. 여기서는 AWS 서비스와 특정 IAM 사용자인 arn:aws:iam::123456789012:user/Dave에 대한 권한을 부여합니다.
           "Principal": {
             "AWS": "arn:aws:iam::123456789012:user/Dave"
           },
           // 이 선언이 허용하는 특정 작업을 나열합니다. 여기서는 s3:GetObject, s3:GetBucketLocation, s3:ListBucket 작업이 허용됩니다.
           "Action": [
             "s3:GetObject",
             "s3:GetBucketLocation",
             "s3:ListBucket"
           ],
           // 이 선언이 적용되는 AWS 리소스를 지정합니다. 여기서는 두 개의 리소스가 지정되어 있습니다. 
           // arn:aws:s3:::awsexamplebucket1/*는 버킷 내의 모든 객체를 나타내며, 
           // arn:aws:s3:::awsexamplebucket1는 버킷 자체를 나타냅니다.
           "Resource": [
             "arn:aws:s3:::awsexamplebucket1/*",
             "arn:aws:s3:::awsexamplebucket1"
           ]
         }
       ]
     }
     
     // 저는 연습이니 모든 객체에 대한 공개 읽기 권한을 허용코드를 사용합니다.
     {
       "Version": "2012-10-17",
       "Statement": [
         {
           "Sid": "PublicReadGetObject",
           "Effect": "Allow",
           "Principal": "*",
           "Action": [
             "s3:GetObject"
           ],
           "Resource": [
             "arn:aws:s3:::your-bucket-name/*"
           ]
         }
       ]
     }
     
     ```
     - 코드를 작성후 `변경 사항 저장`한다음 다시 `속성` 탭 으로 이동후 `버킷 엔드 포인트`로 가보면
     - ![5]()
     - 아까와는 다른 오류가 보이는데 이건 `AWS S3 버킷에` GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 2 )에서  
정적 웹사이트 호스팅 설정할때 입력한 `index.html`파일이 없기때문에 출력되는 겁니다.  

