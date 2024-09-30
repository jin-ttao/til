# Style Component

## context

[공식 문서](https://styled-components.com/)

<br>

## opinion

### 1. 결국 style component도 '컴포넌트'다. 그 특징들을 모두 가지고 있을 것. 가령 매개변수를 받을 수 있다거나.
<br>

### 2. 
<br>

### 3. 

<br>

## research

### 1. styled component으로 '기본'을, css로는 '변화'를.
- styled component로 기본 스타일 지정해주고,
- css로 특정 조건에서의 스타일 지정해주기
- styled component의 prop으로 JS변수를 전달해서, styled component 안에서 css 변화를 줄 수 있음.

```js
// styled component, css를 따로!
import styled, { css } from 'styled-components'

// 결국 Button는 styled.button로 인해 반환된 컴포넌트.
const Button = styled.button<{ $primary?: boolean; }>` 
  background: transparent;
  border-radius: 3px;

// 해석: '아 이 코드들은 $primary 프로퍼티가 설정되면 컴포넌트에 CSS를 추가하고, 이 경우 배경과 색상을 변경하는 거야.'
  ${props =>
    props.$primary &&
    css`
      background: '#BF4F74';
      color: white;
    `};
` // 백틱 유의!
```
<br>

### 2. 유의사항 01. render 하는 JSX 코드 안에 styled component 속성 넣지 마세요!
> *React 컴포넌트의 render 메서드 안에 스타일 컴포넌트를 선언하면 모든 렌더링에서 새 컴포넌트를 동적으로 생성하게 됩니다. 즉, React는 이후 렌더링할 때마다 DOM 하위 트리의 해당 부분을 버리고 다시 계산해야 하며, 그 사이에 변경된 사항의 차이를 계산하는 것이 아니라 그 부분을 삭제하고 다시 계산해야 합니다. 이는 성능 병목 현상과 예측할 수 없는 동작으로 이어집니다.*

> *By declaring a styled component inside the render method of a react component, you are dynamically creating a new component on every render. This means that React will have to discard and re-calculate that part of the DOM subtree on each subsequent render, instead of just calculating the difference of what changed between them. This leads to performance bottlenecks and unpredictable behavior.*
<br>

### 3. 유의사항 02.스타일 컴포넌트를 사용하고 싶은 컴포넌트 마다 일일이 개별 선언 필요하고, 많아지면 가독성 떨어짐.


### 4. 유의사항 03. prop 전달할 때 transient prop으로 전달해야, HTML로 전달하지 않도록 함.
prop이 "transient" prop임을 나타냅니다. 이 접두사가 있는 prop은 styled-component로 전달되지만, 실제 HTML 요소로 전달되지 않습니다.

### 5. 참고자료
[스타일 컴포넌트의 장단점](https://aboveimagine.tistory.com/124)

<br>

# h1

<br>

## context

<br>

## opinion

### 1.
<br>

### 2. 
<br>

### 3. 

<br>

## research

### 1.
<br>

### 2. 
<br>

### 3. 
