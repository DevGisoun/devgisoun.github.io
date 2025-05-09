---
title: 매우 쉬운 Chirpy 테마 Github 블로그 만들기 ② - 로컬 서버 실행과 빌드 및 배포
description: >-
  지난 포스팅에서는 Chirpy Starter와 Docker, Dev Containers 확장 프로그램을 사용해 Chirpy 테마를 적용한 Github 블로그 생성과 컨테이너 환경에 리포지토리를 클론하여 개발 환경 구축까지 했습니다.</br>

  이번 포스팅에서는 로컬 서버를 실행하여 블로그를 로컬 환경에서 테스트하는 것과 수정 사항을 Github에 푸쉬하여 빌드부터 배포까지 하는 과정을 설명하도록 하겠습니다.
author: gisoun
date: 2025-05-09 23:48:00 +0900
categories: [Blog]
tags: [blog, github pages, jekyll, chirpy]
pin: false
media_subpath: '/assets/posts/20250509'
---

## 로컬 서버 실행

1. VSCode에서 <kbd>Ctrl + `</kbd> 단축키를 입력하여 터미널을 열어주세요.
   
   ![image](empty-terminal.png)
   _명령어를 입력할 터미널_


2. 터미널에서 아래 명령어를 입력하여 로컬 서버를 실행해 주세요.
   ```terminal
   $ bundle exec jekyll s
   ```
3. 로컬 서버가 실행되었다면 브라우저 주소창에 **http://127.0.0.1:4000** 을 입력해 블로그를 확인할 수 있습니다.  
   블로그 페이지가 정상적으로 나타나는지 확인해 주세요!
   
   ![image](empty-blog.png)
   _로컬 서버에서 실행 중인 블로그_


이렇게 실행한 로컬 서버를 통해 우리는 게시글 작성 또는 블로그 설정을 수정하였을 때의 변경 사항을 배포하기 전에 로컬에서 확인할 수 있습니다!

---

## 블로그 초기 설정

블로그의 전반적인 설정을 관리하는 파일은 최상위 경로에 있는 **`_config.yml`** 입니다. 이곳에서 블로그 타이틀, 프로필 사진 등 여러분의 스타일에 맞게 변경하시면 됩니다. 저는 기본적으로 아래와 같은 사항들을 **`_config.yml`** 파일에서 필수적으로 변경하시길 권장드립니다.

```yaml
lang: ko
timezone: Asia/Seoul # 블로그 빌드 시간대 설정
title: Dev. Gisoun # 원하는 블로그 타이틀
tagline: 개발자 기순 블로그 # 블로그 타이틀 아래에 보여질 한 줄 설명
url: "https://devgisoun.github.io" # "https://<username>.github.io"
avatar: /assets/img/avatar.jpg # /assets/img/<이미지 파일명> 또는 외부 이미지 URL
```

이외에도 여러 설정 항목들이 있으니 필요에 따라 변경해주셔도 됩니다.

**또한 `_config.yml` 파일은 수정 후 로컬 서버를 재시작해야만 변경 사항이 반영됩니다.**

![image](blog-with-settings.png)
__config.yml 설정이 반영된 블로그_

---

## 빌드 및 배포

1. 우선 최상위 경로에 **Gemfile.lock** 파일이 존재하는지 확인해 주세요. 만약 해당 파일이 없다면 터미널에 아래 명령어를 실행하여 생성해 주세요.
   ```bash
   $ bundle lock --add-platform x86_64-linux
   ```
2. VSCode에서 <kbd>Ctrl + Shift + G</kbd> 단축키를 입력하여 '소스 제어'로 이동 후 변경 사항을 반영할 파일들을 추가하고 <kbd>커밋</kbd>과 <kbd>변경 내용 동기화</kbd> 버튼을 클릭하여 커밋 및 푸쉬를 해줍니다.
   
   ![image](git-source-control.png)
   _소스 제어_

3. Github 블로그 리포지토리의 **Actions** 페이지로 돌아가면 변경된 사항들에 대해서 빌드 및 배포를 진행하는 것을 볼 수 있습니다.
   
   ![image](github-actions-1.png)
   _블로그 빌드 및 배포 중인 워크플로우_

4. 모든 워크플로우에 ✅ 표시가 되어있다면 배포까지 완료된 것이니 브라우저에 블로그 URL을 입력하여 확인합니다.  
   블로그 URL은 **`https://<username>.github.io`** 형태입니다.
   
   ![image](github-actions-2.png)
   _블로그 빌드 및 배포가 완료된 워크플로우_  

   ![image](deployed-blog.png)
   _배포된 블로그_


제 블로그 URL로 접속해보니 변경 사항이 성공적으로 반영되어 배포되었음을 확인하였습니다!

---

## 마무리

이것으로 컨테이너 개발 환경에서 로컬 서버 테스트까지 마쳤습니다.
또한, 변경 사항들을 Github에 커밋 및 푸쉬했을 때 성공적으로 빌드와 배포가 되는 것도 확인했습니다.
다음 포스팅에서는 마크다운(Markdown) 기반의 게시글을 작성하여 이를 업로드하는 과정을 다루어 보도록 하겠습니다.

긴 글 읽어주셔서 감사합니다.

