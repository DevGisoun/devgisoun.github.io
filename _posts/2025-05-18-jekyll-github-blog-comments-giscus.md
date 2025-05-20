---
title: Jekyll 기반 Github 블로그에 댓글 기능 추가 (with. Giscus)
description: >-
  정적인 블로그는 빠르고 안정적이라는 장점이 있지만, 독자와의 소통이라는 측면에서는 아쉬움이 있습니다. 특히 Jekyll 기반으로 GitHub Pages에 호스팅하는 블로그에서는 별도의 솔루션 없이 동적인 기능인 댓글을 자체적으로 구현하기는 어렵습니다. 때문에 이번 포스팅에서는 Jekyll 기반의 Github 블로그에 Giscus를 이용하여 간단하고 효과적으로 댓글 기능을 추가하는 방법을 설명하도록 하겠습니다.
author: gisoun
date: 2025-05-18 14:39:00 +0900
categories: [Blog]
tags: [blog, github pages, jekyll, chirpy]
pin: false
media_subpath: '/assets/posts/20250518'
comments: true
---

## 왜 댓글 기능이 필요했나요?

저는 이 블로그를 일방적인 정보 공유 및 개발 히스토리를 기록하는 공간으로 사용하기 위해 제작하였지만, **독자들과의 상호작용을 통해 더 풍부한 콘텐츠를 만들거나 기존 프로젝트의 개선점을 찾을 수 있겠다**라는 생각이 들었습니다. 글에 대한 피드백을 받거나, 궁금한 점에 대해 답변해주고, 혹은 다른 독자들끼리 지식을 공유하는 장을 마련하여, 블로그를 단순 기록 저장소 역할을 넘어 살아있는 소통 공간으로 만들기 위한 댓글 기능이 필요했기에 이번 포스팅을 작성하려 합니다.

---

## Disqus vs Utterances vs Giscus

정적 블로그에 댓글 기능을 추가하는 솔루션으로는 대표적으로 **Disqus**, **Utterances**, **Giscus** 가 있습니다.

| 특징                    | Disqus                     | Utterances          | Giscus                    |
| ----------------------- | -------------------------- | ------------------- | ------------------------- |
| 저장 위치               | Disqus 자체 서버           | GitHub Issue        | GitHub Discussion         |
| 로그인 방식             | 자체 로그인 or 소셜 로그인 | GitHub 계정         | GitHub 계정               |
| 광고 유무               | ✅ 무료 플랜 기준           | ❌                   | ❌                         |
| 다크모드 지원           | ✅                          | ✅                   | ✅                         |
| 정적 블로그 호환        | ✅                          | ✅                   | ✅                         |
| 언어 설정               | 제한적                     | GitHub UI 따름      | GitHub UI 따름            |
| GitHub 저장소 권한 요구 | ❌                          | ✅ Issue 권한 필요   | ✅ Discussion 권한 필요    |
| 댓글 관리 방식          | 외부 대시보드              | GitHub Issue 페이지 | GitHub Discussions 페이지 |

이 중 **Giscus**를 선택한 이유는 아래와 같습니다.

### **GitHub Discussions 기반 저장 구조**
**Giscus**는 댓글 데이터를 GitHub Discussions에 저장합니다. Issue 기반의 **Utterances**보다 토론과 커뮤니티 관리에 적합하며, 프로젝트와 블로그의 피드백을 명확히 구분해 관리할 수 있습니다.  
**Utterances**이 아닌 **Giscus**을 선택한 가장 결정적인 이유이기도 합니다!

### **완전한 오픈소스 & 광고 없음**
**Disqus**는 무료 플랜에서 광고가 삽입되는 데 반해, **Giscus**는 광고 없이 깔끔한 UI를 제공합니다.  
**Disqus**이 아닌 **Giscus**을 선택한 가장 결정적인 이유이기도 합니다!

### **다크 모드 완벽 지원**
제가 사용하는 **Chirpy** 테마는 다크 모드를 지원하기 때문에, 댓글 UI도 이에 어울려야 합니다. **Giscus**는 시스템 다크 모드 설정을 자동 인식하며 수동으로 조정하는 것도 가능합니다.

### **GitHub 생태계와의 자연스러운 통합**
저처럼 블로그를 GitHub Pages에서 호스팅 중일 때, **Giscus**는 GitHub 계정으로 댓글 작성이 가능하여 별도의 회원가입 없이 원활한 사용자 경험을 제공합니다.

---

## Giscus 설치

### GitHub 리포지토리 Discussions 탭 활성화

먼저 블로그 리포지토리 페이지로 이동하여, <kbd>Settings</kbd> 탭을 클릭해 주세요.

![image](settings-tab.png)
_블로그 리포지토리의 'Settings' 탭_

그리고 스크롤을 내려 **`Features`>`Discussions`** 체크박스를 활성화해 주세요.

![image](discussions-checkbox.png){: w="567" h="621" }
_'Discussions' 체크박스 활성화_

체크하면 리포지토리에 <kbd>Discussions</kbd> 탭이 생긴 걸 확인할 수 있습니다.

![image](discussions-tab.png)
_블로그 리포지토리의 'Discussions' 탭_

### Giscus GitHub App 설치

[Giscus 앱 설치 페이지](https://github.com/apps/giscus)로 이동하여 <kbd>Install</kbd> 버튼을 클릭해 주세요.

![image](giscus-app-install-1.png)
_Giscus 앱 설치 페이지_

그리고 **`Only select repositories`** 를 클릭해 주세요. 아래 이미지와 같이 **`Select repositories`** 를 펼쳐, 댓글 기능을 적용할 블로그 리포지토리를 선택한 뒤에 <kbd>Install</kbd> 버튼을 클릭하면 **Giscus** 앱 설치가 완료됩니다.

![image](giscus-app-install-2.png)
_Giscus 앱 설치 페이지_

### Giscus 설정 및 코드 생성

[Giscus 설정 사이트](https://giscus.app/ko)로 이동해 주세요.  

페이지의 **`설정`** 문단에서 우리는 블로그 리포지토리에 사용될 **Giscus**의 설정을 구성해야 합니다. 아래의 과정을 참고하여 진행해 주세요!

**Giscus**에서 사용할 **`언어`**는 **한국어**로 설정합니다.

![image](giscus-config-1.png)
_언어_

**`저장소`**에는 **`<Github Username>/블로그 리포지토리명`** 형태로 입력하시면 됩니다.  

**<span style="color: green;">통과했습니다! 이 저장소는 모든 조건을 만족합니다.</span>** 문구가 나타나야 합니다!

![image](giscus-config-2.png)
_저장소_

**`페이지 ↔️ Discussions 연결`**에서는 **`Discussion 제목이 페이지 경로를 포함`**을 선택해 주세요.

![image](giscus-config-3.png)
_페이지 ↔️ Discussions 연결_

**`Discussion 카테고리`**에서는 댓글 Discussion이 생성되고 관리될 원하시는 Discussions 카테고리를 선택해 주시면 됩니다. 저는 **Comments**라는 별도의 카테고리를 Github Discussion 페이지에서 생성하였고 이를 선택했습니다.  

새 Discussion 카테고리를 생성하는 방법은 [**이곳**](https://devgisoun.github.io/posts/create-a-new-discussion/)을 참고해 주세요.

![image](giscus-config-4.png)
_Discussion 카테고리_

**`기능`**에서는 필요하다고 생각되는, 또는 사용해보고자 하는 **Giscus** 기능의 사용 여부를 체크하시면 됩니다.

![image](giscus-config-5.png)
_기능_

최종적으로 우리는 **`giscus 사용`** 문단에서 아래와 같은 구조의 **Giscus** 설정 코드를 볼 수 있게 됩니다!

```html
<script src="https://giscus.app/client.js"
        data-repo="DevGisoun/devgisoun.github.io"
        data-repo-id="R_data-repo-id"
        data-category="Comments"
        data-category-id="DIC_data-category-id"
        data-mapping="pathname"
        data-strict="0"
        data-reactions-enabled="1"
        data-emit-metadata="0"
        data-input-position="bottom"
        data-theme="preferred_color_scheme"
        data-lang="ko"
        crossorigin="anonymous"
        async>
</script>
```

그리고 로컬에서 블로그 리포지토리의 **`_config.yml`** 파일을 열어 **comments** 옵션을 찾아주세요. 우리는 이 **comments** 옵션의 내용을 위에서 설정한 **Giscus** 설정 코드에 맞게 아래와 같이 바꿀 것 입니다.

```yaml
comments:
  provider: giscus # [disqus | utterances | giscus]
  ...
  giscus:
    repo: data-repo
    repo_id: data-repo-id
    category: data-category
    category_id: data-category-id
    mapping: data-mapping
    strict: data-strict
    input_position: data-input-position
    lang: data-lang
    reactions_enabled: data-reactions-enabled
```

---

## 로컬 환경 테스트

만약 Jekyll 로컬 서버를 실행 중인 경우 위에서 **`_config.yml`** 파일을 수정했으므로 서버를 재시작해 주세요. 그리고 로컬 블로그 페이지에서 <kbd>Ctrl + Shift + R</kbd> 단축키를 입력하여 블로그 페이지의 캐시를 지우고 새로고침해 주세요.  

그리고 아무 게시글을 클릭하여 스크롤을 맨 아래로 내려주세요.

![image](comments-1.png)
_로컬 서버 내 Giscus 댓글 입력 창_

성공적으로 페이지 하단에 **Giscus** 댓글 입력 창이 보이는 걸 확인할 수 있습니다!  

> 만약 댓글 입력 창이 나타나지 않는다면, 해당 게시글의 **`YAML Frontmatter`** 옵션 중에 **`comments: false`** 로 설정되어 있는 지 확인해 주세요. **`comments`** 옵션이 **`true`** 여야만 댓글 입력 창이 활성화됩니다.
{: .prompt-info }

## 빌드 및 배포

로컬에서 댓글 입력 창이 나타나는 것을 확인하였으니, 이제 실제 블로그 페이지에서도 잘 나타나는 지 확인해야겠죠?  

**`_config.yml`** 파일을 커밋하고 푸쉬하여 블로그를 새로 빌드 및 배포한 뒤에 확인인하겠습니다.

![image](comments-2.png)
_실제 블로그 내 Giscus 댓글 입력 창_

실제 블로그 내에서도 댓글 입력 창은 잘 나타나며, 테스트 댓글을 작성하였는데도 문제없이 잘 입력되었습니다!

---

## 마무리

오늘은 **Giscus** 를 사용하여 정적인 Jekyll 기반 Github 블로그에 댓글 기능을 적용해 보았습니다.  

GitHub 생태계와 자연스럽게 통합되며, 설치도 매우 간단했고 UI도 깔끔해서 정말 만족스러운 선택이었습니다.

혹시 해당 게시글을 따라 진행 중에 궁금한 점이나 오류가 생기면 언제든 댓글로 질문 남겨주셔도 좋습니다. 😊

긴 글 읽어주셔서 감사합니다.
