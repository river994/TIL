# CH4 - 함수와 프로토타입 체이닝

## 4.5 프로토타입 체이닝
### 4.5.1 프로토타입의 두 가지 의미
  - 프로토타입 기반의 객체지향 프로그래밍
  - 모든 객체는 프로토타입 객체를 가리키는 참조 링크 형태 프로퍼티, 암묵적 프로토타입 링크를 가짐 = [[Prototype]]링크
### 4.5.2 객체 리터럴 방식으로 생성된 객체의 프로토타입 체이닝
  - 프로토타입 체이닝으로 프로토타입 객체 프로퍼티 접근 가능
  - 프로토타입 체이닝이란 해당 객체에 접근하려는 것이 없다면 [[Prototype]]링크 따라 차례대로 검색 하는 것

### 4.5.3 생성자 함수로 생성된 객체의 프로토타입 체이닝
  - 객체 리터럴 방식과 생성자 함수 생성된 객체는 프로토타입 체이닝에 있어서 차이
  - *모든 객체는 생성자 함수의 prototype 프로퍼티가 가리키는 객체를 자신의 프로토 타입 객체로 취급*

### 4.5.4 프로토타입 체이닝의 종점
  - Object.prototype 객체는 프로토타입 체이닝의 종점
  - 객체 리터럴 방식 
      + [[Prototype]] -> Object.prototype
  - 생성자 함수 방식
      + [[Prototype]] -> 생성자 함수 -> [[Prototype]] -> Object.prototype

### 4.5.5 기본 데이터 타입 확장
  - 기본 내장 프로토타입 객체 프로토타입 -> Object.prototype
  - 표준 빌트인 프로토타입 객체에도 직접 메서드 추가 가능

### 4.5.6 프로토타입도 자바스크립트 객체다
  - 동적으로 프로퍼티 추가/삭제 가능

### 4.5.7 프로토타입 메서드와 this 바인딩
  - 메서드 호출 객체에 this 바인딩

### 4.5.8 디폴트 프로토타입은 다른 객체로 변경이 가능하다
  - 디폴트 프로토타입 객체 다른 일반 객체로 변경 가능
  - 생성자 함수 프로토 타입 객체 변경
      + *이후 생성된 객체*들은 변경된 프로토타입 객체로 [[Prototype]] 링크 연결
      + *이전 생성된 객체*들은 기존 프로토타입 객체로 [[Prototype]] 링크 유지

### 4.5.9 객체의 프로퍼티 읽기나 메서드를 실행할 때만 프로토타입 체이닝이 동작한다