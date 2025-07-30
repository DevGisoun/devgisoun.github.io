---
title: "[스나이퍼팩토리] 한컴AI 2기 - 교육 4주차 후기"
description: >-
  Typescript 기반 React 를 활용한 팀 프로젝트 진행.
author: gisoun
date: 2025-07-25 17:05:00 +0900
categories: [Hancom AI Academy, Education]
tags: [hancom, hancom ai academy, education, ai, html, css, javascript, js]
pin: false
media_subpath: '/assets/posts/20250725'
published: true
---

> 2025\. 7\. 21\. ~ 2025\. 7\. 25\.

---

## 팀 프로젝트

이번 주차에는 이제까지 배워온 것들을 바탕으로 랜덤하게 팀을 구성하고 주제를 선택한 **미니 프로젝트**를 진행하였습니다.  

주제는 지도 API 연동 기반 맛집 리스트, 설문 폼 플랫폼, 재고 관리 플랫폼 등 여러가지가 있었으며 저희 팀은 **설문 폼 플랫폼** 주제를 선택하여 진행하기로 하였습니다.  

프로젝트 진행에 앞서 팀원들과 시간을 짧게 가졌으며 프로젝트의 볼륨을 무리해서 크게 하지 않고 **지난 것들을 복습**하여 프로젝트를 진행하는 것에 의의를 둬 목표를 잡았습니다.

---

## 사용 기술 스택

- **`React`**: 이번 프로젝트는 **`Next.js`**, **`React`** 중 하나를 선택하여 진행할 수 있었습니다. **`Next.js`** 는 한 번도 사용해본 적 없지만 새로운 기술에 도전할 기회가 생긴다는 장점이 있었고, **`React`** 는 이제껏 강의에서 여러 번 사용하여 꽤나 익숙하며 아직 부족한 숙련도를 다질 수 있다는 장점이 있었는데, 저희 팀은 이중 **`React`** 를 선택하였습니다.
- **`Supabase`**: **사용자 인증(회원가입 및 로그인)** 구현을 쉽게 하고 **관계형 데이터베이스의 장점**을 살릴 수 있다는 점에서 데이터베이스는 **`Supabase`** 를 사용하였습니다.
- **`Shadcn UI`**: 이제까지 강의 실습에서 사용해왔으며, 잘 갖춰진 컴포넌트를 입맛에 맞게 프로젝트에 접목하는 것은 프로젝트 진행 시간을 단축하고 동시에 매우 좋은 연습이 되어줄 것이기에 메인 컴포넌트 라이브러리로 **`Shadcn UI`** 를 사용하였습니다.
- **`Git/Github`**: 팀원들과의 협업과 프로젝트의 일관성을 유지하기 위해 **`Github`** 의 시스템을 적극 활용하였습니다. 각자의 **`Branch`**를 나누고 **`Issues`** 에 개발 현황을 기록하고 **`Pull Request`** 에서 팀원들끼리 각자의 코드를 공유하고 리뷰할 수 있었습니다.

---

## NavBar (헤더)

페이지의 전체 네비게이션 바를 구성하는 컴포넌트입니다.  

**`NavBar`** 컴포넌트는 별도로 제작한 **`NavLink`** 컴포넌트들을 모아 실제 메뉴를 구성하고, 현재 URL 경로에 따라 특정 버튼을 보여주거나 숨기는 역할도 합니다.

### 현재 경로 가져오기 (useLocation)

```
const location = useLocation();
const pathname = location.pathname;
```

**`react-router-dom`** 라이브러리의 **`useLocation`** Hook을 사용하여 현재 페이지의 위치 정보를 가져옵니다.  

**`location.pathname`**을 통해 실제 URL 경로 문자열 (ex. **`/list`**)을 얻을 수 있습니다.  

### NavLink

현재 페이지에 해당하는 네비게이션 링크에 동적으로 스타일을 적용하는 재사용 가능하게 제작한 **`NavLink`** 컴포넌트입니다. 상위 컴포넌트인 **`Navbar`**에서 현재 URL(**`useLocation`**)을 비교하여 **`isActive`** prop을 전달받는 방식으로 사용됩니다.  

**특징**
- **`조건부 스타일링`**: **`isActive`** prop이 **`true`**이면 텍스트 색상을 네이버 컬러(**`text-naver`**)로 강조하고, **`false`** 라면 기본 컬러(**`text-gray-400`**)을 적용합니다.
- **`조건부 렌더링`**: **`isActive`** prop이 **`true`**일 때만 **`&&`** 연산자를 통해 하단 밑줄 **`<span>`** 요소를 렌더링합니다.

### 경로에 따른 조건부 렌더링

```
{pathname === '/list' && (<Button>...</Button>)}
```

<kbd>설문 만들기</kbd> 버튼을 오직 현재 경로가 **`/list`**일 때만 보여줍니다. 다른 페이지에서는 이 버튼이 렌더링되지 않습니다.

---

## 설문 제목 및 기간 입력 컴포넌트

**`QuestionTitle`** 컴포넌트는 **사용자가 설문 제목과 설명을 직접 입력**하고, 복잡할 수 있는 **기간 설정과 캘린더** 구현을 **`Shadcn UI`**의 **`Dialog`** 컴포넌트를 통해 설정할 수 있습니다.

**특징**
- **`QuestionTitle`** 컴포넌트는 **`title`**, **`description`** 같은 상태 값과 상태 변경 함수를 모두 **`props`**로 전달받습니다. 컴포넌트 스스로 상태를 소유하는 대신, 모든 상태 관리를 부모 컴포넌트에게 위임하여 전체 폼의 상태를 한곳에서 통합적으로 관리하기 용이하게 구성되어 있습니다.  
   ```
   interface QuestionTitleProps {
     ...
     title: string;
     description: string;
     handleTitleChange: (e: React.ChangeEvent<HTMLInputElement>) => void;
     handleDescriptionChange: (e: React.ChangeEvent<HTMLInputElement>) => void;
     ...
   }
   ```
- **`임시 상태 관리`**: **설문 기간 (시작, 종료)**처럼 여러 값을 동시에 변경해야 하는 UI에서는, 사용자가 <kbd>취소</kbd> 버튼을 눌렀을 때 변경사항이 반영되지 않아야 합니다.
  - 기간을 설정할 수 있는 **`Dialog`** 가 열렸을 때만 사용하는 임시 상태 변수들(**`startTypeState`**, **`startDateState`** 등)을 **`useState`** 로 선언합니다.  
     ```
     ...

     // Dialog 내부에서만 사용할 임시 상태
     const [startTypeState, setStartTypeState] = useState<string>(startDateTime ? SurveyPeriod.CUSTOM : SurveyPeriod.START);
     const [startDateState, setStartDateState] = useState<string>(formatDate(startDateTime));
     
     ...

     // 부모의 상태가 바뀌면 Dialog 내부 상태도 동기화
     useEffect(() => { ... }, [startDateTime, isDialogOpen]);
     useEffect(() => { ... }, [endDateTime, isDialogOpen]);

     ...
     ```
  - 사용자는 이 임시 상태 위에서 자유롭게 날짜와 시간을 변경하고, 오직 **<kbd>확인</kbd> 버튼을 눌렀을 때만 `handleDialogConfirm` 함수가 호출되어 부모 컴포넌트의 실제 상태를 업데이트**합니다. <kbd>취소</kbd> 버튼을 누르면 임시 상태는 그냥 사라지므로, 원래 값이 유지됩니다.
     ```
     <DialogFooter className="sm:justify-start">
       <div className="w-full flex items-center justify-center gap-2">
         <DialogClose asChild>
           <Button
             type="button"
             className="w-1/2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 rounded"
           >
             취소
           </Button>
         </DialogClose>
         <Button
           type="button"
           className="w-1/2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 rounded"
           onClick={handleDialogConfirm} {/* 임시 상태를 부모의 실제 상태로 반영 */}
         >
           확인
         </Button>
       </div>
     </DialogFooter>     
     ```
  - ⭐ 이러한 컴포넌트 구조는 사용자에게 **안전한 수정 환경을 제공**하여 경험을 크게 향상시킵니다.
- **`useMemo` `를 이용한 연산 최적화`**: **`dateConfig`**는 여러 상태 값(시작일, 종료일, 기간 적용 여부 등)을 조합해 화면에 표시될 문자열을 만듭니다.  
   ```
   // 표시될 날짜 텍스트 계산
   const dateConfig = useMemo(() => {
     const startPart = startType !== SurveyPeriod.CUSTOM ?
       "즉시 시작" : `${startDate} ${startTime}`;
     const endPart = endType !== SurveyPeriod.CUSTOM ?
       "제한 없음" : `${endDate} ${endTime}`;
     return `${startPart} ~ ${endPart}`;
   }, [startType, startDate, startTime, endType, endDate, endTime]);
   
   ...
   
   <DialogTrigger asChild>
     <Input
       readOnly
       type="text"
       value={dateConfig}
       className="focus-visible:ring-0 focus-visible:ring-offset-0"
     />
   </DialogTrigger>
   ```
  - 이 값은 관련 상태가 변경될 때만 다시 계산하면 충분합니다. **`useMemo`**를 사용하면 불필요한 리렌더링 시에도 복잡한 문자열 조합 연산을 반복하지 않아 성능을 최적화할 수 있습니다.

---

## 날짜/시간 선택 컴포넌트

사용자는 **`QuestionTitle`** 컴포넌트 내에서 **'즉시 시작'**이나 **'제한 없음'**처럼 간단한 옵션을 선택할 수도 있고, 특정 **날짜**와 **시간**까지 직접 지정해야 할 수도 있어야 합니다.  

이에 자식 컴포넌트인 **`DateConfigRow`** 컴포넌트는 날짜와 시간 선택 로직을 하나의 행(Row)으로 캡슐화한 컴포넌트로, 재사용성을 높여 **'시작일'**과 **'종료일'** 설정에 모두 활용될 수 있도록 설계되었습니다.

**하나의 컴포넌트가 많은 상태를 동시에 관리해야 했다는 점**과 **각 컴포넌트들을 하나의 자연스러운 흐름으로 엮어야** 했다보니, 개인적으로 구현하는데 생각보다 꽤 애먹기도 했습니다.

**특징**
- **`UI 라이브러리의 조합`**: **`DateConfigRow`** 컴포넌트는 최대한 좋은 사용자 경험을 이끌어내기 위해 여러 UI 컴포넌트를 유기적으로 조합합니다.  
  - **`RadioGroup`**: **'즉시 시작'**/**'직접 설정'** 같은 선택지를 제공합니다.  
     ```
     {/* 옵션 선택을 위한 라디오 버튼 그룹 */}
     <RadioGroup
       defaultValue={selectedValue}
       onValueChange={handleValueChange}
     >
       {/* ... 라디오 버튼 옵션들 ... */}
     </RadioGroup>     
     ```
  - **`Popover + Calendar`**: 버튼이나 입력 필드를 클릭했을 때, 그 자리에 캘린더가 팝업처럼 나타나도록 구현합니다.  
     ```
     {/* '직접 설정'을 선택했을 때만 날짜/시간 선택 UI 표시 */}
     { selectedValue === SurveyPeriod.CUSTOM && (<>... ... ...</>) }

     ...
     
     {/* Popover와 Calendar를 이용한 날짜 선택 */}
     <Popover open={openCalendar} onOpenChange={setOpenCalendar}>
       ...

      <PopoverContent>
        <Calendar
          mode="single"
          selected={selectedDate}
          onSelect={(date) => {
            // ... 날짜 선택 시 상태 업데이트 및 부모에게 상태 알림
            onSetDateChange(formatDate(date));
            setOpenCalendar(false);
          }}
        />
      </PopoverContent>

       ...
     </Popover>
     ```
  - **`DropdownMenu` + `ScrollArea`**: 수많은 시간 옵션을 스크롤 가능한 **드롭다운** 메뉴에 담아 깔끔하게 제공합니다.  
     ```
     {/* DropdownMenu와 ScrollArea를 이용한 시간 선택 */}
     <DropdownMenu>
       ...

       <DropdownMenuContent>
         <ScrollArea className="h-72">
           {timeOptions.map((time) => (
             <DropdownMenuItem
               key={time}
               onSelect={() => {
                 // ... 시간 선택 시 상태 업데이트 및 부모에게 상태 알림
                 onSetTimeChange(time);
               }}
             >
               {time}
             </DropdownMenuItem>
           ))}
         </ScrollArea>
       </DropdownMenuContent>

       ...
     </DropdownMenu>
     ```
- **`상태 관리`**: 이 컴포넌트는 **자체적인 UI 상태**와 부모 컴포넌트인 **`QuestionTitle`** 컴포넌트로부터 받는 **상태 업데이트 함수**를 모두 가집니다.
  - **`내부 상태` `(useState)`**: **`selectedValue`**(선택된 라디오 버튼 옵션), **`openCalendar`**(캘린더 활성화 여부) 등은 **`DateConfigRow`** 컴포넌트 내부에서만 관리됩니다.  
     ```
     // 라디오 그룹 상태 관리
     const [selectedValue, setSelectedValue] = useState<string | undefined>(
       dateType
     );

     // 캘린더 상태 관리
     const [openCalendar, setOpenCalendar] = useState(false);
     ```
  - **`외부와 소통` `(props)`**: 사용자가 최종적으로 날짜나 시간을 선택하면, **`props`**로 전달받은 **`onSetDateChange`**, **`onSetTimeChange`** 함수를 호출하여 부모 컴포넌트인 **`QuestionTitle`** 의 상태를 변경합니다. 이로써 복잡한 UI 로직은 **`DateConfigRow`** 안에 캡슐화되고, 부모 컴포넌트는 최종 결과값만 신경 쓸 수 있게 됩니다.
    ```
    interface DateConfigRowProps {
      ...

      onSetDateChange: (value: string) => void;
      onSetTimeChange: (value: string) => void;

      ...
    }
    ```
- **`성능 최적화` (`useMemo`)**
  - 30분 단위의 시간 목록(**`timeOptions`**)은 한 번만 생성하면 다시 만들 필요가 없는 데이터입니다. **`useMemo`**를 사용해 이 목록을 처음 렌더링될 때만 계산하고 그 결과를 메모리에 저장해 둡니다. 이것으로 컴포넌트가 리렌더링될 때마다 불필요한 반복문이 실행되는 것을 막아 성능을 확보할 수 있습니다.
    ```
    // 처음 렌더링될 때 단 한 번만, 30분 간격의 시간 목록 동적 생성 (00:00 ~ 23:30).
    const timeOptions = useMemo(() => {
      const timeList = [];

      // 24시간을 30분 단위로 나누면 총 48개의 구간이 생기므로 48번 반복
      for (let i = 0; i < 48; i++) {
        const hour = Math.floor(i / 2);
        const minute = (i % 2) * 30;
        const period = hour < 12 ? "오전" : "오후";
    
       // 24시간제를 12시간제로 변환
       let displayHour = hour % 12;
    
       // 변환 결과가 0이면 자정 또는 정오이므로, 12시로 표시
       if (displayHour === 0) displayHour = 12;
    
       // 최종 시간 문자열을 "오전/오후 HH:MM" 형식으로 조합
       const timeStr = `${period} ${String(displayHour).padStart(
          2,
          "0"
        )}:${String(minute).padStart(2, "0")}`;
    
       timeList.push(timeStr);
      }
      return timeList;
    }, []);
    ```

---

## 설문 작성 페이지 상태와 Supabase 연동

**`FormBuilderPage`** 페이지는 위에서 설명한 **`QuestionTitle`**, **`DateConfigRow`** 같은 개별 컴포넌트들의 최상위 컴포넌트로, **설문 전체의 상태**를 관리하고, 사용자의 최종 입력을 **Supabase에 저장**합니다.

**특징**
- **`상태와` `QuestionTitle` `컴포넌트 연결`**: **`FormBuilderPage`** 페이지에서는 **`useState`**를 사용해 설문 기간과 관련된 모든 상태를 정의합니다.  
   ```
   // QuestionTitle과 관련된 모든 상태를 이 페이지가 소유
   const [title, setTitle] = useState("");
   const [description, setDescription] = useState("");
   const [startType, setStartType] = useState<string>(SurveyPeriod.START);
   const [endType, setEndType] = useState<string>(SurveyPeriod.UNLIMITED);
   
   ...

   {/* 페이지가 소유한 상태와 상태 변경 함수를 QuestionTitle에 props로 전달 */}
   <QuestionTitle
     title={title}
     description={description}
     startType={startType}
     endType={endType}
     
     ...
   />

   ...
   ```
- **`데이터 중앙 관리`**: **`FormBuilderPage`** 페이지가 모든 상태를 소유하고, **`QuestionTitle`** 컴포넌트는 그 상태를 **`props`**로 전달받아 화면에 표시하기만 합니다. 또한, 만약 사용자가 **`QuestionTitle`** 내부의 **`Input`**이나 **`Dialog`**를 조작하면, **`props`**로 함께 전달된 **`setStartType`** 같은 상태 변경 함수가 호출되어 부모의 상태를 업데이트합니다.  
   즉, **데이터는 위에서 아래로**, **변경 요청은 아래에서 위로** 전달되는 **단방향 데이터 흐름**을 통해 상태가 변경되는 지점을 예측하기 쉽게 하여 안정성과 유지보수성을 챙길 수 있었습니다.
- **`UI 상태를 데이터베이스 Payload로 변환`**: 사용자가 <kbd>폼 저장</kbd> 버튼을 누르면, **`handleSaveForm`** 함수가 실행됩니다. 이때 페이지가 관리하던 UI 상태들(**`startDate`**, **`startTime`** 등)을 Supabase 가 이해할 수 있는 형식으로 가공하여 전송합니다.  
   ```
   const handleSaveForm = async () => {
     // ...
     
     const { error: saveError } = await supabase.rpc(
       // ...
       
       {
         payload: {
           // ...

           title,
           description,
           // '직접 설정'을 택했을 때만 날짜/시간 값을, 아니면 null을 전송
           start_time:
             startType === SurveyPeriod.CUSTOM
               ? parseDateTime(startDate, startTime) // '2025. 07. 28.', '오후 02:30' -> '2025-07-28T14:30:00Z'
               : null,
           end_time:
             endType === SurveyPeriod.CUSTOM
               ? parseDateTime(endDate, endTime)
               : null,
           
           // ...
         },
       }

       // ...
     );
     // ...
   };
   ```
  - **`조건부 데이터`**: **삼항 연산자**를 사용해 **`startType`**이 **`'CUSTOM'`**(날짜 직접 설정)일 때만 **`parseDateTime`** 함수로 날짜/시간 문자열을 **`Date`** 로 변환합니다. 만약 '즉시 시작' 옵션을 선택했다면, Supabase 에는 **`null`** 값이 저장됩니다.
  - **`UI와 데이터의 분리`**: UI에서는 사용자가 보기 편한 '**2025. 07. 28.**' 같은 문자열로 상태를 관리하고, Supabase 로 보낼 때만 형식을 **`Date`** 로 변환합니다. 이를 통해 개발자/고객 간의 관심사를 명확하게 분리할 수 있었습니다.

---

본 후기는 [한글과컴퓨터x한국생산성본부x스나이퍼팩토리] 한컴 AI 아카데미 2기 (B-log) 리뷰로 작성 되었습니다.

#한컴AI아카데미2기 #AI개발자 #AI개발자교육 #한글과컴퓨터 #한국생산성본부 #스나이퍼팩토리 #부트캠프 #AI전문가양성 #개발자교육 #개발자취업
