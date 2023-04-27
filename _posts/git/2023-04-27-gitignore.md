---
title: "[ Git ] gitignore"
author: <author_id>
categories: [ Git, GitHub ]
tags: [ Git, GitHub ]
math: true
toc: true
mermaid: true
image: /images/backgrounds/github.png
---


## .gitignore 란?

- .gitignore 는 원격서버에 프로젝트 파일을 을 올릴 때 불필요한 파일들을 업데이트 하지 않도록 제외할 파일들의 목록을 만드는 파일

## .gitignore을 왜 사용 하는가?

- 프로젝트를 하다보면 프로젝트 내부의 더미 파일이나 API Key등 외부에 공개하면 안되는 파일들이 있습니다 그런경우에 .gitignore라는 파일을 생성해서 관리한다면 원경저장소에 pushㄹ를 해도 노출되지 않는 장점이 있습니다

## .gitignore 생성 하기

- 처음에 저장소를 만들때 Add .gitignore에 체크를 한다면 생성할수 있습니다

![img](/images/postImages/git/githubgitgnore.png)

- 처음 저장소를 생성할때  Add .gitignore를 체크를 하지 않았다면 수동으로 추가를 해줄수도 잇습니다

    ```jsx
    // .gitignore 파일 생성
    
    touch .gitignore
    ```


#### [.gitignore의 내용을 자동으로 구서앻주는 사이트](https://www.toptal.com/developers/gitignore)
프로젝트에 사용된 언어, 개발툴, 프레임워크, OS 등 제외해야할 항목들을 생성해 줍니다
