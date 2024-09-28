# JSX 내부에서 자바스크립트 '표현식(expression)'만 사용 가능한 이유

<br>

## Opinion

### 표현식이 값을 반환하는 건 알겠다, JSX에는 왜 값만 있어야 할까?: React는 주문만 받고 요리는 하지 않는 ‘웨이터’. 
- 개발자에게든, 사용자에게든 주문(value, event)을 받기만 하고 직접 지지고 볶고(연산, statement) 하지 않음. 여기서 받은 대로 저기로 전하기만 할 뿐임. 
- 추가로 정리할 부분
  - JSX 가 품을 수 있는 ‘값’의 정의
  - JSX에는 왜 ‘값’이나 ‘값으로 표현되는 표현식’만 있을 수 있을지.
  - HTML 태그, 함수 객체도 모두 ‘값’의 일종인가
  - JSX 내부에 자바스크립트 statement 코드가 있으면 내부적으로 어떻게 되는지.

<br>

## Learned

### 결론
- JSX는 마크업을 위해 결국 HTML '값'을 반환해야 함.
- 그 자체로 '값'으로 볼 수 있는 코드(표현식)를 JSX는 그나마 유연하게 허용해줌.

<br>

### Statement(문) vs Expression(표현식) 차이
- "A statement does something. An expression evaluates to a value.": 작업 수행하는 코드 vs 값을 내는 코드

<details>
<summary>(참고) expression은 statement의 일부</summary>
<div markdown="1">

- expression들은 평가(evaluate)가 가능해서 하나의 ‘값’으로 환원된다
- statement는 ‘진술’, ‘서술’의 의미로 프로그래밍에서는 실행가능한(executable) 최소의 독립적인 코드 조각.
  - statement는 흔히 한 개 이상의 expression과 프로그래밍 키워드를 포함하는 경우가 많다.

</div>
</details>

<br>
  
### JSX “마크업 하고 싶어! (HTML 반환하고 싶음)”

- 결국 JSX는 마크업을 위한 수단이므로, JSX 코드를 실행하면, **결과로 'HTML'이 남아야 함.**
- 핵심은 HTML Node의 '값(value)'을 반환하는 것.
- JS가 데이터 타입 등 유연하듯, JSX도 유연한 부분이 있는데 바로 '값(value)을 결정할 수만 있는 코드면 허용' 해준다는 것임.
  - 표현식은 JSX의 목표인 '값을 결정'하는 데에 도움을 주기 때문.
- 참고
  - Stack Overflow Why can you only use expressions in JSX, not statements? [링크](https://stackoverflow.com/questions/60988649/why-can-you-only-use-expressions-in-jsx-not-statements)
  - JSX를 ‘Javascript Syntax eXtension’ 혹은 ‘JavaScript to XML’ 의 약자로 보는 시선도 있음.

<br>

### (반론) 중간에만 조건문 쓰고, 결과적으로 값만 반환할 수 있으면 안돼요?
- (읽기는 할까?)
- 예시: if 조건문 vs 삼항 연산자 차이
```js
// 반환 값이 없음
if(value){
   변수 = 10;
} else {
   변수 = 7;
}
```

```js
// 반환 값이 있음. 이 자체가 '값'임.
변수 = value === true ? 10 : 7;
```

<br>

### (망가뜨려보기) JSX 내부에 표현식이 아닌 것을 쓰면?
- statement(문)을 쓰면? (if 조건문, for 반복문 등)

<br>

### JSX 안에서 statement를 못 쓴다고 React에서 조건문, 반복문 등을 활용하지 못하는 거 아님.

- 가령 조건부 렌더링을 구현할 때 삼항연산자, map() 메소드로 충분하지 않을 수 있음.
- 이때는 jsx 바깥에서 js 문법으로 연산 하고 결과(값)를 jsx에 가져와서 쓰면 됨.
    
  ```jsx
  let 버튼; 
  if (value) { 
    버튼 = <LogoutButton />; 
  } else { 
    버튼 = <LoginButton />; 
  } 
  
  return ( 
    <nav> 
      <Home /> 
      {버튼} 
    </nav> 
  );
  ```

- 혹은 즉시 실행 함수로. (권장하는 방식인지 체크 필요)
  ```jsx
  return (
    <section>
      <h1>Color</h1>
      <p>{this.state.color || "white"}</p>
      <p>
        {(() => {
          switch (this.state.color) {
            case "red":   return "#FF0000";
            case "green": return "#00FF00";
            case "blue":  return "#0000FF";
            default:      return "#FFFFFF";
          }
        })()}
      </p>
    </section>
  );
  ```

