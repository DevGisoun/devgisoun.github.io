---
title: 매우 쉬운 Chirpy 테마 Github 블로그 만들기 ③ - 게시글 작성
description: >-
  지난 포스팅에서는 컨테이너에서의 로컬 서버 실행과 리포지토리의 변경 사항들을 Github에 커밋 및 푸쉬하여 블로그를 빌드 후 배포까지 하는 과정을 다뤘습니다.</br>

  이번 포스팅에서는 Markdown 문법을 기반으로 한 블로그 게시글을 작성하여 배포하는 과정을 설명하도록 하겠습니다.
author: gisoun
date: 2025-05-14 01:24:00 +0900
categories: [Blog]
tags: [blog, github pages, jekyll, chirpy]
pin: false
media_subpath: '/assets/posts/20250514'
---

# 이전 포스팅
[**매우 쉬운 Chirpy 테마 Github 블로그 만들기 ① - Jekyll Chirpy 테마 적용**](https://devgisoun.github.io/posts/creating-a-github-blog-1/)  
[**매우 쉬운 Chirpy 테마 Github 블로그 만들기 ② - 로컬 서버 실행과 빌드 및 배포**](https://devgisoun.github.io/posts/creating-a-github-blog-2/)  

## 게시글 파일 생성 및 기본 구조

새로운 게시글을 작성하려면 블로그 리포지토리 최상위 경로에 위치한 **`_posts`** 폴더에 Markdown(**`'md`**) 파일을 생성해야 합니다. 파일명은 아래와 같은 규칙을 따릅니다.

**파일명: `YYYY-MM-DD-제목.md`**
- **`YYYY-MM-DD`:** 게시글 작성 날짜입니다.
- **`제목`:** 게시글의 제목을 URL 친화적으로 `-`로 연결하여 작성합니다. 이유는 **파일명에 들어가는 제목은 URL에 표시되는 경로 역할을 할 뿐 실제 게시글에 보여지는 제목이 아니기 때문입니다!** 한글 제목도 가능은 하지만 URL 안정성을 위해 영어와 `-`으로 조합하시는 것을 추천합니다.

**예시: `_posts/2025-05-10-my-first-post.md`**

저는 아래와 같이 **`2025-05-10-temporary-post.md`** 라는 이름의 Markdown 파일을 **`_posts`** 폴더에 생성하였습니다.

![image](create-a-new-post.png)
__posts/2025-05-10-temporary-post.md 파일 생성_

Markdown 파일을 생성했다면, 해당 파일의 최상단에는 **`YAML Frontmatter`** 라는 메타데이터 블록을 작성해야 합니다.  
**`YAML Frontmatter`** 는 Jekyll에서 사용되는 작성 규칙으로, 게시글의 메타데이터를 처리하는 데 사용됩니다.  
저는 보통 아래와 같은 형태로 작성합니다.

```yaml
---
title: 게시글의 제목입니다!
description: >-
  게시글의 설명입니다.
author: gisoun
date: 2025-05-10 16:34:00 +0900
categories: [Blog]
tags: [blog, github pages, jekyll, chirpy]
pin: false
media_subpath: '/assets/posts/20250510'
---
```

- **`title`:** 게시글의 제목
- **`description`:** 게시글의 간력한 설명
- **`author`:** **`_data/authors.yml`** 파일에 작성된 **`{author_id}`** 를 입력하시면 됩니다. 이는 게시글 내에서 **`{author_id}`** 의 **`name`** 이 작성자의 이름으로 표시됩니다.  
   작성 예시는 아래와 같습니다.  
   ```yaml
   # author.yml 작성 예시
   gisoun: # {author_id}
     name: Dev Gisoun
   ```
- **`date`:** 게시글 작성 일시입니다. YYYY-MM-DD HH:MM:SS +0900 (한국 시간) 형식으로 작성합니다.
- **`categories`:** 게시글이 속할 카테고리 목록입니다. 최대 두 개를 지정할 수 있으며, 대괄호 [] 안에 쉼표로 구분하여 작성합니다.
- **`tags`:** 게시글을 설명하는 키워드 태그 목록입니다. 개수는 무한대로 지정할 수 있으며, 마찬가지로 대괄호 [] 안에 쉼표로 구분하여 작성합니다.
- **`pin`:** **`true`** 로 설정하면 해당 게시글이 메인 페이지 상단에 고정됩니다. 고정된 게시글들은 공개 날짜에 따라 역순으로 정렬됩니다.
- **`media_subpath`:** 해당 게시글에서 사용할 이미지와 같은 미디어 파일의 경로 접두사입니다. 이 기능을 사용하면 **`/assets/posts/background/image-1.png`** 와 같은 긴 경로 대신 **`![alt](image-1.png)`** 처럼 파일명만으로 리소스를 참조할 수 있어 아주 편리합니다!

---

## 게시글 작성하기

**`YAML Frontmatter`** 블록 작성 후에는 블록 아래에 Markdown 문법 기반의 내용을 자유롭게 작성하시면 됩니다!  
저는 아래와 같이 간단한 내용의 게시글을 작성했습니다.

```markdown
---
title: 게시글의 제목입니다!
description: >-
  게시글의 설명입니다.
author: gisoun
date: 2025-05-10 16:34:00 +0900
categories: [Blog]
tags: [blog, github pages, jekyll, chirpy]
pin: true
media_subpath: '/assets/posts/temporary'
---

# 안녕하세요, 개발자 기순입니다!

![gif](hello.gif)
_만나서 반갑습니다. 😊😊😊_

---

## 앞으로 다룰 주제

저는 이 블로그를 통해 제가 배우고 경험한 것들을 기록하고 공유하고자 합니다. 주요 내용은 다음과 같습니다.

* 개발 과정에서 겪은 `기술적인 문제 해결` 
* 관심이 있는 `개발 지식 및 트렌드` 공유 (*서적, 강의 리뷰 등*)
* 그 외 `공유하고 싶은 생각`

> 제가 쌓는 경험이 많은 개발자들에게 도움이 될 수 있도록, 앞으로 **양질의 게시글**로 자주 찾아 뵙겠습니다.

---

## 마무리

아직은 많이 부족하지만, 앞으로 차차 발전시켜 나가겠습니다.  
그리고 [**GitHub**](https://github.com/DevGisoun/) 팔로우는 환영입니다! ㅎㅎ;
```

이제 [매우 쉬운 Chirpy 테마 Github 블로그 만들기 ②](https://devgisoun.github.io/posts/creating-a-github-blog-2/)에서 다룬 내용대로, 로컬 서버를 실행하여 작성된 게시글을 미리보기 한 후에 빌드 및 배포까지 하겠습니다! 

---

## 게시글 미리보기

터미널에 아래 명령어를 입력하여 로컬 서버를 실행해 주세요.
```terminal
$ bundle exec jekyll s
```

그리고 브라우저 주소창에 **http://127.0.0.1:4000** 을 입력하여 작성한 게시글을 확인해 보겠습니다.

![image](preview-a-new-post-1.png)
_새로 작성한 게시글 제목_

블로그 메인페이지에 새로 작성한 게시글의 제목이 보이는 것을 확인할 수 있습니다.  
게시글 제목을 클릭하여 내용까지 확인해 보도록 할까요?

![image](preview-a-new-post-2.png)
_새로 작성한 게시글 내용_

게시글 내용 역시 Markdown 문법이 잘 적용된 채로 확인되었습니다!

---

## 게시글 빌드 및 배포

VSCode의 '소스 제어'로 이동 후 작성한 게시글과 게시글에 사용된 미디어 파일들을 모두 선택하여 커밋 및 푸쉬까지 합니다.

![image](git-source-control-1.png)
_게시글과 미디어 파일이 선택된 '소스 제어'_

만약 커밋 후 '소스 제어'에서 <kbd>변경 내용 동기화</kbd> 버튼이 보이지 않는다면 아래 이미지와 같이 '변경 내용' 우측의 <kbd>⋯</kbd> 아이콘을 클릭하여 <kbd>Push</kbd> 를 클릭하시면 됩니다.

![image](git-source-control-2.png)
_'소스 제어'의 'Push' 버튼_

블로그 URL로 접속해보니 새 게시글이 성공적으로 배포되어 목록에 보이는 것을 확인할 수 있었습니다!

![image](a-new-post-1.png)
_새로 작성한 게시글 제목_

내용도 잘 나오네요 ㅎㅎ

![image](a-new-post-2.png)
_새로 작성한 게시글 내용_

---

> 만약 **Github Actions** 워크플로우에 빌드 및 배포까지 완료된 것을 확인하였는데 새 게시글 또는 변경 사항이 반영되지 않았다면?
{: .prompt-warning }

## 블로그 변경 사항 업데이트

푸쉬한 내용이 배포된 후 블로그 URL 접속 후 새로 고침을 하시면 아래와 같은 팝업이 나타날 겁니다.

![image](update-content.png)
_블로그 내용 업데이트 팝업_

여기서 <kbd>Update</kbd> 버튼을 클릭하면 변경 사항이 반영된 것을 확인할 수 있습니다!

---

## 추가적인 가이드

이 외에 더 자세한 작성 방법은 [Markdown 문법 가이드](https://www.markdownguide.org/basic-syntax/) 또는 **Chirpy 테마의 공식 가이드** [Writing a New Post](https://chirpy.cotes.page/posts/write-a-new-post/) 페이지를 참고하시면 큰 도움이 됩니다!  
저 또한 언젠가 Markdown 문법에 대해 자세히 다루게 된다면 블로그에 업로드 하도록 하겠습니다. 😊😊

---

## 마무리

오늘은 Chirpy 테마를 적용한 Jekyll 기반 Github 블로그에 Markdown 문법을 사용하여 게시글을 작성하는 방법을 알아보았습니다.  

사실 블로그를 시작하기 전에는 Markdown 을 사용하여 글 작성하는 것 쯤은 뚝딱 할 줄 알았는데, **막상 해보니 이거 꽤 까다롭네요ㅋㅋ;; 비효율적이기도 하고..**  
직접 Markdown 을 사용하지 않고 별도의 **`WYSIWYG`** 에디터라도 사용해서 작성하든지 해야겠어요.  

이로써 Github 블로그 제작 과정과 기본적인 사용법에 대한 내용은 모두 다룬 것 같습니다. 추가적인 기능을 더하는 것은 **`매우 쉬운 Chirpy 테마 Github 블로그 만들기`** 라는 주제의 범위를 넘어선다고 판단하여 이만 마치겠습니다!  

긴 글 읽어주셔서 감사합니다.
