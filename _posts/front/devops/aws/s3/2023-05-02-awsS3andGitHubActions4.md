---
title: 'GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 4 )'
author: <author_id>
categories: [ Front, AWS ]
tags: [ Front, AWS,S3,GitHub]
math: true
toc: true
mermaid: true
image: /images/backgrounds/awss3.png
---

### S3로 앱 자동 배포를 위한 yml 파일 완성하기
 `GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 1 )`에서 프로젝트에 생성한  
 
 `.github/workflows/node.js.yml`파일에 테스트까지 성공적으로 끝나면 `AWS S3 버킷에`소스코드를 전송할 코드를 추가해줍니다.   

### [S3애 소스코드 전송방법 링크](https://github.com/awact/s3-action)

이부분만 복사해서 `.github/workflows/node.js.yml`마지막에 복붙해줍니다.**(들여쓰기 중요)**

```yaml
- uses: awact/s3-action@master
  with:
    args: --acl public-read --follow-symlinks --delete
   env:
    SOURCE_DIR: './public'
    AWS_REGION: 'ap-northeast-2'
    AWS_S3_BUCKET: ${{ secrets.AWS_S3_BUCKET }}
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
    AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
 
#### 위 코드에서 각 코드들이 하는 역할입니다.
 
- ##### `uses` : awact/s3-action@master - 이 액션은 awact의 s3-action 저장소의 마스터 브랜치를 사용합니다. 이 액션은 AWS S3 버킷에 파일을 업로드하기 위한 것입니다.
  - ##### `with` :
    - ##### `args` : AWS CLI 명령에 전달되는 추가 인수입니다. 위 코드에서는 `--acl public-read`, `--follow-symlinks`, `--delete` 옵션을 사용합니다.
      - ##### `--acl public-read` : 업로드된 객체에 대한 공개 읽기 권한을 설정합니다.
      -   ##### `--follow-symlinks` : 심볼릭 링크를 따르고 대상 파일을 업로드합니다.
      -   ##### `--delete` : 원격 버킷에 있지만 로컬에 없는 파일을 삭제합니다.
  - ##### `env` : 이 단계에서 사용할 환경 변수를 설정합니다.
    - ##### `SOURCE_DIR` : 업로드할 파일이 있는 로컬 디렉토리 경로입니다. 여기서는 ./public을 사용합니다.
    - ##### `AWS_REGION` : 사용할 AWS 리전을 지정합니다. 예시에서는 'us-east-1'을 사용하고 있습니다.
    - ##### `AWS_S3_BUCKET` : 업로드할 AWS S3 버킷 이름을 저장하고 있는 GitHub secrets 변수입니다.
    - ##### `AWS_ACCESS_KEY_ID` : AWS 계정의 액세스 키 ID를 저장하고 있는 GitHub secrets 변수입니다.
    - ##### `AWS_SECRET_ACCESS_KEY` : AWS 계정의 시크릿 액세스 키를 저장하고 있는 GitHub secrets 변수입니다.

---

복붙한 코드에서 `SOURCE_DIR`부터 `AWS_SECRET_ACCESS_KEY`까지 수정해 줍니다

- #### `SOURCE_DIR` : `./public`에서 `./build`로 수정해줍니다, `npm build`를 해주면 빌드된 파일들이 `./build`로 들어가기 때문에 수정해 줍니다.
- #### `AWS_REGION` : `버킷을 생성할때 선택한 리전`을 입력해 줍니다. (`저는 서울로 했으니 ap-northeast-2`)
- #### `AWS_REGION`까지 작성하고 저장해 줍니다 그리고 `AWS_S3_BUCKET`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` 이 3개는 `AWS IAM`에서 사용자를 만들어 만들어 `ACCESS_KEY`를 생성해 주고 `GitHub`에서 `Project Setting`에서 따로 등록해 줘야합니다.

1. #### AWS 서비스 검색창에 `IAM`을 입력해 해당 페이지로 이동합니다.
   - ![13](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_13.png)
2. #### `IAM`페이지 좌측 사이드바에서 `액세스 관리 > 사용자`페이지로 이동해 줍니다.
   - ![12.5](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_12.5.png)
3. #### 우측 상단에 사용자 추가 버튼을 클릭후 페이지 이동
   - ##### `사용자 이름`은 나중에 알아볼 수 있게 작성해 줍니다.
   - ##### `AWS Management Console에 대한 사용자 액세스 권한 제공` 체크
   - ##### `IAM 사용자를 생성하고 싶음` 체크
   - ##### `콘솔 암호 / 자동 생성된 암호` 체크
   - ##### `사용자는 다음 로그인 시 새 암호를 생성해야 합니다(권장).` 체크후 다음 페이지로 이동
   - ![12](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_12.png)
4. #### 권한 설정
   - ##### `직접 정책 연결`체크
   - ##### `권한 정책`검색창에 `AmazonS3FullAccess`입력후 `AmazonS3FullAccess`체크후 다음 페이지로 이동
   - ![11](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_11.png)
5. #### 검토 및 생성
   - ##### 우측 하단에 `사용자 생성`클릭해 다음 페이지로 이동
6. #### 사용자 생성 완료
   - ##### 콘솔 로그인 세부정보가 저장된 `.csv`다운로드 해줍니다.
   > ##### CSV 
   > CSV(Comma Separated Values) 파일은 데이터를 저장하고 교환할 때 자주 사용되는 파일 형식입니다.
   > 
   > CSV의 사용처는 
   > 1. 데이터 저장 및 교환: CSV 파일은 다양한 데이터베이스, 스프레드시트 및 프로그래밍 언어 사이에서 데이터를 저장하고 교환하는 데 사용됩니다. 이러한 형식의 가볍고 간단한 구조는 크로스 플랫폼 데이터 이동에 매우 적합합니다.
   >
   > 2. 대용량 데이터 처리: CSV 파일은 대용량 데이터 세트를 빠르게 읽고 쓸 수 있기 때문에 대용량 데이터 처리 작업에 적합합니다.
   >
   > 3. 스프레드시트 및 데이터베이스 작업: 스프레드시트 프로그램 (예: Microsoft Excel, Google Sheets) 및 데이터베이스 관리 시스템 (예: MySQL, PostgreSQL)은 모두 CSV 형식을 지원합니다. 이를 통해 데이터를 손쉽게 가져오거나 내보낼 수 있습니다.
   >
   > 4. 데이터 분석 및 시각화: CSV 파일은 데이터 분석 및 시각화를 수행하는 데 사용되는 도구 및 라이브러리와 호환되는 표준 데이터 형식입니다. 이를 통해 데이터 사이언티스트와 분석가들은 손쉽게 데이터를 다룰 수 있습니다.
   >
   > 5. 데이터 전송 및 API 통합: 데이터를 전송하거나 다양한 API와 통합할 때 CSV 형식이 사용됩니다. 이를 통해 서로 다른 플랫폼 및 시스템 간에 데이터가 원활하게 이동할 수 있습니다.

   - ![10](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_10.png)
   - ##### 생성 후 사용자 페이지로 이동하면 사용자가 추가된 걸 볼 수 있습니다.
   - ![9](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_9.png)
7. #### 사용자 AccessKey 생성하기
   - ##### 생성된 사용자 이름을 클릭하면 사용자 상세 페이지로 이동됩니다, 사용자 상세페이지 중간에 `보안 자격 증명`탭으로 이동해 줍니다.
   - ![8](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_8.png)
   - ##### `보안 자격 증명`탭 에서 `액세스 키`섹션을 보면 액세스키가 없는걸 볼 수 있습니다.
   - ##### `액세스 키`섹션 에서 `액세스 키 만들기` 클릭해서 액세스 키 생성 페이지로 이동해 줍니다.
   - ##### `액세스 키 모범 사례 및 대안`페이지에서 `Command Line Interface(CLI)`체크하고 `위의 권장 사항을 이해했으며 액세스 키 생성을 계속하려고 합니다.`체크 후 다음 페이지로 이동
   - ![7](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_7.png)
   - ##### `설명 태그 설정`페이지는 선택사항이라 바로 다음 페이지로 이동해 줍니다.
   - ##### `액세스 키`생성을 완료하고 `.csv`파일을 다운로드해줍니다.
   - ![6](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_6.png)
8. #### GitHub에 AccessKey등록하기
   - #### `GitHub`의 `Project Repository`로 이동한다음 `Settings`페이지로 이동한다음 좌측 사이드 바에서 `secrets and variables / Actions`로 이동해줍니다.
   - ![4](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_4.png)
   - #### 처음에는 `Repository secrets`가 비어있으니 `New Repository secret`버튼을 클릭해 `Repository secrets`생성페이지로 이동해 줍니다.
   - ![3.5](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_3.5.png)
   - #### 여기선 아까 미뤄둿던 `AWS_S3_BUCKET`, `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`를 하나씩 생성해줍니다.
     - `Name` : `AWS_S3_BUCKET`, `Secret` : [GitHub Actions를 이용한 AWS S3로 앱 자동 배포하기( 2 )](https://seungjin-le.github.io/posts/awsS3andGitHubActions2/)에서 생성했던 버킷 이름을 넣어줍니다. 
     - `Name` : `AWS_ACCESS_KEY_ID`, `Secret` : 사용자 AccessKey를 생성할때 다운로드 받은 `.csv`파일을 열어보면 `Access key ID`와 `Secret access key`가 적혀 있으니 그중`Access key ID`를 복붙해줍니다.
     - `Name` : `AWS_SECRET_ACCESS_KEY`, `Secret` : 사용자 AccessKey를 생성할때 다운로드 받은 `.csv`파일의 `Secret access key`를 복붙해 줍니다.
   - ![3](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_3.png)
9. #### GitHub에 Push
   - #### 처음에 수정한 `.github/workflows/node.js.yml`파일을 GitHub에 Push해줍니다.
   - #### 그리고 `Project Repository`의 `Actions` 탭으로 이동해보면 에러가 난걸 볼 수 있습니다.
   - ![2](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_2.png)
   - #### 에러가 발생한 빌드를 클릭했을때 'Run npm test'에서 에러가 발생했을 경우
     - ![2](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_2.png)
       > 이 경우에는 테스트 파일 을 찾을 수 없어서 발생한 경우 입니다.
       > 이럴때는  Jest, Mocha, Jasmine 등의 테스트 프레임워크를 사용하여 테스트를 작성하거나
       >  `.github/workflows/node.js.yml`에서 `run: npm test`코드를 `run: npm test -- --passWithNoTests`로 수정해주면 됩니다.
   - #### `test`파일이 있을경우 우측 상단에 `Re-Run failed jobs`버튼을 클릭해 다시 빌드 합니다.
10. #### 수정후 다시 GitHub에 Push
    - ![1](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_1.png)
    - ![14](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_14.png)
11. #### S3 확인
    - ##### 정상적으로 빌드 된걸 확인 후 이전에 생성한 `AWS S3 Bucket`으로 이동해 보면 파일이 정상적으로 배포된 걸 볼 수 있습니다.
    - ![15](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_15.png)
12. #### 버킷 웹 사이트 엔드포인트 확인
    - ##### 버킷을 생성할때 생성된 엔드 포인트로 이동해보면 정상적으로 배포된걸 볼 수 있습니다.
    - ![16](/images/postImages/front/aws/s3/awsS3andGitHubActions4/s3_4_16.png)

