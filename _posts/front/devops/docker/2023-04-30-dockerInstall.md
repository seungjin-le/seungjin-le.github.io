---
title: "[ Mac Docker ] Docker설치 해보기"
author: <author_id>
categories: [ Front,  Docker]
tags: [ Front, DevOps, Docker, Mac]
math: true
toc: true
mermaid: true
image: /images/backgrounds/docker.png
---

# Docker 설치

## 1.다운로드

### [링크](https://www.docker.com/)

![1](/images/postImages/front/docker/install/1.png)

링크를 클릭하면 PC OS에 맞게 다운로드 버튼이 나옵니다 여기서 `Download Docker DeskTop` 를 눌러

`docker.dmg` 파일을 다운받은 후 설치해줍니다.

## 2. 설치

1번의 명령어를 클릭하면 2번 커맨드라인에 명령어가 자동으로 복사가 되는데 Enter를 누르면 복사된 명령어를 실행하면서 필요한 파일들을 설치해줍니다. 이작업을 4(Clone, Build, Run, Share)번 반복하면 설치가 완료됩니다.

![1](/images/postImages/front/docker/install/2.png)

![1](/images/postImages/front/docker/install/3.png)

![1](/images/postImages/front/docker/install/4.png)

![1](/images/postImages/front/docker/install/5.png)

## 3. 설치완료(확인)
설치가 끝나면 우측 상단에 도커 아이콘이 생긴걸 볼 수 있습니다

![1](/images/postImages/front/docker/install/7.png)

그리고 Docker Version 확인

```shell
docker -v
```

![1](/images/postImages/front/docker/install/8.png)


