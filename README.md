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

## 5. 디버깅

### 5-1. Modal 관련 디버깅
<details>
<summary>create-react-app 사용시 문제</summary>
<div markdown="1">

```
You are running `create-react-app` 4.0.3, which is behind the latest release 

(5.0.0).

We no longer support global installation of Create React App.
```

* 버전으로 인한 문제 생김. 재설치한뒤 npx 빼고 사용하니 되었음

</details>

</br>

<details>
<summary>svg 아이콘 입력시 네임스페이스 속성이 지원되지 않는 상황</summary>
<div markdown="1">

* xmlns:xlink -> xmlnsXlink 처럼 JSX와 호환되도록 구문 변환 적용하니 해결

</details>
  
</br>

<details>
<summary>span 관련 css 문제</summary>
<div markdown="1">

* span으로 묶여있는 New(N) 버튼 w와 h가 안 먹어서 고민   
* span은 inline 이라서 안 먹혔던 것. inline-block으로 바꾸니 해결   

</details>
  
</br>

<details>
<summary>조금 어이 없는 실수</summary>
<div markdown="1">

* 캐러셀 슬라이드가 하나씩 나와야하는데 한꺼번에 나온 뒤 5초 후   
동시에 사라지는 현상이 발생.. css 계속 고쳐봤으나 해결이 안되어서   
첫줄부터 반복해서 확인함   

* 알고보니 carousel-conten'n't 로 클래스 네임 주고.. css엔 content로..   
스펠링 실수로 css가 전혀 안 먹혀서 발생한 문제.. 고치니 바로 작동함   
  
</details>

</br>

<details>
<summary>useInterval 작동하며 슬라이드가 밀리는 문제</summary>
<div markdown="1">

* slide에 margin을 줬을 때, 슬라이드가 넘어가면서 점점 한쪽으로 치우치는 문제   
슬라이드가 교체되면서 margin이 점점 늘어나서 생긴 문제인듯 보임   
slide가 아닌 carousel-content에 margin을 줘서 해결

</details>
  
</br>

<details>
<summary>netlify 배포 관련</summary>
<div markdown="1">

* gh-pages로 먼저 배포해보고, 이후 netlify로 배포하고자 했을 때 build.command   
부분 에러가 계속 발생   

```
npm install netlify-cli -g   
netlify deploy
```
로 해결
  
* 이 후 배포는 되었다고 떴지만 화면에 아무 것도 안 뜨는 문제   
homepage 링크가 github으로 되어있어서 netlify url로 다시 설정 후 배포

</details>


## 5. 회고 / 느낀점
> 원티드 선발 과제를 위한 클론 코딩이었는데, 리액트로 프로젝트를 만들어본적은 있지만   
  반응형으로 만들어본건 처음이라 (리액트) 아쉬움이 많았다.   
  JS에 비해 아직 리액트는 덜 익숙하다보니 모바일 퍼스트로 구현하지않고 데스크탑 기준으로   
  먼저 만든 후에 모바일 버전을 다시 추가하려하니 번거로움이 있었다.   
  그리고 기존에는 gh-pages로만 거의 배포를 하다가 netlify로 하다보니 조금은 시간이 걸렸다.   
  그래도 계속 사용하다보니 리액트 Hooks나 배포 등에 조금씩 익숙해지는 느낌인데   
  더 공부하며 연습해야겠다!




