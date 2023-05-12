## 에러처리

- 에러가 발생하지 않는 코드를 작성하는 것은 불가능

* 에러처리를 하는 방법

  1.  if문, 옵셔널체이닝, 단축평가(??, ) 등으로 처리하기
  2.  try-catch문으로 처리하기 = 일반적으로 말하는 에러처리

* try - catch - finally

```js
function a(str) {
  return str.map(Number); // error
}

try {
  console.log(a("try"));
} catch {
  console.log("catch");
} finally {
  console.log("finally");
}
console.log("etc");
```

= 출력순서: catch > finally > etc

## `Error` 객체

- `message` 속성은 에러 메시지를 저장
- `stack` 속성은 에러가 발생한 위치와 호출 스택 정보를 나타내는 문자열로 디버깅 목적으로 사용
  ![[스크린샷 2023-04-20 오후 7.20.18.png]]

- Error 종류
  - Error : 일반적인 에러
  - SyntaxError: JS문법에 맞지 않는 문을 해석할 때 발생
  - ReferenceError: 참조할 수 없는 식별자를 참조했을 때 발생
  - TypeError: 피연산자 또는 인수의 데이터 타입이 유효하지 않을 때 발생
  - RangeError: 숫자값의 허용범위를 벗어났을 때 발생
  - URIError: encodeURI 또는 decodeURI 함수에 부적절한 인수를 전달했을 때 발생
  - EvalError: eval 함수에서 발생

## throw문

```js
//case1
try {
  const error = new Error("error");
  error;
} catch {
  console.log("hi");
}

//case2
try {
  throw new Error("error");
} catch {
  console.log("hi");
}
```

- throw expression
  ![[Pasted image 20230420200442.png]]

```js
try {
  throw 1;
  console.log("a");
} catch {
  console.log("b");
}
// b 출력
```

## 에러의 전파

- 에러는 호출자 방향으로 전파된다.
- 콜 스택의 아래 방향으로 전파된다.

```js
function frontEnd(crew) {
  throw new Error(crew);
}

function techCourse(crew) {
  frontEnd(crew);
}

function woowahan(crew) {
  techCourse(crew);
}

woowahan("sua");
```

![[Pasted image 20230420203159.png]]

## 비동기 에러 처리

```js
function outer() {
  try {
    function inner() {
      setTimeout(() => {
        throw new Error("error");
        console.log("a");
      }, 1000);
    }
    inner();
  } catch {
    console.log("hi");
  }
}
outer();
// 무엇이 출력될까?
```

[예시 구글](https://docs.google.com/presentation/d/16gK8t7hlRvWVDg3wJcYAt0n-OtOpa-Oasf9TLrXMWjg/edit#slide=id.p)
[promise와 에러처리](https://ko.javascript.info/promise-error-handling)

### 처리 방법

- [토스](https://www.youtube.com/watch?v=FvRtoViujGg) - 에러를 잘 다루다는 것 - 성공하는 경우와 실패하는 경우가 분리되어 있는것
  ![[스크린샷 2023-04-21 오후 3.05.39.png]]

* react: [ErrorBoundary](https://jbee.io/react/error-declarative-handling-1/) \* **컴포넌트에서 에러가 발생했을 때 이를 캐치하여 리포팅**하고, **사용자들에게 에러가 발생하여 앱이 중단되는 것이 아닌 다른 대체 화면**을 보여줄 수 있다.

## [에러 메세지 잘 작성하는 법](https://hyeon9mak.github.io/writing-helpful-error-messages/)

- 오류의 원인 식별
  - 유효하지 않은 입력 값이 무엇인지 명확히 안내
  - 시스템의 요구 사항, 제약 사항 안내
- 해결방법 설명
  - 사용자가 문제를 해결하는데 도움이 될 수 있는 적절한 예시 제공
- 명확한 설명
  - 장황하지 않게, 최대한 간결하게. 지나친 간결함은 지양
  - 이중 부정 금지
  - 사용자를 위한 적절한 단어 선택
  - 일관된 용어 사용
  - 확장 문서 링크, 자세히 보기 등을 이용한 오류 메세지 포맷 통일
  - 긍정적인 어조 사용, 불필요한 미안함 금지

## 그 외 여러 에러에 대한 관점

1. 에러의 종류 [출처사이트](https://jbee.io/react/error-declarative-handling-2/)
   ![[Pasted image 20230420211049.png]]
   ![[Pasted image 20230420211657.png]]

custom Error
https://imkh.dev/js-error/
