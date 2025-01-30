---
title: 매우 쉬운 Chirpy 테마 Github 블로그 만들기 ① - Jekyll Chirpy 테마 적용
description: >-
  Jekyll 테마와 Github를 활용해 정적 블로그를 만드는 것은 생각보다 간단합니다!</br>

  특히 Jekyll의 Chirpy 테마는 깔끔하게 정돈된 디자인을 제공하며 설정도 쉬워 빠르게 효과적인 블로그를 구축하는 데 적합하죠.</br>
  
  이번 포스팅에서는 Chirpy 테마를 사용해 Github 블로그를 만드는 과정을 설명하도록 하겠습니다.
author: gisoun
date: 2025-01-30 23:08:00 +0900
categories: [Blog]
tags: [blog, github pages, jekyll, chirpy]
pin: false
media_subpath: '/assets/posts/20250130'
---

## 사전 준비

블로그를 만들기 전에 몇가지 사전 준비가 필요합니다.

1. [Github 계정](https://github.com): Github 블로그를 만드는데 당연히 필수입니다!
2. [VSCode](https://code.visualstudio.com): 코드를 편집하고 작업할 때 사용하는 코드 편집기입니다.
   특히, 이번 과정에서 사용하게 될 **Dev Containers** 확장 프로그램과 함께 원활한 개발 환경을 제공합니다.
3. [Docker Desktop](https://docs.docker.com/desktop/setup/install/windows-install): 컨테이너 기반 개발 환경을 구축하기 위한 필수 도구로, 블로그를 로컬에서 테스트하고 배포하기 전에 안정적인 환경을 제공합니다. 참고로 Docker 계정도 따로 필요하니 [이곳](https://www.docker.com)에서 계정을 먼저 생성하셔야 합니다.

사전 준비 끝! 본격적인 블로그 제작을 시작합시다.

---


## Chirpy 템플릿 가져오기

1. [Chirpy Starter 페이지](https://github.com/cotes2020/jekyll-theme-chirpy)에 접속한 후 Github 로그인을 해주세요.
2. 우측 상단의 <kbd>Use this template</kbd>을 클릭한 후 <kbd>Create a new repository</kbd>를 선택합니다.
   
   ![image](use-this-template.png)
   _'Create a new repository' 선택_

3. 리포지토리 이름을 **`<username>.github.io`** 형태로 직접 입력합니다. **`<username>`** 부분에 본인의 Github username을 소문자로 입력하시기만 하면 됩니다. 이 리포지토리 이름은 블로그 URL로 사용될 것입니다.  
   그리고 <kbd>Create repository</kbd>를 클릭하여 리포지토리를 생성해줍니다.  
   
   ![image](create-a-new-repository.png)
   _username 입력 후 'Create repository' 선택_

---

이 리포지토리가 앞으로 여러분 블로그의 기본 구조가 됩니다!
   
   ![image](github-repository.png)
   _Chirpy Starter가 설치된 리포지토리_

---

## 블로그 배포 확인

본인 리포지토리에 **Chirpy Starter**가 설치된 것을 확인하셨나요?
그렇다면 자동으로 초기 버전 블로그에 대한 배포가 진행되고 있거나 이미 마무리 되었을 겁니다!

이를 확인하기 위해 리포지토리 페이지 상단의 <kbd>Actions</kbd>를 클릭해 주세요.
![image](github-actions.png)
_Github Actions 탭_

이곳에서 블로그가 빌드 및 배포되었는 지에 대한 워크플로우를 볼 수 있습니다. 현재는 초기 버전 블로그에 대한 워크플로우만 있을겁니다.  
만약 모든 워크플로우에 ✅ 표시가 되어있다면 성공적으로 배포가 완료된 것입니다.
![image](initial-blog-workflows.png)
_초기 버전 블로그에 대한 Workflows_

브라우저 주소창에 **`<username>.github.io`** 을 입력하여 본인의 블로그를 확인해 주세요.
![image](empty-blog-page.png)
_비어있는 블로그 페이지_

---

## 개발 환경 세팅

우리는 아직 아무런 세팅을 하지 않았기에 텅 빈 블로그만 볼 수 있습니다! 때문에 추후 게시글 업로드, 블로그 설정 등을 위한 개발 환경을 구축해야 합니다. 아래 과정을 따라와 주세요.

1. Docker Desktop을 실행합니다. 처음 실행 시 로그인을 요구할 수 있는데 **Work**와 **Personal** 중 **`사전 준비`** 단계에서 생성한 형태의 Docker 계정으로 로그인 하시면 됩니다. 저는 Personal 계정으로 로그인 하였습니다.  
   
   ![image](docker-first-run-screen.png)
   _Docker 첫 실행화면 (로그인 화면)_

2. VSCode를 실행한 후 좌측의 확장 프로그램 마켓플레이스에 접근하여 **Dev Containers**를 검색 후 설치하세요.  
   
   ![image](install-dev-containers.png)
   _VSCode에서 'Dev Containers' 확장 프로그램 설치_

## 컨테이너 환경 연결 및 블로그 리포지토리 클론

1. VSCode에서 <kbd>F1</kbd> 키를 눌러 명령 팔레트를 엽니다.
2. **"Dev Containers: Clone Repository in Container Volume"** 명령을 선택합니다.  
   
   ![image](clone-repository-1.png)
   _VSCode의 명령 팔레트에서 "Dev Containers: Clone Repository in Container Volume" 검색 후 선택_

3. **`1. Chirpy 템플릿 가져오기`** 과정에서 생성했던 블로그 리포지토리를 선택해 클론합니다.  
   
   ![image](clone-repository-2.png)
   _'컨테이너 볼륨의 Github에서 리포지토리 복제' 선택_  
   

   만약 VSCode에 Github 로그인이 안 되어있다면 아래 이미지와 같은 
창을 보게 될 텐데요. <kbd>허용</kbd>을 클릭하여 Github 계정 인증 페이지로 이동해 주세요.  

   ![image](clone-repository-3.png)
   _'허용' 선택_  

   해당 페이지에서 <kbd>Continue</kbd>를 클릭하여 로그인 및 인증을 하시면 됩니다.  
   
   ![image](clone-repository-4.png)
   _Github 계정 인증 페이지에서 'Continue' 선택_  

   인증 후 VSCode로 돌아왔을 때 아래 이미지와 같이 리포지토리를 선택할 수 있다면 성공한 겁니다! 복제할 블로그 리포지토리를 클릭해 주세요.  
   만약 명령 팔레트가 닫혀있으면 <kbd>F1</kbd> 키를 눌러 명령 팔레트를 연 뒤 이전 과정을 다시 시도해 주시면 됩니다.
   
   ![image](clone-repository-5.png)
   _VSCode 명령 팔레트에서 복제할 블로그 리포지토리 선택_  
   
1. Dev Containers를 통해 리포지토리를 복제하였다면 VSCode 상단의 타이틀이 아래와 같이 바뀌어 있을 겁니다.
   
   ![image](vscode-title.png)
   _Dev Containers와 연결된 리포지토리_  
   
   이어서 VSCode 터미널에서 Dev Containers의 환경 설정이 진행 중인 것을 확인하실 수 있을 겁니다.  
   설정이 모두 완료될 때까지 기다립시다.  
   
   ![image](setting-devcontainers.png)
   _Dev Containers의 환경 설정_  
   
2. 모든 설정이 완료되었다면 터미널에서 아무 키를 눌러서 마무리해 주세요!  
   
   ![image](devcontainers-setup-complete.png)
   _완료된 Dev Containers 환경 설정_  

---

## 결과

VSCode의 파일 탐색기가 아래 이미지와 같이 구성된 것을 확인하셨나요?  
이것으로 Github 블로그에 Chirpy 테마 적용 및 앞으로의 개발을 위한 컨테이너 환경에서의 모든 준비가 끝났습니다!

![image](vscode-file-explorer.png)
_VSCode 파일 탐색기에서 확인한 리포지토리_  

---

## 마무리

다음 포스팅에서는 로컬 서버를 실행하여 블로그를 직접 테스트하고 블로그 초기 설정을 한 뒤 이를 Github에 푸쉬하여 빌드, 배포까지하는 과정을 다루어 보도록 하겠습니다.

긴 글 읽어주셔서 감사합니다.

