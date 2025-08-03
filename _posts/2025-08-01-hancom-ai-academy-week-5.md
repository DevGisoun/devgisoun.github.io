---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 5주차 후기"
description: >-
  Typescript 기반 React 를 활용한 팀 프로젝트 마무리 단계.
author: gisoun
date: 2025-08-01 17:05:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, html, css, javascript, js]
pin: false
media_subpath: '/assets/posts/20250801'
published: true
---

> 2025\. 7\. 28\. ~ 2025\. 8\. 1\.

---

## 팀 프로젝트

[지난 주차](https://devgisoun.github.io/posts/hancom-ai-academy-week-4/)에 이어서 이번 주차에도 팀 프로젝트를 진행하였습니다. 이번 주차에는 기반이 어느정도 갖춰진 설문 폼에 **디테일을 더하여 프로젝트를 다듬거나**, **추가적으로 필요한 기능을 구현**하는 식으로 각자 임무를 맡았습니다.

---

## Github Projects & Issues & Pull Requests

지난 주차부터 Github의 **Projects**, **Issues**, **Pull Requests** 를 활용하여 팀 프로젝트의 워크플로우를 구성하였는데, 사용하면 할 수록 정말 유용하고 협업에 대한 경험이 크게 향상되는 것을 체감할 수 있었습니다.  

![image](github-projects-1.png)
_Github Projects 페이지에서 등록한 각자 맡은 역할에 대한 Issues_

팀원들 각자의 역할을 쉽고 빠르게 **`Issues`** 에 작성하고 이를 진행 상황에 맞는 컬럼에 블록처럼 배치하여 관리하니 **프로젝트의 전체적인 척도 파악**과 **`Comments`** 를 통한 **피드백 소통**이 원활하게 이루어질 수 있었습니다.  

![image](github-projects-2.png)
_각 팀원별 Git Branch 및 Pull Request 목록_

또한, 팀원별 **Branch** 를 분리함으로써 다른 팀원의 작업에 영향을 주지 않게끔 하여 **프로젝트의 안정성**을 챙기고, **Pull Request** 를 적극 활용하여 팀원 간의 원활한 소통 및 코드 리뷰를 통해 **프로젝트의 품질을 향상**할 수 있었습니다.

---
## any 대신 interface로 타입 정의

프로젝트 규모가 커지고 기능이 복잡해질수록, 다루는 데이터의 구조를 명확하게 정의하는 것이 매우 중요해집니다. 지금까지는 단순히 개발 속도를 위해 Supabase에서 받아온 데이터에 **`any`** 타입을 사용했지만, 사실 이는 TypeScript의 가장 큰 장점인 **타입 안정성**을 포기하는 것이기에 종종 신경 쓰였습니다.

개발자 입장에서 **`any`** 타입은 당장은 편할지 몰라도, 예상치 못한 버그를 만들고 팀원들 간 코드를 이해하기 어렵게 만드는 원인이 될 수 있습니다. 때문에 규모가 더 커지기 전에 **`interface`** 를 사용해 데이터 객체의 형태를 명확히 정의하고 안전하게 만들어 보았습니다.

### 데이터 모델을 위한 interface 정의

저의 경우, Supabase 데이터베이스 테이블 구조에 맞춰 **`interface`**를 생성하였습니다.

**[/src/types/form.ts]**
```
// 'forms' 테이블의 구조를 interface 로 정의.
export interface FormData {
  id: string;
  user_id: string;
  title: string;
  description: string;
  
  // ...
  
  start_time?: Date | null; // 설문 시작일 (선택적)
  end_time?: Date | null;   // 설문 종료일 (선택적)
}
```  

**[/src/types/question.ts]**
```ts
import type { Answer } from "./answer";
import type { Option } from "./option";

// 'questions' 테이블과 그와 관련된 데이터 구조를 interface 로 정의.
export interface QuestionData {
  id: string;
  form_id: string;
  text: string;
  type: string;
  
  // ...
  
  // Partial<T> 유틸리티 타입을 사용해 Option, Answer 의 모든 필드가 필수가 아님을 명시.
  options?: Partial<Option>[];
  answers?: Partial<Answer>[];
}
```  

위와 같이 **`FormData (forms 테이블)`**, **`QuestionData (questions 테이블)`**, **`Option (options 테이블)`**, **`Answer (answers 테이블)`** 등 각 데이터의 구조를 **`interface`**로 정의하면, 이 데이터들이 애플리케이션 내에서 어떤 형태를 가져야 하는지 명확하게 알 수 있습니다.

### 실제 타입 적용 예시

이렇게 정의한 **`interface`**를 실제 코드에 적용해 **`any`** 로 부터 교체 작업을 하였습니다.  

#### **`useState`**의 제네릭 타입(**`<>`**) 명시

먼저, 컴포넌트가 다루는 **상태(State)**의 타입을 명확히 지정했습니다.

- **`기존 코드 `** 
   ```
   const [formElements, setFormElements] = useState<any[]>([]);
   ```
- **`수정 코드`**  
   ```
   import type { QuestionData } from "@/types/question";

   const [formElements, setFormElements] = useState<QuestionData[]>([]);
   ```

이제 **`formElements`** 배열은 **`QuestionData`** 객체만 포함할 수 있으며, 배열의 요소를 다룰 때 **`id`**, **`text`**, **`options`** 등의 속성을 자동 완성으로 편리하고 안전하게 사용할 수 있습니다.

#### 컴포넌트 **`props`** 타입 지정

컴포넌트에 전달되는 데이터의 타입을 명시하여, 잘못된 데이터가 전달되는 것을 방지하였습니다.

- **`기존 코드 `**
   ```
   interface QuestionProps {
     question: any;
     // ...
   }
   ```

- **`수정 코드`**
   ```
   interface QuestionProps {
     question: QuestionData;
     // ...
   }
   ```

이제 **`Question`** 컴포넌트 안에서 **`props.question`** 을 사용할 때, TypeScript는 이 객체가 어떤 속성들을 가지고 있는지 정확히 알고 있어 개발 중 실수를 방지해 줍니다.

#### **`타입 단언(Type Assertion)`**을 통한 구체화

때로는 부모 컴포넌트로부터 받은 데이터의 타입이 다소 포괄적일 수 있습니다. 이 경우, 해당 데이터가 특정 구조를 가졌다고 **`타입 단언`**을 통해 TypeScript에게 알려줄 수 있습니다.

- **`기존 코드 `** 
   ```
   const [options, setOptions] = useState<any[]>(question.options || []);
   ```

- **`수정 코드`**  
   ```
   import type { Option } from "@/types/option";

   // question.options가 Option 배열이라고 단언  
   const [options, setOptions] = useState<Partial<Option>[]> ((question.options as Partial<Option>[]) || []);
   ```

---

## 미니 프로젝트를 마치며

처음에는 **`NavLink`** 의 활성화 스타일을 동적으로 바꾸는 작은 기능부터 시작해서, 이내 복잡한 상태 로직을 가진 **`DateConfigRow`** 나 **`QuestionTitle`** 같은 컴포넌트를 직접 설계하고, 페이지 전체의 상태를 관리하며 Supabase 데이터베이스와 연동하는 경험은 컴포넌트 설계와 데이터 흐름에 대한 이해를 한층 깊게 만들어 주었습니다. 특히, 처음엔 **`any`**로 가득했던 코드를 명확한 **`interface`**로 리팩토링하며 타입 안정성이 주는 견고함과 개발 편의성을 온몸으로 체감할 수 있었습니다.  

무엇보다 값진 경험은 팀원들과의 협업이었습니다. 서로의 코드를 간단하게 리뷰하고, 더 나은 컴포넌트 구조, DB 설계에 대해 함께 고민하며 맞춰나가는 과정 속에서 혼자서는 결코 얻지 못했을 시야를 얻었습니다. 저와 다른 팀원이 만든 UI 컴포넌트가 매끄럽게 연결될 때, 그리고 막혔던 문제를 소통을 통해 해결해냈을 때의 희열은 이 프로젝트를 끝까지 이끌어준 가장 큰 원동력이었습니다. 결과물도 물론 중요하지만, 그 과정에서 얻은 **기술적 성장**과 **협업의 경험**이야말로 이번 미니 프로젝트의 가장 큰 가치였습니다. 이 경험을 발판 삼아, 앞으로 마주할 또 다른 도전에도 자신 있게 나아갈 수 있을 것 같아 매우 설렙니다😊😊

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
