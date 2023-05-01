---
title: 'AWS EC2에서 Docker설치하기'
author: <author_id>
categories: [ Docker, AWS ]
tags: [ Docker, AWS,EC2,Ubuntu]
math: true
toc: true
mermaid: true
image: /images/backgrounds/awsec2.png
---



### AWS에 로그인(가입)
> 먼저 [AWS에](https://aws.amazon.com/ko/) 접속후 가입합니다
> 가입후 아래 이미지처럼 콘솔 홈으로 이동합니다.
> 페이지 중간쯤에 솔루션 구축에서 **가상 머신 시작** 클릭

![image](/images/postImages/front/aws/ec2/ec2_1.JPG)

> 인스턴트 시작 페이지에서 `Name and Tags`는 어짜피 연습이니
> 아무거나 입력해줍니다. 그리고 `애플리케이션 및 OS 이미지(Amazon Machine Image)` 섹션에서
> `Ubuntu`클릭

![image](/images/postImages/front/aws/ec2/ec2_2.JPG)

> `키페어 생성`모달에서 키페어 이름도 아무거나 입력후 키패어 생성을 클릭시
> `키페어이름.pen`파일이 다룬로드 됩니다.
> EC2에서 키페어는 인스턴스에 로그인하는 데 사용되는 암호화된 키 정보입니다. 키 페어는 공개 키와 개인 키의 쌍으로 구성되어 있습니다.
> 나중에 인스턴스에 로그인하려면 이 키 페어의 개인 키가 필요합니다. 
> 키 페어를 생성하면 개인 키를 다운로드할 수 있으며, 이 개인 키를 사용하여 인스턴스에 SSH 접속할 수 있습니다.
> 키 페어는 인스턴스에 로그인하는 데 사용되므로 개인 키를 보안하고 안전한 위치에 저장하는 것이 중요합니다. 
> 개인 키가 손실되면 해당 인스턴스에 접근할 수 없으며, 다른 사람이 개인 키를 획득하면 인스턴스의 보안이 위협될 수 있습니다.


![image](/images/postImages/front/aws/ec2/ec2_3.JPG)

> 기본적은건 다끝났으니 우측에 `인스턴스 시작` 클릭


![image](/images/postImages/front/aws/ec2/ec2_4.JPG)

> 인스턴스가 생성됬으니 EC2 인스턴트 탭으로 이동

![image](/images/postImages/front/aws/ec2/ec2_5.JPG)

> 인스턴스를 선택후 연결버튼 클릭

![image](/images/postImages/front/aws/ec2/ec2_6.JPG)

> 사용자 이름도 아무거나 입력하고 연결을 클릭시
> Ubuntu를 실행중인 시스템의 명령 프롬프트(터미널)페이지로 로 이동되며, 이 화면에서는 
> 시스템의 기본 정보와 상태가 표시되고 있습니다.
> 
![image](/images/postImages/front/aws/ec2/ec2_7.JPG)

> 지금부터 `Docker`를 설치해주면 됩니다
> 현제 `Ubuntu 22.04.2`버전에서 `Docker`를 설치하고 사용하는 방법까지 잘 정리된 사이트를 따라
> [우분투에서 도커를 설치하고 사용하는 방법](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04)
> 

![image](/images/postImages/front/aws/ec2/ec2_9.JPG)

> 설치 완료

![image](/images/postImages/front/aws/ec2/ec2_10.JPG)


