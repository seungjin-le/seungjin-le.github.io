---
title: 'GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 2 )'
author: <author_id>
categories: [ Front, AWS ]
tags: [ Front, AWS,S3,GitHub]
math: true
toc: true
mermaid: true
image: /images/backgrounds/awss3.png
---

### 1. AWS S3 서비스에 가기

- AWS에 로그인한다음 콘솔홈으로 이동해줍니다

![1](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_0.png)

- 콘솔홈 상단에 검색창에 `S3`입력후 `S3`서비스 페이지로 이동 

![2](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_1.png)

### 2. AWS S3 버킷 만들기

- `S3`서비스 페이지 우측 상단에 버킷 만들기 클릭 

![3](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_2.png)

- 버킷 이름과 AWS 리전을 선택후 맨 하단에 버킷 생성 클릭.
  > AWS 리전(Region) : AWS 인프라를 지리적으로 나누어 배포한 것을 의미합니다. 사용자와 리전이 가까울수록 네트워크 지연을 최소화할 수 있습니다.

![4](/images/postImages/front/aws/s3awsS3andGitHubActions2/s3_2_4.JPG)

- 이렇게 생성된 버킷을 볼 수 있습니다

![5](/images/postImages/front/aws/s3/s3_2_5.JPG)

### 4. 생성한 버킷을 웹사이트 호스팅을 위해서 사용할 수 있게 설정하기

- 생성된 버킷의 이름을 클릭 시 해당 버킷의 정보 페이지로 이동해줍니다.

![6](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_6.png)

- 속성 탭 맨 아래로 스크롤을 내려주면 아래에 `정적 웹 사이트 호스팅`섹션이 `비활성화`돼있는걸 볼 수 있는데 우측에 `편집하기`를 클릭해 줍니다.

![7](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_7.png)

- 여기서 `정적 웹 사이트 호스팅`을 `활성화`상태로 한다 `인덱스 문서` 입력창에 `index.html`을 입력해 주고 `변경 사항 저장`클릭
  > AWS S3 버킷에서 정적 웹 사이트 호스팅을 설정할 때 "인덱스 문서(Index Document)"는 웹 사이트의 기본 페이지를 지정하는 설정입니다. 일반적으로 웹 사이트의 첫 페이지는 'index.html'이라는 파일로 지정됩니다.
  > 
  > 예를 들어, 사용자가 웹 사이트의 URL(예: www.example.com)을 입력하고 엔터를 누르면, 웹 브라우저는 기본적으로 인덱스 문서를 찾아서 표시합니다. S3 버킷 설정에서 인덱스 문서를 'index.html'로 지정한 경우, www.example.com에 대한 요청이 있을 때 브라우저는 www.example.com/index.html 페이지를 표시하게 됩니다.
  > 
  >  따라서 인덱스 문서는 웹 사이트에 접근했을 때 기본적으로 로드되는 페이지를 지정하는 역할을 합니다. S3 버킷의 정적 웹 사이트 호스팅 설정에서 인덱스 문서를 지정하면, 해당 파일이 기본 페이지로 사용되며, 사용자가 웹 사이트에 접속할 때 해당 페이지가 자동으로 표시됩니다.

![8](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_8.png)

- 그러면 호스팅을 편집했다는 알림을 받을 수 있습니다.

![9](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_9.png)

- 다시 속성 탭 맨 아래에 `정적 웹 사이트 호스팅`을 보면  `버킷 웹 사이트 엔드포인트`가 생성된걸 볼 수 있습니다


- AWS는 호스팅이 활성화된 버킷에 대한 고유한 URL을 생성합니다. 이 URL은 생성된 S3 버킷에 대한 정적 웹 사이트의 공개 엔드포인트입니다. 


- URL을 해석하면
  - `http://` : 프로토콜을 나타냅니다. 여기서는 HTTP 프로토콜을 사용하고 있습니다.
  - `react-s3-action-test-bucket` : 아까 생성한 버킷의 이름입니다.
  - `s3-website` : S3 버킷을 웹 사이트로 호스팅하기 위한 URL 구성 요소입니다.
  - `ap-northeast-2` : AWS 리전을 나타냅니다. 저의 경우 아까 선택한, 아시아 태평양 북동부 2 리전(서울)입니다.
  - `amazonaws.com` : AWS의 도메인입니다.

![10](/images/postImages/front/aws/s3/awsS3andGitHubActions2/s3_2_10.png)



