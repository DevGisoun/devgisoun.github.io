---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 3주차 후기"
description: >-
  Typescript 기반 React 내에서 Supabase 를 활용한 이메일, 패스워드 회원가입 및 로그인 기능 구현.
author: gisoun
date: 2025-07-11 22:05:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, html, css, javascript, js]
pin: false
media_subpath: '/assets/posts/20250718'
published: true
---

> 2025\. 7\. 11\. ~ 2025\. 7\. 18\.

---

이번 주에는 **TypeScript 기반의 React 환경에서 Supabase를 활용해 이메일, 패스워드 기반의 회원가입 및 로그인 기능을 구현**하는 방법을 배웠습니다.

## Supabase 프로젝트 설정하기

먼저 Supabase 프로젝트를 생성하였습니다.

1. [Supabase 공식 홈페이지](https://supabase.com)에 접속하여 로그인 후, 메인 페이지에 있는 **'Start your project'**를 선택합니다.
   
   ![image](supabase-1.png)
   _Supabase 메인 페이지_

2. 프로젝트 이름, 데이터베이스 비밀번호, 리전(Region)을 선택한 후, **'Create new project'** 버튼을 클릭하면 몇 분 내로 프로젝트가 생성됩니다.
   
   ![image](supabase-2.png)
   _Supabase 새 프로젝트 생성_

3. 생성한 프로젝트 대시보드로 이동한 뒤, 상단의 **Connect** 버튼을 클릭합니다.
   
   ![image](supabase-3.png)
   _Supabase 대시보드의 'Connect' 버튼_

4. **'App Frameworks'** 탭을 선택한 뒤, **'Framework'** 메뉴에서 **React** 를, **Using** 메뉴에서 **Vite** 를 선택합니다.
   
   ![image](supabase-4.png)
   _'App Frameworks' 탭_

5. 이곳에서 **`Vite`** 로 생성한 React 앱과 연동할 때 필요한 **`Project URL`**과 **`Anon Key`** 를 복사해 둡니다.

   ![image](supabase-5.png)
   _Project URL 과 Anon Key_

---

## React 프로젝트에 Supabase 연동하기

이제 기존 수업에 사용한 React 프로젝트에 **`Supabase`**를 설치하고 연동해 보겠습니다.

1. 프로젝트 터미널에서 아래 명령어를 실행하여 **`@supabase/supabase-js`** 라이브러리를 설치합니다.

   ```bash
   pnpm i @supabase/supabase-js
   ```

2. React 프로젝트의 최상위 경로에 **`.env.local`** 파일을 생성하여 이전에 복사한 **`Project URL`**과 **`Anon Key`** 를 입력합니다.  
  
   ![image](supabase-6.png)
   _'App Frameworks' 탭_

3. **`/src`** 디렉토리 아래에 **`/utils`** 폴더를 만들고 **`supabase.ts`** 파일을 생성합니다. 그리고 아래 코드를 복사하여 입력합니다.  

   ```typescript
   // /src/utils/supabase.ts
   import { createClient } from '@supabase/supabase-js';
 
   const supabaseUrl = import.meta.env.VITE_SUPABASE_URL;
   const supabaseKey = import.meta.env.VITE_SUPABASE_ANON_KEY;
 
   const supabase = createClient(supabaseUrl, supabaseKey);
 
   export default supabase;
   ```

이것으로 **`Supabase`** 클라이언트를 초기화하여 React 프로젝트에 연동하였습니다.

---

## 회원가입 기능 구현하기

1. 우선 아래와 같이 이메일, 패스워드 기반 회원가입 Form 을 제작하였습니다.

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
