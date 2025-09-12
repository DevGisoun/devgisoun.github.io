---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 11주차 후기"
description: >-
   Python 의 핵심 기능인 리스트 컴프리헨션과 람다(Lambda) 함수의 개념 학습. 다양한 예제를 통해 예시 데이터 처리, 필터링, 매핑, 그룹핑 등 실용적인 활용법을 익힌 과정 정리.
author: gisoun
date: 2025-09-13 00:33:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, python, numpy]
pin: false
media_subpath: '/assets/posts/20250912'
published: true
---

> 2025\. 9\. 8\. ~ 2025\. 9\. 12\.

---

11주차에는 Python 코드를 한 차원 더 간결하고 효율적으로 만들어주는 **리스트 컴프리헨션(List Comprehension)**과 **람다(Lambda) 함수**에 대해 집중적으로 다룹니다. 기본적인 문법부터 시작하여, 실제 데이터 처리와 유사한 복잡한 시나리오의 예제들을 통해 이러한 기능들이 어떻게 코드의 가독성과 성능을 향상시키는지 구체적인 예제와 함께 학습하였습니다.

---

## 리스트 컴프리헨션 (List Comprehension)

기존의 반복문을 한 줄로 압축하여 새로운 리스트를 생성하는 Python 의 독특하고 강력한 문법입니다. 단순히 코드를 짧게 만드는 것을 넘어, 가독성을 높이고 일반적으로 실행 속도도 더 빠릅니다.

### 전통적인 for 문 과 성능 비교

먼저 **`if`** 조건문이 포함된 가장 기본적인 리스트 컴프리헨션의 문법을 익히고, 전통적인 **`for`** 문과 비교했을 때 실제 성능 차이가 얼마나 나는지 확인해 보았습니다.

- **`리스트 컴프리헨션 활용`**

   ```py
   # 예제 - 1부터 50까지 숫자 중 3의 배수만 리스트로 만들기

   multiples_of_3 = [i for i in range(1, 51) if i % 3 == 0]
   print(multiples_of_3)
   ```

   **실행 결과**

   ```terminal
   [3, 6, 9, 12, 15, 18, 21, 24, 27, 30, 33, 36, 39, 42, 45, 48]
   ```

   리스트 컴프리헨션을 활용하여 **`for`** 루프와 **`if`** 조건문이 한 줄에 자연스럽게 녹아들어 훨씬 직관적인 코드가 완성되었습니다.

- **`성능 비교`**
   
   글 초반에 언급했듯 일반적으로 리스트 컴프리헨션이 전통적인 **`for`** 문보다 더 빠르게 동작합니다. Python 의 **`time`** 모듈을 사용하여 간단한 성능 테스트를 진행해 보겠습니다.

   > 성능 차이를 명확히 보기 위해 반복 횟수(**`limit`**)를 늘려서 테스트했습니다.
   {: .prompt-info }

   ```py
   # 전통적인 for 문과 리스트 컴프리헨션의 성능 비교

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

### 조건부 표현식 활용

리스트 컴프리헨션은 **`if...else`** 와 같은 **조건부 표현식(삼항 연산자)**과 결합하여 더욱 복잡한 로직을 처리할 수 있습니다. 이를 통해 조건에 따라 각기 다른 연산을 적용하는 방법을 연습해 보았습니다.

```py
# 예제 - 1부터 20까지 숫자를 홀수는 제곱, 짝수는 세제곱으로 변환

# [표현식1 if 조건 else 표현식2 for 변수 in 반복객체]
power_numbers = [i**2 if i % 2 != 0 else i**3 for i in range(1, 21)]
print(power_numbers)
```

이처럼 **`for`** 문 앞에 조건부 표현식을 사용하여 각 요소에 대해 서로 다른 연산을 적용할 수 있는 것을 확인하였습니다.

### 중첩 데이터 처리

이번에는 중첩된 딕셔너리 데이터를 다루면서, 이중 **`for`** 문을 사용해 데이터를 단일 리스트로 펼치는 평탄화(Flattening) 작업과, 딕셔너리 및 집합(Set) 컴프리헨션을 활용한 데이터 집계 방법을 익혔습니다.

```py
# 1. 모든 반의 점수를 하나의 리스트로 만들기 (평탄화)
# 2. 각 반의 평균 점수를 담은 딕셔너리 만들기
# 3. 90점 이상인 모든 점수를 중복 없이 담은 집합(set) 만들기

# 학급 데이터
classes = {
    'A반': [85, 92, 78, 96, 89],
    'B반': [88, 75, 91, 84, 87],
    'C반': [79, 93, 86, 90, 82]
}

# 1. 모든 점수를 평탄화한 리스트
all_scores = [score for scores in classes.values() for score in scores]
print("모든 점수:", all_scores)

# 2. 각 반의 평균 점수 딕셔너리 (딕셔너리 컴프리헨션)
class_averages = {class_name: sum(scores) / len(scores) for class_name, scores in classes.items()}
print("반별 평균:", class_averages)

# 3. 90점 이상인 점수 집합 (집합 컴프리헨션)
high_scores_set = {score for scores in classes.values() for score in scores if score >= 90}
print("90점 이상 점수:", high_scores_set)
```

### CSV 형태의 데이터 처리 시뮬레이션

실제 데이터 분석 작업에서는 파일이나 API로부터 **CSV(Comma-Separated Values)** 형태의 데이터를 받아 처리하는 경우가 많습니다. 이번 예제는 실제 파일을 사용하는 대신, 문자열로 된 예시 CSV 데이터를 Python 의 **`csv`** 모듈과 **`io.StringIO`** 를 이용해 파일처럼 다루는 방법을 시뮬레이션합니다. 이를 통해 리스트 컴프리헨션이 실제 데이터 처리 예제에서 어떻게 활용될 수 있는지 알아보았습니다.

```py
# 1. 각 도시별 평균 연봉 계산
# 2. 나이대별로 그룹핑하여 이름 목록 만들기
# 3. 이름의 첫 글자가 같은 사람들끼리 그룹핑하기

import csv
from io import StringIO

# 예시 CSV 데이터
csv_data = """name,age,city,salary
Alice,25,Seoul,50000
Bob,30,Busan,55000
Charlie,35,Seoul,60000
Diana,28,Daegu,52000
Eve,32,Seoul,58000"""

# StringIO 를 사용해서 메모리에서 CSV 처리
# 실제 파일이 아닌 문자열을 파일처럼 다룰 수 있게 해줍니다.
csv_file = StringIO(csv_data)

# DictReader 는 각 행을 딕셔너리로 읽어옵니다.
csv_reader = csv.DictReader(csv_file)

# 리스트 컴프리헨션으로 모든 CSV 데이터를 딕셔너리 리스트로 변환
data = [row for row in csv_reader]

# 1. 각 도시별 평균 연봉 계산 (딕셔너리 컴프리헨션 사용)
cities = {person['city'] for person in data} # 중복 없는 도시 집합 생성
city_avg_salary = {
    city: sum(int(p['salary']) for p in data if p['city'] == city) / len([p for p in data if p['city'] == city])
    for city in cities
}
print("도시별 평균 연봉:", city_avg_salary)


# 2. 나이대별 그룹핑 (딕셔너리의 값이 리스트)
age_groups = {
    age_group: [p['name'] for p in data if (int(p['age']) // 10) * 10 == age_group]
    for age_group in { (int(p['age']) // 10) * 10 for p in data }
}
print("나이대별 그룹핑:", age_groups)

# 3. 이름의 첫 글자가 같은 사람들끼리 그룹핑
initials = {p['name'][0] for p in data}
name_groups = {
    initial: [p['name'] for p in data if p['name'].startswith(initial)]
    for initial in initials
}
print("이름 첫 글자별 그룹핑:", name_groups)
```

**실행 결과**  

```terminal
도시별 평균 연봉: {'Daegu': 52000.0, 'Seoul': 56000.0, 'Busan': 55000.0}
나이대별 그룹핑: {20: ['Alice', 'Diana'], 30: ['Bob', 'Charlie', 'Eve']}
이름 첫 글자별 그룹핑: {'A': ['Alice'], 'E': ['Eve'], 'D': ['Diana'], 'C': ['Charlie'], 'B': ['Bob']}
```

---

## 람다(Lambda) 함수와 고차 함수

람다 함수는 이름이 없는 **'익명 함수'**로, 간단한 기능을 하는 함수를 한 줄로 정의할 때 매우 유용합니다. 주로 **`map`**, **`filter`**, **`sorted`** 와 같은 **고차 함수(함수를 인자로 받거나 함수를 반환하는 함수)**와 함께 사용될 때 아주 유용합니다.

### map 과 filter 활용

**`map`** 과 **`filter`** 는 Python 에서 함수형 프로그래밍의 기본이 되는 고차 함수입니다. 람다 함수와 함께 사용하면 리스트의 각 요소를 변환하거나 특정 조건에 맞는 요소만 걸러내는 작업을 매우 간결하게 처리할 수 있습니다.

- **`map(함수, 반복객체)`**: 각 요소에 함수를 적용하여 새로운 **`map`** 객체를 반환합니다.
- **`filter(함수, 반복객체)`**: 함수 결과가 **`True`** 인 요소만 걸러내어 새로운 **`filter`** 객체를 반환합니다.

```py
prices = [100, 250, 75, 300, 150, 400, 50]

# 1. 모든 가격에 10% 할인을 적용한 리스트 (map 사용)
discounted_prices = list(map(lambda p: p * 0.9, prices))
print("할인 가격:", discounted_prices)

# 2. 200원 이상인 가격만 필터링 (filter 사용)
expensive_items = list(filter(lambda p: p >= 200, prices))
print("비싼 상품:", expensive_items)

# 3. 100원 이상인 가격에만 세금 10%를 추가한 리스트 (filter + map 조합)
taxed_prices = list(map(lambda p: p * 1.1, filter(lambda p: p >= 100, prices)))
print("세금 포함 가격:", taxed_prices)
```

**실행 결과**

```terminal
할인 가격: [90.0, 225.0, 67.5, 270.0, 135.0, 360.0, 45.0]
비싼 상품: [250, 300, 400]
세금 포함 가격: [90.0, 225.0, 270.0, 135.0, 360.0]
```

### sorted 와 reduce 활용

이번에는 좀 더 복잡한 자료구조를 다루며 **`sorted`** 함수의 **`key`** 인자에 람다를 활용하여 원하는 기준으로 정렬하고, **`reduce`** 함수로 리스트의 모든 요소를 누적 계산하는 방법을 익혔습니다.

- **`sorted(반복객체, key=함수)`**: 특정 키(**`key`**)를 기준으로 정렬합니다.
- **`reduce(함수, 반복객체)`**: 모든 요소를 누적적으로 계산하여 단일 값을 반환합니다. (**`functools`** 모듈 **`import`** 필요)

```py
from functools import reduce

students = [
    {'name': 'Alice', 'score': 85, 'grade': 'B'},
    {'name': 'Bob', 'score': 92, 'grade': 'A'},
    {'name': 'Charlie', 'score': 78, 'grade': 'C'},
    {'name': 'Diana', 'score': 96, 'grade': 'A'},
    {'name': 'Eve', 'score': 89, 'grade': 'B'}
]

# 1. 점수순 정렬
sorted_students = sorted(students, key=lambda s: s['score'], reverse=True)
print("점수순 정렬:", sorted_students)

# 2. A등급 학생 이름 추출
a_grade_names = list(map(lambda s: s['name'], filter(lambda s: s['grade'] == 'A', students)))
print("A등급 학생:", a_grade_names)

# 3. 평균 점수 계산
total_score = reduce(lambda acc, s: acc + s['score'], students, 0)
average_score = total_score / len(students)
print("평균 점수:", average_score)
```

**실행 결과**

```terminal
점수순 정렬: [{'name': 'Diana', 'score': 96, 'grade': 'A'}, {'name': 'Bob', 'score': 92, 'grade': 'A'}, {'name': 'Eve', 'score': 89, 'grade': 'B'}, {'name': 'Alice', 'score': 85, 'grade': 'B'}, {'name': 'Charlie', 'score': 78, 'grade': 'C'}]
A등급 학생: ['Bob', 'Diana']
평균 점수: 88.0
```

---

## 마무리

11주차에는 Python 의 **리스트 컴프리헨션**과 **람다 함수**를 집중적으로 학습했습니다. 다른 프로그래밍 언어에서는 찾아보기 힘든 난해한 문법이었지만, 다양한 연습 문제를 통해 점차 그 간결함과 효율성에 익숙해질 수 있었습니다. 특히 복잡한 **`for`** 루프와 **`if`** 조건문을 단 한 줄로 표현하거나, **`map`**, **`filter`** 와 같은 **고차 함수**와 결합하여 데이터를 유연하게 다루는 과정으로 함수형 프로그래밍을 학습하는 것에 큰 흥미를 느꼈습니다. 앞으로 데이터를 처리하거나 알고리즘을 구현할 때, 적어도 Python 문법을 몰라서 해매는 일 없이 코드를 작성하는 데 큰 도움이 될 것이라 기대하며 글 마치겠습니다. 감사합니다!

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
