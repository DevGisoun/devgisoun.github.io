---
title: Github 리포지토리에서 특정 폴더 및 파일 추적 제외
description: >-
  이번 포스팅에서는 임시 작업에 사용된 폴더 및 파일을 Git의 추적 대상에서 제외하고 앞으로 Git이 해당 파일들을 무시하도록 설정하는 방법을 설명하도록 하겠습니다.
author: gisoun
date: 2025-05-16 21:23:00 +0900
categories: [Git]
tags: [git, github]
pin: false
media_subpath: '/assets/posts/20250516'
---

## 개요

Git을 사용하다 보면 실수로 커밋 대상이 아닌 파일이나 폴더를 함께 커밋하고 푸쉬하는 경우가 종종 있습니다. 개발 환경 설정 파일, 로그 파일, 또는 테스트나 임시 작업에 사용된 폴더 등이 대표적이죠.

저 또한 [**매우 쉬운 Chirpy 테마 Github 블로그 만들기 ③ - 게시글 작성**](https://devgisoun.github.io/posts/creating-a-github-blog-3/) 에서 예제로 사용된 **임시 게시글**이 있습니다. 원래는 사용 후에 지워버리고 업데이트하려고 했는데, 해당 임시 게시글을 **언젠가 다시 재활용 될 수도 있겠다** 라는 생각이 들어서 그냥 Github 리포지토리에서만 제거하고 로컬에서는 추적되지 않게 설정하여 보관하려고 합니다.  

두 가지 방법이 있으니 편한 대로 하시면 됩니다.  

## 첫 번째: Github 리포지토리 페이지

> 이 방법은 Github 리포지토리 상에서 해당 폴더 및 파일을 삭제하는 커밋을 생성합니다. 즉 이 방법으로 파일을 삭제하고 로컬에서 **`git pull`**을 수행하면 **로컬 컴퓨터에서도 해당 파일이 삭제됩니다. 따라서 저처럼 로컬 파일을 유지하면서 Git 추적만 제외하고 싶다면 이 방법은 권장되지 않습니다.**
{: .prompt-info }

Github 블로그 리포지토리 페이지에서 삭제하고자 하는 파일 또는 폴더로 이동합니다. 그리고 우측 상단에 있는 <kbd>⋯</kbd> 버튼을 클릭하여 펼친 후 <kbd>Delete directory</kbd> 또는 <kbd>Delete file</kbd> 버튼을 클릭해 주세요.  

![image](delete-directory-and-file.png)
_'Delete directory' 또는 'Delete file' 버튼 클릭_

그러면 아래 이미지와 같이 바뀌게 되는 데, 여기서 <kbd>Commit changes…</kbd> 버튼을 클릭하면 커밋 메세지를 입력할 수 있는 팝업이 나타납니다.

![image](commit-changes.png)
_'Commit changes…' 버튼 클릭_

해당 팝업에서 **`Commit Message`**와 **`Extended description`**을 자유롭게 작성하신 후 <kbd>Commit changes</kbd> 버튼을 클릭하여 커밋해 주세요.  

그리고 로컬에서 해당 리포지토리를 참조하고 있는 프로젝트의 루트 디렉토리로 돌아와 터미널을 열고 아래 명령어를 실행하거나 Git 관리 GUI 툴을 사용하여 **Pull** 을 실행해 주세요.

```bash
git pull
```

그러면 Github 페이지에서 파일을 제거한 커밋 내용이 로컬에도 반영되어서 파일이 삭제되어 있을 겁니다.

![image](git-pull.png)
_'git pull' 명령어 입력 결과_

## 두 번째: `git` 명령어 입력

프로젝트의 루트 디렉토리에서 터미널을 열고 **`git rm --cached -r`** 명령어 뒤에 Git 추적 대상에서 제외하고자 하는 폴더 및 파일의 경로를 입력하여 명령어를 실행해 주세요. **띄어쓰기를 통해 여러 경로를 입력할 수 있습니다.**  
저는 **`assets/posts/temporary`** 폴더와 **`_posts/2025-05-10-temporary-post.md`** 파일을 추적 대상에서 제외하기 위해 아래와 같은 명령어를 실행하였습니다.

```bash
git rm --cached -r assets/posts/temporary _posts/2025-05-10-temporary-post.md
```

아래와 같은 실행 결과가 나타났다면 된 겁니다.

![image](git-rm.png)
_'git rm --cached -r' 명령어 입력 결과_

> **`git rm --cached -r`** 명령어 실행 시, 해당 파일들은 이미 Staging Area에서 제거된 상태가 되므로, **`git add`**를 따로 하지 않아도 커밋에 포함됩니다. 이때, **`git rm --cached -r`** 명령어로 Git 추적을 중지시켰더라도, 앞으로 해당 폴더에 새로운 파일이 추가되거나 수정될 때 Git이 다시 추적하려고 시도할 수 있습니다. 이를 방지하기 위해 [**다음 문단**](https://devgisoun.github.io/posts/ignore-in-a-gitHub-repository/#gitignore)을 통해 꼭! **`.gitignore`** 파일에 해당 경로를 추가해야 합니다.
{: .prompt-info }

## .gitignore

위의 [**첫 번째**](https://devgisoun.github.io/posts/ignore-in-a-gitHub-repository/#%EC%B2%AB-%EB%B2%88%EC%A7%B8-github-%EB%A6%AC%ED%8F%AC%EC%A7%80%ED%86%A0%EB%A6%AC-%ED%8E%98%EC%9D%B4%EC%A7%80) 또는 [**두 번째**](https://devgisoun.github.io/posts/ignore-in-a-gitHub-repository/#%EB%91%90-%EB%B2%88%EC%A7%B8-git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%9E%85%EB%A0%A5) 과정을 진행하셨다면 앞으로 Git이 추적 대상에서 제외된 폴더 및 파일을 다시 추적하려고 시도하지 않도록 **`.gitignore` 파일에 해당 경로를 추가하는 작업이 반드시 필요**합니다.  

프로젝트의 루트 디렉토리에 있는 **`.gitignore`** 파일을 엽니다. 만약 **`.gitignore`** 파일이 없다면 새로 생성하시면 됩니다.

그리고 **`.gitignore`** 파일의 원하는 위치에 Git의 추적 대상에서 제외된 폴더 및 파일의 경로를 아래와 같이 추가하시면 됩니다.

```
_posts/2025-05-10-temporary-post.md # 파일
assets/posts/temporary/ # 폴더
```

> 폴더의 경우 이름 뒤에 슬래시(`/`)를 붙여 해당 이름의 **디렉토리** 자체만 무시하도록 명확하게 지정합니다. 파일 이름과 겹칠 경우 발생할 수 있는 혼동을 방지할 수 있습니다!
{: .prompt-info}

![image](git-ignore.png)
_.gitignore 작성 예시_

이후 **`.gitignore`** 파일을 Git Staging에 추가한 뒤 커밋 및 푸쉬까지 해주세요. 명령어는 아래와 같습니다.
```bash
git add .gitignore
git commit -m ".gitignore 추가"
git push
```

다만 저의 경우 Git 명령어가 아닌 VSCode의 '소스 제어' 툴을 사용하기 때문에 아래 이미지와 같이 처리했습니다.

![image](git-staging.png)
_Staging에 추가한 변경 사항_

푸쉬까지 마치셨다면 이제 Git은 **`.gitignore`** 파일에 추가한 폴더 및 파일에 대한 추적을 완전히 중지하고 앞으로 발생할 변경사항들을 무시하게 됩니다.

---

## 마무리

오늘은 특정 목적을 위해 잠시 Git에 커밋했었지만 이후에 Git 추적 대상에서는 제외하고 싶은 파일이나 폴더를 어떻게 관리하는지에 대해 알아보았습니다.  

로컬에는 파일을 남겨두어 나중에 재활용할 수 있도록 하면서, Git 리포지토리에서는 해당 파일이 더 이상 추적되지 않도록 하는 것이 목표였는데 이 글이 도움이 되었기를 바랍니다!  

긴 글 읽어주셔서 감사합니다.
