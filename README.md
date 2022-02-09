# :pushpin: (리액트) 원티드 프리 온보딩 코스 선발 과제
> React Component 제작

>https://irrpl-ar.github.io/wanted_pre_onboarding/

</br>

## 1. 제작 기간 & 참여 인원
- 2022년 2월 3일 ~ 9일
- 개인 프로젝트

</br>

## 2. 사용 기술
#### `Front-end`
  - React JS
  - Jsx
  - CSS

</br>

## 3. 자세한 실행 방법

<details>
<summary><b>실행 방법 설명 펼치기</b></summary>
<div markdown="1">

### Modal
- Open Modal 버튼과 클릭 시 나타날 모달창 두가지로 구성되어있습니다
- Open Modal 버튼을 클릭하면 모달창이 나타나고, x 버튼을 누르면 모달창이 종료됩니다
  
### Tab
- 총 3가지 Tab이 있고, 각각 Tab 메뉴 클릭 시 해당 메뉴 글자가 굵게 나타납니다
- Tab을 누를 때마다 바로 아래 작은 페이지의 내용도 달라집니다
  
### Toggle
- 초기 상태는 회색 버튼 모양이고, 버튼을 누르면 On이 되어 초록색으로 바뀜과 동시에 볼도 이동합니다
- 한번 더 클릭하면 원 상태로 돌아갑니다
  
### Click To Edit
- 이름 / 나이를 입력할 수 있는 칸과 그에 해당하는 결과가 나타납니다
- 입력 후 빈 공간을 클릭해야 결과에 반영됩니다

</div>
</details>

</br>

## 4. 구현 방법 및 이유

<details>
<summary><b>구현 방법 및 이유 설명 펼치기</b></summary>
<div markdown="1">

### Modal
- 모달 기능에 있어서 핵심이 모달창이 열릴 때는 모달창만 보이고 버튼은 사라지며   
  모달창이 닫힐 때는 모달창이 사라지고 버튼이 다시 보이는 부분이라고 생각해서   
  그 부분을 중점적으로 생각하며 구현했습니다
- 삼항연산자와 useState를 활용하였습니다. 'modal' 변수가 true일 경우 모달 컴포넌트를 렌더링하고,   
  css class에는 'hidden'(display: none) 을 추가하여 버튼이 사라지도록 했습니다
- App.js에서 모달을 open하고 close하는 간단한 props를 전달하여 사용했습니다
  
### Tab
- 탭 디자인을 보기 좋게 하기 위해 React Bootstrap을 설치하여 디자인에 활용했습니다
- 총 세가지 탭이므로 0 1 2 각각 번호를 부여하여 클릭시 부여된 번호로 state를 변경하고   
  css class도 그에 맞게 변경했습니다
- 탭이 세개이므로 탭 아래 내용도 총 세가지가 필요했는데, 이 부분에 있어서는   
  TabContent로 따로 분리하고 Tab 내에는 컴포넌트를 한번 렌더링하면 효율적일 것 같아 그렇게 구현했습니다   
  위에서 부여한 번호에 따라 각각 해당되는 div가 출력되도록 if문을 사용했습니다
  
### Toggle
- 토글 기능이기 때문에 처음 state를 지정하고, 클릭시마다 !변수 로 true <-> false 되도록 구현했습니다
- on이 될 때 색 변환 외에도 볼 이동이 부드럽게 되도록 transition: transform 0.2s linear; 를 설정했습니다
- translateX는 값을 대입해보면서 가장 화면상 보기 좋은 값으로 정했습니다
  
### Click To Edit
- 이름 라벨이 있는 input창과 나이 라벨이 있는 input창을 각각 만들고, 아래에 입력값에 따른 결과가 나오도록 구현했습니다
- 처음에 기본적으로 빈 값이 아니라 예시 사용자 정보가 나올 수 있도록, 임의의 이름과 나이가 있는 데이터를 만들고   
  기본값으로 주었습니다 (useState)
- input창과 관련된 내용을 하위 컴포넌트로 따로 분리하고, 전체적인 렌더링은 Click To Edit에서 담당하도록 했습니다
- 하위 컴포넌트 InputBox에서는 변수 상태에 따라 클릭을 하면 편집 가능한 input창으로, 입력 후에는 span태그처럼 보이도록   
  삼항연산자를 활용했습니다
- 입력되는 값(name, age)를 values로 묶어서 상위 컴포넌트로 전달하고, input창 선택을 위해 useRef를 활용했습니다   
  span(이름 / 나이) 클릭 시 -> handleClick 작동하여 편집모드 켜짐(useState true) -> input.current.focus 됨   
  글자 입력하고 나면 -> onChange에 달아둔 함수 작동하여 e.target.value 담기고 -> 바깥 공간 클릭하면 onBlur에 달아둔   
  함수 작동하여 편집모드 꺼짐(useState false) 그리고 새 값이 handleValueChange에 전달됨
- 이렇게 전달된 값은 handleValueChange를 통해 상위 컴포넌트에 전달하여 새로운 값이 화면에 결과로 렌더링 되도록 했습니다
  

</div>
</details>

</br>

## 5. 에러 핸들링

### 5-1. Modal 관련 
<details>
<summary>git clone 후 npm error</summary>
<div markdown="1">

* 네가지 기능중 모달을 처음으로 만들었고, 시작을 위해서 git clone을 해온 뒤 서버모드를 열려하니   
  계속 npm error가 뜨면서 경로를 찾을 수 없다고 나옴
* 이전에 리액트로 개인 프로젝트를 만들 때는 한번도 보지 못한 에러라 git clone npm error로 계속 구글링함   
* 구글링 + 에러 문구 다시 찬찬히 읽어보며 파악한 것인데, wanted_pre_onboarding 이라는 폴더 아래에   
  custom-component라는 폴더가 하나 더 있기 때문에 이 폴더에서 작업을 해야하는데   
  wanted_pre_onboarding 위치에서 npm 명령을 치니 경로 에러가 났음
* 경로 수정 후 정상 작동함

</details>

</br>

<details>
<summary>Open Modal 버튼 형태는 남고 글자만 사라지는 문제</summary>
<div markdown="1">

* 처음에 button 태그로 Open Modal 버튼을 만들지 않고 div를 버튼처럼 사용하려 했더니   
  삼항연산자로 class 붙였다 뗐다 할 때 버튼 형태는 남고 글자만 사라지게 작동됨   
* div 내에 button태그로 분리하고 button 태그에만 삼항연산자 붙이니 정상 작동함

</details>
  
</br>

<details>
<summary>class에 삼항연산자 사용시 문제</summary>
<div markdown="1">

```
<div className={'modal-button' + (setModal(true)?' hidden':"")}
```
* setModal에 따라가 아니라 modal 상태에 따라 true/false로 태그 붙여야함   
  아래와 같이 수정하여 해결

```
<button className={`modal-button ${modal?'hidden':''}`}
```

</details>
  
</br>

### 5-2. Tab 관련 에러 핸들링
<details>
<summary>리액트 부트스트랩 사용시 디자인 적용 제대로 안되는 문제</summary>
<div markdown="1">

* import 'bootstrap/dist/css/bootstrap.css'; 생략해서 생김
* index.js에 추가하여 해결
  
</details>

</br>

<details>
<summary>return 관련 에러</summary>
<div markdown="1">

* TabContents 컴포넌트에 return()으로 묶고 그 안에 if문별로 return 쓰려하니 오류
* 최상단의 return 빼서 해결

</details>
  
</br>

<details>
<summary>if문에서 Missing semicolon 오류</summary>
<div markdown="1">

* 아무리 봐도 semicolon 문제는 없어 보여서 계속 찾았는데, else if 띄어쓰기함으로   
  오류 해결

</details>
  
</br>

### 5-3. Toggle 관련 에러 핸들링
<details>
<summary>css transition 속성이 안 먹히는 문제</summary>
<div markdown="1">

* <Toggle /> 안에 <ToggleButton /> 컴포넌트를 중첩시켜서 props를 전달하려하니
배경색 변경은 되는데 ball transition이 제대로 안 먹힘
* 상세한 원인은 찾지 못했으나 컴포넌트 중첩하지않고 하나로 통일시키니 해결됨
  
</details>

</br>

<details>
<summary>ontoggle과 toggleOn 혼동</summary>
<div markdown="1">

* ontoggle은 useState 변수이고, toggleOn은 함수인데 이름이 비슷해서 잘못 사용함   
* 첫줄부터 다시 보면서 변수 / 함수 다시 정리하여 해결함

</details>
  
</br>

### 5-4. Click To Edit 관련 에러 핸들링
<details>
<summary>props 전달 문제</summary>
<div markdown="1">

```
  { name, age, handleValueChange }) => {

    const { name, age, handleValueChange } = props;
```
  
* 위와 같이 선언하여 props 전달이 제대로 안 됨
* const ~ = props를 쓸 경우 윗줄에는 props로 받아오면됨
  
</details>

</br>

<details>
<summary>변수명 정리</summary>
<div markdown="1">

* value 관련 비슷한 변수 많아서 헷갈림   
  newValue(새로 받아온 값)와 values(name과 age 묶음)로 바꾸고   
  같은 양식에 데이터만 다르게 넣을것이니 name과 age를 values로 묶어서 전달

</details>

</br>

<details>
<summary>클릭시 input창이 안뜨는 문제</summary>
<div markdown="1">

* 클릭시 input으로 변경되어야하는데 값이 하드코딩되어 나타남
* setEditing을 true로 만들어주는 함수가 없어서 생긴 문제
  
```
  const handleClick = () => {
        setEditing(true);
    }
```

* 위와 같은 함수 추가하여 onClick에 달아줘서 해결

</details>

</br>

<details>
<summary>inputbox 테두리가 이중으로 지저분하게 나타나는 문제</summary>
<div markdown="1">

* inputbox 테두리가 기본 검정색과 새로 지정한 색상이 이중으로 나타나며 지저분해짐
* outline 0 줘서 해결

</details>


## 5. 회고 / 느낀점
> 지난번 원티드 선발 과제에 이어 두번째 과제 도전이었는데, 지난번보다는 수월했던 것 같다   
  리액트 컴포넌트중 핵심적인 기능을 만들어보면서 큰 틀에서 조금씩 변화를 주면서   
  다양한 기능을 더 만들 수 있겠다는 생각을 했다   
  리액트를 공부할수록 상태 변화 및 관리에 리액트가 아주 유용하다는 생각이 드는데   
  앞으로도 더 공부하고싶다




