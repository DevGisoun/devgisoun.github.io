---
title: Github 리포지토리의 Discussion 카테고리 추가
description: >-
  
author: gisoun
date: 2025-05-20 17:20:00 +0900
categories: [Blog]
tags: [github]
pin: false
media_subpath: '/assets/posts/20250520'
comments: true
---

## 사전 준비

먼저 리포지토리에 <kbd>Discussions</kbd> 탭이 활성화되어 있어야 합니다. 만약 리포지토리의 <kbd>Discussions</kbd> 탭이 활성화 되어 있지 않아 보이지 않는다면 [**이곳**](https://devgisoun.github.io/posts/jekyll-github-blog-comments-giscus/#github-%EB%A6%AC%ED%8F%AC%EC%A7%80%ED%86%A0%EB%A6%AC-discussions-%ED%83%AD-%ED%99%9C%EC%84%B1%ED%99%94)을 참고해 주세요.

---

## Discussion 카테고리 추가

<kbd>Discussions</kbd> 탭 내에 좌측을 보시면 **Categories** 부분에 ✏️ 아이콘이 있습니다.

![image](categories.png){: w="339" h="311" }
_Categories_

해당 아이콘을 클릭하여 **Manage discussion categories** 페이지로 이동해 주세요.

그리고 우측의 <kbd>New category</kbd> 버튼을 클릭해 주세요.

![image](manage-discussion-categories.png)
_Manage discussion categories 페이지지_

그러면 **Create category** 페이지로 이동됩니다.

![image](create-category-1.png)
_Create category 페이지_

- **`Category name`:** 카테고리의 이름과 아이콘을 지정합니다.
- **`Description`:** 해당 카테고리의 용도나 내용을 간단히 설명하며, 필수는 아닙니다.
- **`Discussion Format`:** 생성할 카테고리에서 사용될 **Discussion** 의 형식을 정합니다.
  - **`Open-ended discussion`:** 자유로운 대화, 아이디어 공유, 또는 일반적인 토론을 위한 형식
  - **`Question / Answer`:** 질문 게시 및 질문에 대한 답변을 받고, 답변 중 하나를 채택할 수 있는 형식
  - **`Announcement`:** 프로젝트 업데이트, 공지사항 등 일방적으로 정보를 전달하는 데 주로 사용되는 형식. 오직 권한이 있는 사람만이 토론을 게시할 수 있으나, 댓글은 누구나 자유롭게 작성 가능
  - **`Poll`:** 투표를 생성하고 결과를 확인할 수 있는 형식
- **`Add this category to a section (optional)`:** 생성하려는 카테고리를 기존의 섹션에 포함시킬지 여부를 결정합니다. 필수는 아닙니다.

저의 경우 블로그 내 댓글 기능을 적용하기 위해 **Giscus** 를 사용했는데, 댓글이 관리될 별도의 Discussion 카테고리를 아래와 같이 구성하였습니다.

![image](create-category-2.png)
_Create category 페이지_

입력란을 모두 작성하였다면 <kbd>Create</kbd> 버튼을 클릭하여 생성해 주세요.

![image](comments-category.png)
_생성된 'Comments' 카테고리_

성공적으로 **`Comments`** Discussion 카테고리가 생성된 것을 확인할 수 있습니다!

---

## 마무리

사실 저는 Github의 <kbd>Discussions</kbd> 탭을 적극 활용할 생각은 없었는데, 최근에 **Giscus** 를 사용하여 블로그 내 댓글 기능을 설정하다 보니 댓글들을 관리할 별도의 카테고리를 생성할 필요성을 느꼈고 **이 내용을 블로그에 공유하면 좋겠다** 싶어서 이번 포스팅을 작성하게 되었습니다!  

많은 분께 도움이 되었으면 좋겠습니다.  

긴 글 읽어주셔서 감사합니다.
