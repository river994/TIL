## 쇼핑몰 프로젝트 : 프로젝트 생성 & Bootstrap 설치
  - yarn 설치 권장 : npm 보다 빠름
  - React-bootstrap
  `npm install react-bootstrap bootstrap`
  - bootStrap 사용 시 요소 import 한 후 사용
  `import { Navbar, Nav, Button, Jumbotron } from 'react-bootstrap';`

## 쇼핑몰 레이아웃 디자인 시간
  - src는 발행시 압축 -> public에 이미지 넣기

## 코드가 길다면 import / export 사용해보기
  - export : 마지막에 한 번만 사용
```javascript
export default variableName
export { var1, var2 }

import name from './directory.js'; // export default 된 컴포넌트 가져오기
import { var1, var2 } from './directory.js'; // {} 안의 변수, 함수 가져오기
```
## 상품목록 Component화 + 반복문
  - `/* eslint-disable */` eslint warning 무시하기
  - props 전송법
    1. `<자식컴포넌트 보낼이름={전송할 state} 다른방식="일반문자"/>`
    2. `function 자식컴포넌트(props){}`
    3. `props.보낼이름` 사용
  - map key값 설정 시 return 되는 부분에 key 값 줄 것

## router 1 : setup
  - react-router-dom 설치   
    `npm install react-router-dom`
  - react-router-dom index.js에 연결   
  `import { BrowserRouter } from 'react-router-dom'`
  - index.js에 추가    `<BrowserRouter><App /></BrowserRouter>`
  - App.js에 필요한 요소  import    `import { Link, Route, Switch } from form 'react-router-dom'`
  - Route로 페이지 나누기    `<Route path="/example" component={ componentName }></Route>`
  - Route 경로 완벽 일치 시 페이지 노출 원하면 `<Route exact path=''>`

  - React Router 특징 : html 파일이 하나에서 이동이 이루어지는 것

## HashRouter && BrowserRouter
  - HashRouter
    + 라우팅 안전하게 할 수 있게 도와줌
    + 사이트 주소 뒤에 #이 붙는데 # 뒤에 적는 것은 서버로 전달 X

  - BrowserRouter
    + 라우팅을 리액트가 아니라 서버에게 요청할 가능성이 있음
    + 이를 방지하기 위해 서버에 서버 라우팅 방지 API 작성 필요

## router 2 : Link, Switch, History
  - 페이지 이동하는 버튼
    1. `href=""` 삭제
    2. 링크 대상체 `<Link to="/path"> 버튼 </Link>`
  
  - React Router custom 버튼
    1. `import { useHistory } from 'react-router-dom'`
    2. `let history = useHistory()` react-router-dom v5 이상 / react v16.3 이상
    3. 뒤로가기 : `<button onClick={ ()=>{ history.goBack() } }>` 
    4. 특정 페이지 이동 : `<button onClick={ ()=>{ history.push() } }>`

  - Switch 컴포넌트
    + Router 주소가 여러개가 일치해도 하나만 노출하고 싶을 때 사용
    + 해당하는 `<Route>`를 `<Switch>`로 감싸면 상단에서 일치하는 요소 하나만 노출
    + `<Route path="/:id">` 주소에 어떤 문자열이라도 오면 보여줌

## router 3 : URL Parameter
  - 데이터 보관하는 법
    + 중요한 데이터는 최상위 컴포넌트 `App`에 보관
    + 상위 컴포넌트에서 하위 컴포넌트로 보내는 방식이 쉬움
    + 데이터가 너무 많을 경우 -> 데이터 파일 따로 작성 OR redux 파일에 보관
 
  - URL Parameter 이용하는 법
    + `import { useParams } from 'react-router-dom'` 
    + `let { varName } = useParams()` {사용자가 입력한 URL 파라미터}

## find 함수 사용
```javascript
let chkVal = useParams();
let newVar = props.arrayName.find(function(arrayItem){
  return arrayItem.propsName == chkVal
})
```

## styled-components를 이용한 CSS 스타일링
  - styled-components란?
    + class 선언없이 컴포넌트에 CSS를 직접 적용 (CSS in JS)

  - 사용하는 법
    1. `npm install styled-components` in terminal
    2. `import styled from 'styled-components'`
    3. let componentName = styled.div` padding: 20px;`;

```javascript
let titleText = styled.h4`
  font-size: 28px;
  color: ${ props => props.color };
`;
```

## SASS 사용하기
  - SASS란?
    + CSS pre-processor로 변수, 함수, 반복문, 연산자 등을 사용해 CSS의 가독성과 재사용성을 높이기 위한 CSS extension

```javascript
  npm install node-sass // in terminal

  @import './reset.scss'; // import 문법

  $main_color : red; // 변수 사용 가능
  @mixin modal(){
  } // 함수 만드는 mixin

  .my-alert {
    @include modal(); // 함수 사용시 @include 함수명()
    background-color: $alert_color;
    p {
      margin-bottom: 0;
    }
  }// nesting 문법
  .my-alert-notice {
    @extend .my-alert; // css 상속
    background-color: blue;
  }
```

## Lifecycle Hook & useEffect
  - Lifecycle Hook란?
    + 컴포넌트의 생명주기 중간 명령을 내리는 것

```javascript
class sampleClass extends React.Component { 
  componentDidMount(){
  }
  componentWillUnmount(){
  }
}
```
  - useEffect Hook란?
    + React 16.8 부터 사용 가능
    + 컴포넌트가 mount 되었을 때, update 될 때 특정 코드를 실행할 수 있음

```javascript
import React, { useState, useEffect } from 'react'; // useEffect import 필요
function ProductDetail(props){
  useEffect(()=>{
    // component 생성될 때 실행
    return function funcName(){
      // return function -> component 삭제 시 실행
    }
  });
  useEffect(()=>{
    // useEffect 여러개 사용 시 순서대로 실행
  });
}
```
## 컴포넌트 사라지는 코드 작성
```javascript
function ProductDetail(props){
  useEffect(()=>{
    let delayTimer = setTimeout(function(){
      let alert = document.querySelector('.my-alert');
      alert.parentNode.removeChild(alert);
    }, 2000) // 내가 작성한 방식. JS 사용했고 UI 상태 저장 X

    let delayTimer = setTimeout(()=>{
      hideAlert(false);
      return ()=>{ clearTimeout(delayTimer) };
    }, 2000) // 강의 방식. useState로 UI 상태 저장해서 조건문으로 노출
  });
  let [alertStat, hideAlert] = useState(true);
  return(
    {
      alertStat === true
      ? <div className="my-alert">
        <p>품절 임박</p>
      </div>
      : null
    }
  )
}
```
  - 항상 보이는 UI가 아니라면 switch 를 통해 강의 방식대로 작성하는 것이 좋음
  - `setTimeout` 함수 사용시 `clearTimeout` 함수 실행으로 버그 예방 

```javascript
let delayTimer = setTimeout(()=>{
  return ()=>{ clearTimeout(delayTimer) };
}, 2000)
```

## React update(rerender) 시 실행되는 useEffect
```javascript
let [alertStat, hideAlert] = useState(true);

useEffect(()=>{
  console.log('only in alert')
}, [alertStat])
```
  - useEffect 함수의 `{}` 뒤에 `,[조건변수]` => `[조건변수]` 변경시에만 `{}` 실행
  - `[조건변수]` 가 공백일 시 업데이트 시 실행 아예 안됨

## Ajax in React
  - Ajax란?
    + 서버에 새로고침 없이 요청을 할 수 있게 도와주는 것

  - 요청의 종류
    + GET 요청 : 특정 페이지 / 자료 읽기
    + POST 요청 : 서버로 중요 정보 전달
  
  - Ajax 사용법
    1. JQuery 설치 후 $.ajax() 사용
    2. axios 설치 후 axios.get() 사용 // IE8 이상 가능
    3. javaScript fetch() 사용 // IE 호환X
  
  - axios 사용법
  ```javascript
  npm install axios // in terminal

  import axios from 'axios';
  
  function funcName(){
    return (
      <button onClick={ ()=>{ 
        axios.post('url');
        axios.get('url')
        .then((result)=>{ 
          console.log(result) // result.data 시 data 결과값만
         })
        .catch(()=>{  })
        }}
      >
    )
  }
  ```
  1. axios.get(데이터 요청할 URL)
  2. axios.get().then(get요청 성공 시 실행할 코드)
  3. axios.get().then().catch(get 요청 실패 시 실행할 코드)
  4. axios.post(서버 URL)

  + component 로드시 ajax로 데이터 가지고 오고 싶다면 `useEffect(()=>{ axios.get() }, []);`

## axios와 fetch의 차이
  - axios : JSON을 Object로 자동 변환
  - fetch : 자동으로 자료 변환X Object로 변환하는 과정 필요

## React 배포
  - `npm run build` -> build 폴더 생성
  - 첫 페이지 로딩 속도 빠르게 하기 위해서는 [lazy 함수](https://reactjs.org/docs/code-splitting.html#route-based-code-splitting) 이용 가능

## props 대신 사용하는 Context API
  -`let contextCon = React.createContext()`로 범위 생성
  - createContext()로 같은 변수값을 공유할 범위를 생성
  - `<contextCon.Provider></contextCon.Provider>`로 같은 값을 공유할 HTML 범위 지정
  - `<contextCon.Provider value={ 공유하는 값 }>`
  - 공유하는 컴포넌트 안에서 `let varName = useContext(contextCon)`으로 공유된 값 저장 후 사용 가능

  - 다른 파일 간에 값 공유하고 싶을 때
    1. `export let stockContext = React.createContext()` 변수를 export 해서 외부에서 사용 가능하게 준비
    2. `import { stockContext } from './App.js'` 사용할 파일에서 import
    3. 그 이후는 상동
 
  - props/Context API 대신 Redux 사용 가능
    + Redux란 : 모든 컴포넌트 파일들이 같은 값을 공유할 수 있는 저장공간 생성 + state 데이터 관리 기능

## animation in React
  - 애니메이션 class 제작 후 등장/업데이트 될 때 className에 부착하는 방식
  - 애니메이션 라이브러리 `react-transition-group` 사용
    1. `npm install `react-transition-group` 설치
    2. `import { CSSTransition } from 'react-transition-group';
    3. `<CSSTransition>` 으로 애니메이션 필요한 컴포넌트 감싸기 
    4. `<CSSTransition in={} className="tabAnimation" timeout={}>` 필요한 속성 추가
    5. `in={true}` 일 시 애니메이션 동작, false면 동작X, state로 boolean 값 저장해서 사용
    6. `.tabAnimation-enter` 애니메이션 시작 시 적용되는 CSS
    7. `.tabAnimation-enter-active` 애니메이션 동작 때 적용되는 CSS
    8. `.tabAnimation-enter-exit` 애니메이션 마지막에 적용되는 CSS

## Props 대신 사용하는 Redux 
  - redux는 props 사용 안하고 하위 컴포넌트가 state를 사용하게 만듬
  - context API와 동일한 역할이지만 데이터 관리가 더 용이

  1. `npm install redux react-redux` 로 설치
  2. index.js에 `import { Provider } from 'react-redux'` 로 첨부
  3. `<Provider>`로 기능 사용할 컴포넌트 감싸기
  4. `let store = createStore()` 로 state 저장
  5. `import { createStore } from 'redux'` 로 첨부
  6. `<Provider store={ store }`로 props 전송
  7. 하위 컴포넌트들이 redux로 전송한 데이터를 사용하려면 해당 컴포넌트에서 `function storeData(){}`로 function 생성
  8. `export default connect(storeData)(Cart)` 로 연결
  9. 연결한 storeData 함수에서 변수로 전달되는 데이터를 받아 props 변환
  10. `{ props.state[0].title }` 처럼 사용

## reducer/dispatch 로 Redux 데이터 수정
  - redux에선 state 데이터의 수정 방법을 미리 정의
  - 대규모 프로젝트에서 필요하지 토이 프로젝트에서는 필요X
  - redux 사용하면 데이터 변경 시 미리 정의해논 방법으로만 수정이 가능하므로 버그 발견 쉬움, 즉 상태관리 용이
   
  1. 데이터 담고 있는 변수 `cartData` 생성
  2. `function reducer(){ return state }` 함수 생성
  3. `reducer( state = cartData, action )` 로 `state`와 `cartData` 연결 
  4. 앞서 사용한 `store`에 `reducer` 를 변수로 전달
  5. `reducer` 함수는 `state`를 `return` 하는 역할을 하는 함수
  6. `reducer` 함수에서 `if`문으로 경우의 수 정의
```javascript
function reducer( state = cartDate, action ){ //reducer 에는 초기값 필수
  if( action.type === 'addNum'){ 
    let tempState = [...state];
    tempState[0].quan++;
    
    return tempState;
  } else {
    return state;
  }
}
```
  7. `dispatch({ type: 'addNum' })`으로 수정 요청

## default parameter 
  - ES6 신문법
  - 파라미터가 전달되지 않았을 때 기본으로 가질 초기값 부여

```javascript
  function F(state = bindingData, action){
    /* state 초기값을 부등호(=)를 사용해 대입*/
  }
```

## state와 reducer가 더 필요할 때
  1. `state` 가 여러 개 필요 시 해당 `reducer`와 해당 초기값 추가로 만들기
  2. `createStore(combineReducers())` 힘수 안에 `{}` 배열 자료형으로 넘기기
  3. 배열 `state` 를 사용하는 컴포넌트의 파일에서 Redux 데이터와 `props` 연결

## dispatch 시 데이터 전달하기
  - `dispatch({ type: 'typeName'; payload : { data1 : 'data'} })` 로 전달