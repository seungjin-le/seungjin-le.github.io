## GitPage

- ### [ BlogLink ](https://seungjin-le.github.io/)

- ### [ ThemeDocs ](https://chirpy.cotes.page/)

- ### Server Start
  ```shell
  bundle exec jekyll s
  ```


## 작성 규식
- 형식 : yyyy-mm-dd-제목.md
- 확장자는 .md
- 공백이 필요하면 하이픈(-)으로 구분.
- 작성한 파일은 _posts 디렉토리에

```markdown
---
title: "게시글 제목"
author: <author_id> 고정(_date/authors.yml > author_id.name)
categories: [ categories1, categories2 ]
tags: [ tag1, tag2, tag3.... ]
math: true
toc: true
mermaid: true
image: "게시글 상단 메인 이미지"
---
```

## 이미지 기능
#### 사이즈 조절
  ```markdown
  [Desktop View](/assets/img/sample/mockup.png){: w="700" h="400" }
  ```
