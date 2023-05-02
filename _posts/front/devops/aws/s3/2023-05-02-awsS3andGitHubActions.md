---
title: 'GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 1 )'
author: <author_id>
categories: [ Front, AWS ]
tags: [ Front, AWS,S3,GitHub]
math: true
toc: true
mermaid: true
image: /images/backgrounds/awss3.png
---

#### 1. `GitHub` 저장소에 `Project`를 `Push`합니다.

#### 2. Workflow 생성
  - `GitHub`에 `Project`를 `Push` 했다면 그다음은 `Workflow` 를 생성해줍니다
    - `Workflow` : `GitHub` 에 `Project`를`push` 한다면 GitHub에서는 이 프로젝트를 테스트를 합니다
  - `GitHub` 홈페이지에 접속후 `Repository` 에서 `Workflow` 를 생성할  `Project` 로 이동후 상단에 `Actions` 라는 탭을 클릭합니다.

    ![1](/images/postImages/front/aws/s3/s3_1.png)

  - 그러면 `GitHub`의 여러가지(배포, 보안, 자동화, 테스트 등) `Actions`를 볼 수 있습니다.

    ![2](/images/postImages/front/aws/s3/s3_2.png)

  - 그중 **`Continuous integration( 지속적인 통합 통칭 CI )`** 에서 `Node.js`를 선택해 줍니다.

    ![3](/images/postImages/front/aws/s3/s3_3.png)

  - 그러면 `/.github/workflows/node.js.yml` 생성하는 페이지가 나오는데 이미 기존적인 `CI` 셋팅이 되어 있습니다
  - node.js.yml
    > 저는 여기서 `run: npm ci` 를 `run: npm i` 로 수정했습니다.

    ```yaml
    # This workflow will do a clean installation of node dependencies, cache/restore them, build the source code and run tests across different versions of node
    # For more information see: https://docs.github.com/en/actions/automating-builds-and-tests/building-and-testing-nodejs
    
    name: Node.js CI
    
    # "main"이라는 브렌치에 push를 하거나 pull_request를 해주면 jobs의 코드가 동작합니다.
    on:
    push:
    branches: [ "main" ]
    pull_request:
    branches: [ "main" ]
    
    # 밑에 코드
    jobs:
    build:
    # ubuntu에서 실행
    runs-on: ubuntu-latest
    
        strategy:
          matrix:
            # 밑에 steps코드들이 노드 14.x버전에서 실행되고 16.x, 18.x 버전에서 실행되면서 프로젝트의 코드가
            # 다양한 node의 버전과 호환이 되는지 확인할 수 있습니다.
            # 일부 패키지, 라이브러리 또는 프레임워크는 특정 Node.js 버전에서만 정상 작동하기 때문에, 여러 버전에서 
            # 테스트하는 것이 중요합니다. 이를 통해 코드가 최신 Node.js 버전과 이전 버전에서도 문제없이 작동하는지 
            # 확인할 수 있으며, 호환성 문제가 발생하더라도 빠르게 인지하고 수정할 수 있습니다.
            node-version: [14.x, 16.x, 18.x]
            # See supported Node.js release schedule at https://nodejs.org/en/about/releases/
    
        steps:
          # actions/checkout@v3 액션을 사용하여 GitHub 
          # 리포지토리의 코드를 체크아웃합니다. 이로 인해 워크플로우가 실행되는 가상 머신에 프로젝트의 코드가 복사됩니다.
        - uses: actions/checkout@v3 
          # Node.js 버전을 설정하는 작업의 이름을 정의합니다. 여기서 ${{ matrix.node-version }}는 
          # 워크플로우 전략 매트릭스에서 정의한 Node.js 버전 변수를 나타냅니다.
        - name: Use Node.js ${{ matrix.node-version }}
          # actions/setup-node@v3 액션을 사용하여 워크플로우에서 원하는 Node.js 버전을 설정합니다.
          uses: actions/setup-node@v3
          # 액션에 전달할 추가 설정을 지정합니다.
          with:
            # 워크플로우 전략 매트릭스에서 정의한 Node.js 버전을 사용합니다.
            node-version: ${{ matrix.node-version }}
            # npm 종속성 캐시를 사용하여 빌드 속도를 높입니다
            cache: 'npm'
    
        # 프로젝트의 종속성을 설치합니다. npm ci는 package-lock.json 또는 
        # npm-shrinkwrap.json 파일을 기반으로 정확한 종속성 버전을 설치합니다.
        # 저는 여기서 ci를 i로 수정했습니다
        - run: npm ci 
    
        # package.json에 정의된 빌드 스크립트를 실행합니다. --if-present 옵션은 
        # 빌드 스크립트가 없으면 이 작업을 건너뛰게 합니다.
        - run: npm run build --if-present
    
        # 프로젝트의 테스트를 실행합니다. 이 작업은 package.json에 정의된 테스트 스크립트를 실행합니다.
        - run: npm test
    
        # 이 워크플로우는 프로젝트를 체크아웃한 다음, 원하는 Node.js 버전을 설정하고, 종속성을 설치하며,
        # 프로젝트를 빌드하고, 테스트를 실행하는 일련의 단계를 포함합니다. 이를 통해 프로젝트의
        # 빌드와 테스트가 원활하게 진행되는지 확인할 수 있습니다.
        ```

    수정이 끝나면 `Start Commit` 를 클릭해서 프로젝트 루트 디렉토리에 `.github/workflows/node.js.yml` 추가해줍니다.

    ![4](/images/postImages/front/aws/s3/s3_4.png)
