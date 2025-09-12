---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 11주차 후기"
description: >-
  desc
author: gisoun
date: 2025-09-12 17:15:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, python, numpy]
pin: false
media_subpath: '/assets/posts/20250912'
published: false
---

> 2025\. 9\. 8\. ~ 2025\. 9\. 12\.

---

11주차에는 파이썬 코드를 더욱 간결하고 효율적으로 작성할 수 있게 해주는 강력한 기능인 **리스트 컴프리헨션(List Comprehension)**과 **람다(Lambda) 함수**에 대해 학습했습니다. 전통적인 **`for`** 반복문이나 **`def`**를 사용한 함수 정의 방식보다 **짧게 작성하고 빠르게 동작**하는 코드를 작성할 수 있어 매우 유용한 시간이었습니다.

---

## 리스트 컴프리헨션 (List Comprehension)

### 리스트 컴프리헨션

기존의 반복문을 한 줄로 압축하여 새로운 리스트를 생성하는 파이썬의 독특하고 강력한 문법입니다. 단순히 코드를 짧게 만드는 것을 넘어, 가독성을 높이고 실행 속도도 더 빠른 경우가 많습니다.

### 예제 1 - 1부터 50까지 숫자 중 3의 배수만 리스트로 만들기

- **`전통적인 방법`**

   ```py
   multiples_of_3 = []
   for i in range(1, 51):
       if i % 3 == 0:
           multiples_of_3.append(i)
   print(multiples_of_3)
   ```

- **`리스트 컴프리헨션 활용`**

   ```py
   multiples_of_3 = [i for i in range(1, 51) if i % 3 == 0]
   print(multiples_of_3)
   ```

   리스트 컴프리헨션을 활용하여 **`for`** 루프와 **`if`** 조건문이 한 줄에 자연스럽게 녹아들어 훨씬 직관적인 코드가 완성되었습니다.

- **`성능 비교`**
   
   글 초반에 언급했듯 일반적으로 리스트 컴프리헨션이 전통적인 **`for`** 루프보다 더 빠르게 동작합니다. 파이썬의 **`time`** 모듈을 사용하여 간단한 성능 테스트를 진행할 수 있습니다.

   > 성능 차이를 명확히 보기 위해 반복 횟수(**`limit`**)를 늘려서 테스트했습니다.
   {: .prompt-info }

   ```py
   import time
   
   limit = 1000000
   
   # 전통적인 방법 성능 측정
   start_time = time.time()
   multiples_list = []
   for i in range(1, limit + 1):
       if i % 3 == 0:
           multiples_list.append(i)
   end_time = time.time()
   print(f"전통적인 방법 실행 시간: {end_time - start_time:.6f}초")
   
   # 리스트 컴프리헨션 성능 측정
   start_time = time.time()
   multiples_comp = [i for i in range(1, limit + 1) if i % 3 == 0]
   end_time = time.time()
   print(f"리스트 컴프리헨션 실행 시간: {end_time - start_time:.6f}초")   
   ```

   **실행 결과**

   ```terminal
   전통적인 방법 실행 시간: 0.173103초
   리스트 컴프리헨션 실행 시간: 0.075839초
   ```

   위 결과처럼, 리스트 컴프리헨션이 내부적으로 최적화되어 있어 더 나은 성능을 보여주는 것을 확인할 수 있습니다.

### 1부터 20까지 숫자를 홀수는 제곱, 짝수는 세제곱으로 변환

리스트 컴프리헨션은 **`if...else`** 와 같은 **조건부 표현식(삼항 연산자)**과 결합하여 더욱 복잡한 로직을 처리할 수 있습니다.

```py
power_numbers = [i**2 if i % 2 != 0 else i**3 for i in range(1, 21)]
print(power_numbers)
```

이처럼 **`for`** 루프 앞에 조건부 표현식을 위치시켜 각 요소에 대해 서로 다른 연산을 적용할 수 있습니다.

---

## 람다(Lambda) 함수와 고차 함수

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
