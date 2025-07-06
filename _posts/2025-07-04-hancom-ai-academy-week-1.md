---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 1주차 후기"
description: >-
  강의 실습 전 준비 및 HTML, CSS, Javascript의 기초 이해를 위한 실습.
author: gisoun
date: 2025-07-04 10:05:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, html, css, javascript, js]
pin: false
media_subpath: '/assets/posts/20250704'
published: true
---

> 2025\. 6\. 30\. ~ 2025\. 7\. 4\.

K-디지털 트레이닝 지원을 통해 **한컴 AI 아카데미 2기**에 합격하여 첫 주차 강의를 마쳤습니다.  

앞으로 강의 주차에 과제가 있을 경우, 또는 추후 하게 될 프로젝트 진행 상황에 대해 해당 블로그에 기록할 예정입니다.

## 지원 물품

한컴 AI 아카데미 혜택 중 가장 마음에 들었던 것은 **노트북 무료 대여**입니다.  

두 가지 노트북 중 하나를 선택할 수 있었는데, **`화면이 큰 대신 무거운 노트북 vs 화면은 작아도 가벼운 노트북`**  

![image](laptop-1.png)
_LG 그램 i5 모델_

저는 고민도 없이 **화면은 작아도 가벼운 노트북**을 선택했습니다. 매일 노트북과 두꺼운 교재를 들고 편도 1시간 거리를 왔다 갔다 해야 하는데 차마 무거운 놈을 고를 수는 없겠더라고요. 무엇보다 두 노트북을 동시에 들고 비교해 보면 무게 차이가 확실히 납니다.  

가벼운 것이 최고입니다👍👍

![image](welcome-kit-1.png)
_웰컴 키트_

노트북 말고도 한컴과 스나이퍼 팩토리에서 제공하는 **웰컴 키트**와 **교재**도 무료로 지원해 줍니다. 웰컴 키트에는 **노트**, **캘린더**, **약간의 간식** 등이 있었습니다.

저는 노트북을 받자마자 **`Visual Studio Code, Docker, Postman`** 등 개발에 필요한 기본 프로그램들을 설치했습니다.

---

## 권장 VSCode 확장 프로그램

본격적인 강의에 앞서, 앞으로의 개발 과정에서 편의성을 높이기 위해 강사님께서 추천해 주신 **VSCode 확장 프로그램**들 중 몇 가지를 설치했습니다.

### Tailwind CSS IntelliSense

![image](tailwind-css-1.png){: w="150" h="150" }
_Tailwind CSS 확장 프로그램_

추후 진행할 React 강의를 위해 설치하였습니다.

- **`CSS 미리보기:`** class 위에 마우스를 Hover하여 해당 class가 적용하는 CSS 스타일을 바로 확인할 수 있습니다.
- **`class 자동 완성:`** Tailwind CSS에 내장된 class 목록을 자동으로 제시해 줍니다. 일일이 공식 문서에서 서칭할 필요가 없다는 것은 진짜 큰 장점입니다.
- **`Linting:`** 중복된 class나 존재하지 않는 class에 대해 오류 표시를 해줌으로써 코드의 일관성을 챙길 수 있습니다.

### Prettier

![image](prettier-1.png){: w="150" h="150" }
_Prettier 확장 프로그램_

사실 **Prettier**는 딱히 선호하지 않았는데, 아무래도 강제로 코드 스타일을 지정하는 것과 몇몇 경우에는 코드 가독성을 되려 해치는 듯한 포맷팅 때문입니다. 하지만 후반기에 예정된 팀 프로젝트를 위해서 미리 경험해 보기로 했습니다. 쓰다 보면 분명 익숙해질 겁니다.  

개인마다 편하게 느끼는 코드 스타일은 다르기 때문에 일관성이 중요시되는 협업에서는 **Prettier**가 반 필수적이라고 생각됩니다.

### Live Server

![image](live-server-1.png){: w="150" h="150" }
_Live Server 확장 프로그램_

순수 **`HTML/CSS`**, **`Javascript`** 만을 사용하여 웹 페이지를 만들 때, 수정하고 나서 매번 브라우저에서 새로고침을 하는 건 은근히 번거로운 일입니다. 하지만 **Live Server**는 코드를 저장하는 즉시 웹페이지에 변경 사항이 실시간으로 반영되게 해줍니다.  

아카데미 초반에 진행한 **`HTML/CSS`**, **`Javascript`** 강의에서 **`React`**를 미리 사용해 보는 것 같은 경험을 줘서 굉장히 만족스러웠습니다.

---

## HTML/CSS 기반 레이아웃 구조 잡기

본격적인 **`React`** 사용에 앞서, 순수 **`HTML/CSS`** 만을 사용하여 페이지의 레이아웃 구조를 잡아보는 시간을 가졌습니다. 강의 및 과제에 사용된 예제 페이지는 [Dribble](https://dribbble.com/)에 업로드된 [Pinterest Redesign - UX concept](https://dribbble.com/shots/14470620-Pinterest-Redesign-UX-concept) 페이지와 [Google NotebookLM](https://notebooklm.google.com/notebook/) 페이지였습니다.  

시작은 가볍게 레이아웃을 구현하는 것이 아닌, 수기로 페이지의 레이아웃을 분해하고 필요한 CSS 속성을 정의하는 것에 집중하였습니다.  

![image](pinterest-1.png)
_Pinterest Redesign - UX concept 원본 페이지_

**Pinterest Redesign - UX concept** 원본 페이지를 보고, 요소를 하나하나 분해하여 대략적인 구조를 파악하였습니다.

![image](layout-1.png)
_Pinterest Redesign - UX concept 레이아웃 분해_

이후 분해한 각 요소를 다시 조립하여 최종적으로 레이아웃의 전체적인 구조를 정의하였습니다.

![image](layout-2.png)
_Pinterest Redesign - UX concept 레이아웃 정의_

이렇게 정의된 **Pinterest Redesign - UX concept** 페이지는 지금 구현하지 않고, 당장은 구조가 더 간단하고 레이아웃 구조를 구현하는 것에 적합한 **Google NotebookLM** 의 레이아웃을 먼저 구현하였습니다.  

![image](notebook-lm-1.png)
_Google NotebookLM 원본 페이지_

**NotebookLM** 의 경우 레이아웃의 대부분이 단순하여, 행과 열의 개념만으로도 어렵지 않게 구현할 수 있었습니다.  

![image](layout-3.png)
_순수 HTML/CSS 만을 사용하여 구현한 'Google NotebookLM' 의 레이아웃 구조_

말그대로 페이지 카피 구현이 아닌, 레이아웃의 구조만을 직접 HTML/CSs 로 구현하는 것에 집중하여 아이콘, 색상, 기능 등에 초점을 맞추지 않았습니다. 기존 페이지의 레이아웃을 유사하게 구현하였다는 것에 의의를 둘 수 있었습니다.

해당 소스 코드는 개인 [Github](https://github.com/DevGisoun/NotebookLM-HTML.git) 에 업로드하였습니다.

---

## React 기반 페이지 카피 구현

위에서 **Pinterest Redesign - UX concept** 페이지의 대략적인 레이아웃 구조를 파악하였고, 다른 페이지의 레이아웃 구조를 직접 구현해 보기까지 하였으니 이제는 추후 강의에서 다룰 **`React`**를 사용하여 **Pinterest Redesign - UX concept** 페이지를 카피해 구현해 보았습니다.  

![image](pinterest-2.png)
_직접 카피한 'Pinterest Redesign - UX concept' 페이지_

**`Button`**, **`Sidebar`** 같은 대부분의 재사용 가능한 컴포넌트 UI 는 강사님께서 적극 추천해주신 [Shadcn UI](https://ui.shadcn.com/)를 사용하였으며, Pinterest 특유의 이미지 배치 방식인 **Masonry 레이아웃** 구현을 위해 [@egjs/infinitegrid](https://github.com/naver/egjs-infinitegrid.git) 컴포넌트를 사용하였습니다. 또한, 강의에서 사용했던 기존 CSS가 아닌, **`Tailwind CSS`** 를 사용함으로써 UI의 일관성을 유지한 채 구현할 수 있었습니다. 물론 이번에도 페이지의 외형만을 최대한 카피하는 것에 목적을 두었기에 기능은 구현되어 있지는 않으며, 기존 페이지와 100% 동일하지는 않습니다.

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
