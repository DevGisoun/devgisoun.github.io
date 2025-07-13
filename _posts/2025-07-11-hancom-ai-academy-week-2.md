---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 2주차 후기"
description: >-
  React의 기초 개념과 Hooks 이해를 위한 실습.
author: gisoun
date: 2025-07-11 22:05:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, html, css, javascript, js]
pin: false
media_subpath: '/assets/posts/20250711'
published: true
---

> 2025\. 7\. 7\. ~ 2025\. 7\. 11\.

---

## React는 SPA

**`SPA`**는 **S**ingle **P**age **A**pplication의 약자로, **단일 페이지로 구성된 애플리케이션**을 의미합니다. 기존의 웹사이트처럼 여러 HTML 을 서버에서 받아오는 것이 아니라, 최초 한 번만 웹 애플리케이션에 필요한 모든 리소스(HTML, CSS, JavaScript)가 담긴 단일 페이지**`(index.html)`**를 불러오고 이후에는 데이터만 동적으로 변경하여 보여주는 방식입니다.

React는 이러한 SPA를 구축하는 데 매우 효과적인 Javascript 라이브러리입니다. 컴포넌트 기반 구조를 통해 UI를 독립적인 부분으로 나누어 개발하고, 가상 DOM(Virtual DOM)을 사용하여 변경된 부분만 효율적으로 업데이트함으로써 사용자에게 마치 데스크톱 앱을 사용하는 것과 같은 부드럽고 빠른 경험을 제공합니다.

---

## Component 란?

컴포넌트(Component)는 UI를 독립적이고 재사용 가능한 단위로 나눈 것입니다. 미리 만들어 둔 여러 종류의 컴포넌트를 마치 레고 블록처럼 조립하여 하나의 완성된 결과물을 만드는 것과 같습니다.

예를 들어, 웹사이트의 Header, Footer 및 지난 주차에서 **Pinterest Redesign - UX concept** 페이지 카피를 위해 사용한 **Shadcn UI**의 Sidebar, Button 등 모든 요소를 각각의 컴포넌트로 만들어 사용할 수 있습니다. 이렇게 잘게 쪼개진 컴포넌트들은 서로 조합하여 더 복잡한 컴포넌트나 페이지를 구성하게 됩니다.

### Component 사용 시 장점

- **`상태 관리`**: 각 컴포넌트는 자신만의 **상태(state)**를 가질 수 있습니다. 예를 들어, 토글 버튼 컴포넌트는 '켜짐'(true) 과 '꺼짐'(false) 이라는 상태를 스스로 관리할 수 있습니다. 이처럼 컴포넌트 단위로 상태를 관리하면 데이터의 흐름을 파악하기 쉽고, 애플리케이션의 복잡도가 증가하더라도 유지보수가 용이해집니다.
- **`확장성`**: 새로운 기능이 필요하다면 새로운 컴포넌트를 만들거나 기존 컴포넌트를 조합하여 쉽게 추가할 수 있습니다. 이는 코드의 재사용성을 높여 개발 생산성을 크게 향상시키며 애플리케이션의 기능을 확장하기에 매우 편리해집니다. 

---

## Props 란?

**Props(Properties)**는 **부모 컴포넌트 -> 자식 컴포넌트**로 데이터를 전달할 때 사용하는 객체로, 일반적인 함수의 **인자(argument)**와 매우 유사한 역할을 한다고 생각하면 이해하기 쉽습니다. 컴포넌트 간의 데이터 통신을 위한 가장 기본적인 방법이며, 자식 컴포넌트는 이 props를 통해 부모로부터 받은 데이터를 화면에 렌더링하거나 다른 용도로 사용할 수 있습니다.

### Props의 두 가지 규칙

- **`단방향 데이터 흐름(one-way data flow)`**: 자식 컴포넌트는 부모로부터 받은 props를 역으로 전달할 수도 없습니다. 항상 **부모 -> 자식**으로만 흐릅니다. 이는 데이터의 흐름을 예측 가능하게 만들어 애플리케이션의 안정성을 높여줍니다. 만약 자식 컴포넌트에서 발생한 이벤트를 부모에게 알려야 한다면, 부모로부터 콜백 함수를 props로 전달받아 실행하는 방식을 사용합니다.
- **`읽기 전용(readonly)`**: 자식 컴포넌트는 전달받은 props를 절대로 직접 수정해서는 안 됩니다. Props는 오직 읽기만 가능한 데이터입니다.

---

## Hook 이란?

**Hook**은 React의 상태 관리 및 생명주기(Lifecycle) 기능을 사용할 수 있게 해주는 특별한 함수입니다. Hook을 통해 더욱 간결하고 직관적인 코드로 함수형 컴포넌트의 다양한 기능을 구현할 수 있습니다.

### useState

**`useState`**는 함수형 컴포넌트에서 **상태(state)**를 관리할 수 있게 해주는 가장 기본적인 Hook입니다. useState를 호출하면 튜플을 반환하는데, **첫 번째 요소는 현재 상태 값**이고 **두 번째 요소는 그 상태 값을 업데이트하는 함수**입니다. 또한 **`useState`** 함수의 인자로 상태의 기본값을 설정할 수 있습니다.

```
// 'name' 상태 변수와 그 값을 변경할 setName 함수를 선언.
// 초기값: '기순'.
const [name, setName] = useState<string>('기순');

// 'nickname' 상태 변수와 그 값을 변경할 setNickname 함수를 선언.
// 초기값: 'DevGisoun'입니다.
const [nickname, setNickname] = useState<string>('DevGisoun');

// 이름 <input />의 변경 이벤트를 처리하는 핸들러.
const onChangeName = (e: React.ChangeEvent<HTMLInputElement>) =>
    // setName 함수를 호출하여 <input />의 현재 값으로 'name' 상태를 업데이트.
    setName(e.target.value);

// 닉네임 <input />의 변경 이벤트를 처리하는 핸들러.
const onChangeNickame = (e: React.ChangeEvent<HTMLInputElement>) =>
    // setNickname 함수를 호출하여 <input />의 현재 값으로 'nickname' 상태를 업데이트.
    setNickname(e.target.value);

return (
    <>
        <div>
            <div>
                {/* <input />의 value를 'name' 상태에 바인딩하며, */}
                {/* <input />의 내용이 변경될 때마다 'onChangeName' 함수 호출. */}
                <input type="text" value={name} onChange={onChangeName} />
                
                {/* <input />의 value를 'nickname' 상태에 바인딩하며, */}
                {/* <input />의 내용이 변경될 때마다 'onChangeNickname' 함수 호출. */}
                <input type="text" value={nickname} onChange={onChangeNickame}
                />
            </div>

            {/* 'name'과 'nickname' 의 상태가 변경되면 자동으로 업데이트되어 화면에 표시. */}
            <div><b>이름: {name}</b></div>
            <div><b>닉네임: {nickname}</b></div>
        </div>
    </>
);
```

![image](useState-1.png)
_각각 '기순', 'DevGisoun'으로 초기화된 'input'과 텍스트_

![image](useState-2.png)
_'input' 에 입력된 'name' 상태값을 변경하자 동시에 변경된 텍스트_

### useEffect

**`useEffect`**는 컴포넌트가 렌더링될 때마다 특정 작업을 수행하도록 설정할 수 있는 Hook입니다. 데이터 가져오기(fetching), DOM 조작 등 다양한 **부수 효과(Side Effect)**를 처리하는 데 사용됩니다.

**`useEffect`**는 **첫 번째 인자로 실행할 함수**를 받고, **두 번째 인자로 의존성 배열(Dependency Array)**을 받습니다. 이 의존성 배열에 포함된 값 중 하나라도 변경될 때마다 첫 번째 인자로 전달한 함수가 실행됩니다. 만약 빈 배열 []을 전달하면, 컴포넌트가 처음 마운트될 때 한 번만 실행됩니다.

```
const [name, setName] = useState<string>('');
const [nickname, setNickname] = useState<string>('');

// 의존성 배열이 없으므로, 컴포넌트가 렌더링될 때마다 이 useEffect 실행.
useEffect(() => {
    console.log('컴포넌트가 렌더링/리렌더링 될 때마다 특정 작업 수행.');
    console.log({
        name,
        nickname,
    });
});

// 의존성 배열이 빈 배열이므로, 컴포넌트가 처음 화면에 나타날 때, 즉 마운트 될 때만 이 useEffect 실행.
useEffect(() => {
    console.log('마운트 될 때만 수행');
    console.log({
        name,
        nickname,
    });
}, []);

// 의존성 배열에 'name' 이 있으므로, 처음 마운트 될 때와 'name' 상태가 변경될 때만 이 useEffect 실행.
// 'nickname' 은 의존성 배열에 포함되어 있지 않으므로, 'nickname' 의 상태가 변경되어도 이 useEffect 실행 X.
useEffect(() => {
    console.log('name이라는 상태 값이 변경될 때만 수행');
    console.log({
        name,
        nickname,
    });
}, [name]);
```

![image](useEffect-1.png)
_'name', 'nickname' 에 대한 'input' 컴포넌트와 '보이기' 버튼 컴포넌트_

![image](useEffect-2.png)
_'보이기' 버튼 컴포넌트를 클릭하니 나타나는 텍스트 컴포넌트 및 변경된 버튼 텍스트_

### useMemo

**`useMemo`** 는 계산 비용이 큰 함수의 결과값을 메모리에 기억하게 하는 **메모이제이션(Memoization) 을 하여**, 의존성 배열의 값이 변경될 때만 해당 함수를 다시 실행하도록 하는 Hook입니다. **`useMemo`** 를 통해 불필요한 연산을 줄여 애플리케이션의 성능을 최적화할 수 있습니다.

```
// 평균값을 계산하는 함수.
const getAverage = (numbers: number[]) => {
    // 호출 시점을 확인하기 위해 console.log를 사용.
    console.log('평균값 계산 중...');

    if (numbers.length === 0) return 0;

    const sum = numbers.reduce((acc, cur) => acc + cur);
    return sum / numbers.length;
};

function Average() {
    const [list, setList] = useState<number[]>([]);
    const [number, setNumber] = useState<string>('');

    // <input /> 값이 변경될 때마다 'number' 상태 업데이트.
    // 이 함수가 호출될 때마다 컴포넌트 리렌더링.
    const onChange = (event: React.ChangeEvent<HTMLInputElement>) =>
        setNumber(event.target.value);

    // '등록' 버튼 클릭 시 'list' 배열에 새로운 숫자 추가.
    const onInsert = () => {
        const nextList: number[] = list.concat(parseInt(number));
        setList(nextList);
        setNumber('');
    };

    // useMemo를 사용하여 'list' 의 내용이 바뀔 때만 'getAverage' 함수 호출.
    // 즉, <input />의 내용만 바뀌는 리렌더링에서는 이전 계산 결과를 재사용하여 성능을 최적화.
    const avg = useMemo(() => getAverage(list), [list]);

    return (
        <>
            <div>
                <input type="text" value={number} onChange={onChange} />
                <button onClick={onInsert}>등록</button>

                <ul>
                    {list.map((value: number, index: number) => (
                        <li key={index}>{value}</li>
                    ))}
                </ul>

                <div>
                    {/* useMemo를 통해 계산된 평균값을 화면에 표시. */}
                    <b>평균값: </b> {avg}
                </div>
            </div>
        </>
    );
}

export default Average;
```

### useCallback

**`useCallback`**은 useMemo와 유사하지만, 함수의 결과값이 아닌 함수 자체를 메모이제이션하는 데 사용되는 Hook입니다. 자식 컴포넌트에 props로 함수를 전달할 때, 부모 컴포넌트가 리렌더링되어도 불필요하게 함수가 재생성되는 것을 방지하여 자식 컴포넌트의 불필요한 리렌더링을 막아줍니다.

```
const getAverage = (numbers: number[]) => {
    console.log('평균값 계산 중...');

    if (numbers.length === 0) return 0;

    const sum = numbers.reduce((acc, cur) => acc + cur);
    return sum / numbers.length;
};

function Callback() {
    const [list, setList] = useState<number[]>([]);
    const [number, setNumber] = useState<string>('');

    // useCallback을 사용하여 컴포넌트가 처음 렌더링될 때만 'onChange' 함수 생성.
    // 이후 리렌더링 시에는 기억된 함수를 재사용하여 불필요한 함수 생성을 방지.
    const onChange = useCallback(
        (event: React.ChangeEvent<HTMLInputElement>) =>
            setNumber(event.target.value),
        []
    ); // 의존성 배열이 비어있으므로, 최초 1회만 함수 생성.

    // useCallback을 사용하여 'number' 또는 'list' 상태가 변경되었을 때만 'onInsert' 함수를 새로 생성.
    // 다른 상태 변경으로 인한 리렌더링에서는 기존 함수 재사용.
    const onInsert = useCallback(() => {
        const nextList: number[] = list.concat(parseInt(number));
        setList(nextList);
        setNumber('');
    }, [number, list]); // 'number'나 'list'가 변경되면 함수를 새로 생성.

    const avg = useMemo(() => getAverage(list), [list]); 

    return (
        <>
            <div>
                {/* useCallback으로 기억된 함수들을 이벤트 핸들러로 사용. */}
                <input type="text" value={number} onChange={onChange} />
                <button onClick={onInsert}>등록</button>

                <ul>
                    {list.map((value: number, index: number) => (
                        <li key={index}>{value}</li>
                    ))}
                </ul>

                <div>
                    <b>평균값: </b> {avg}
                </div>
            </div>
        </>
    );
}

export default Callback;
```

### useRef

**`useRef`**는 **`.current`** 프로퍼티를 가진 변경 가능한 ref 객체를 반환하는 Hook입니다. 이 객체는 컴포넌트의 전체 생명주기 동안 유지되며, 주로 DOM 요소에 직접 접근하거나 리렌더링을 유발하지 않는 값을 저장하는 데 사용됩니다.

```
const getAverage = (numbers: number[]) => {
    if (numbers.length === 0) return 0;

    const sum = numbers.reduce((acc, cur) => acc + cur);
    return sum / numbers.length;
};

function Ref() {
    const [list, setList] = useState<number[]>([]);
    const [number, setNumber] = useState<string>('');

    // useRef를 사용하여 <input /> DOM 요소에 직접 접근할 ref 객체 생성.
    // 이후 .current 프로퍼티를 통해 실제 요소에 접근 가능.
    const inputElement = useRef<HTMLInputElement | null>(null);

    const onChange = useCallback(
        (event: React.ChangeEvent<HTMLInputElement>) =>
            setNumber(event.target.value),
        []
    );

    const onInsert = useCallback(() => {
        const nextList: number[] = list.concat(parseInt(number));
        setList(nextList);
        setNumber('');

        // '등록' 버튼 클릭 시, ref 를 통해 <input /> 요소에 직접 접근하여 포커스 효과 적용.
        // inputElement.current 가 null이 아닐 때만 focus() 호출.
        inputElement.current?.focus();
    }, [number, list]);

    const avg = useMemo(() => getAverage(list), [list]);

    return (
        <>
            <div>
                <input
                    type="text"
                    value={number}
                    onChange={onChange}
                    { /* ref 를 사용하여 위에서 생성한 'inputElement' 객체와 실제 <input /> DOM을 연결. */ }
                    ref={inputElement}
                />
                <button onClick={onInsert}>등록</button>

                <ul>
                    {list.map((value: number, index: number) => (
                        <li key={index}>{value}</li>
                    ))}
                </ul>

                <div>
                    <b>평균값: </b> {avg}
                </div>
            </div>
        </>
    );
}

export default Ref;
```

![image](useRef-1.png)
_아무런 반응 없는 'input' 컴포넌트_

![image](useRef-2.png)
_'등록' 버튼을 클릭하자 'input' 컴포넌트의 current 프로퍼티에 접근하여 Focus 상태로 변경_

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
