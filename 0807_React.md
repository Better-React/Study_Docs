## virtual Dom
- virtual Dom은 어플리케이션 UI를 구성하는 `HTML 엘리먼트`를 메모리 내에서 구현
- 컴포넌트가 다시 렌더링될 때, virtual DOM은 엡데이트 할 요소의 목록을 만들기 위해 기존의 DOM모델에서 변경되는 사항을 비교
- DOM 전체를 다시 렌더링할 필요 없이 실제 dOM에 필요한 최소한 만 변경하여 효율성이 높다.
- 실제 DOM은 새로운 node를 추가하려면 DOM에 해당 node를 추가하여 업데이트 해줘야하며, 만약 이러한 업데이트로 인해 레이아웃 변화가 생기면 웹 페이지 일부 또는 전체가 리렌더링 될 수 있다. (리페인트, 리플로우)


## JSX
-JSX는 HTML처럼 보이는 코드를 작성할 수 있게 해주는 자바스크립트 문법의 확장


## 클래스 컴포넌트
- React 내부 state를 유지하는데 필요한 컴포넌트를 생성하거나 생명주기 메소드를 활용하기 위해 클래스 기반 컴포넌트를 사용했다.
- 클래스 기반 컴포넌트는 리액트의 Component 클래스를 확장하는 ES6 클래스
- 최소한 render() 메서드를 포함해야 한다.
- 렌더링할 결과를 리턴한다.
- props에만 의존하는 UI를 렌더링하는데 선호된다.


## Key는 왜 사용하는가?
- 리액트에서 collection을 렌더링할 때 엘리먼트와 데이터 사이의 관계를 추적하기 쉽도록 반복되는 각 엘리먼트에 key를 추가한다.
- 키는 고유한 ID를 사용해야한다.
- 키를 사용하지 않으면 collection을 추가하거나 제거할 때 예상치 못한 결과가 발생할 수 있다.


## `state` vs `props`
- state는 component 내에서 읽고, 쓰기 가능 // props 는 읽기 전용


## state
- state를 변경하기 위해 setState 메서드를 사용한다.
- setState 메서드가 실행되면 변경 대상 컴포넌트르 등록하고 virtualDOM갱신하는 배치가 처리된다.
- setState 메서드가 샐행되면 해당 컴포넌트의 shouldComponentUpdate 함수를 실행한다. 그리고 이 함수가 true를 반환하면 render 함수를 실행한다.
- 상태가 변한 컴포넌트를 루트 노드로 해서 깊이 우선 탐색 방식으로 각 자식 컴포넌트의 shouldComponentUpdate 함수와 render 함수를 실행한다. 이렇게 render 함수를 실행하여 얻은 새로운 Virtual DOM을 실제 DOM과 동기화되어 있는 기존 Virtual DOM과 비교해서 변경 사항을 파악한다(reconcilation). 그리고 실제로 변경된 부분만 DOM API를 호출하여 DOM에 반영하면, 브라우저가 변경 사항이 반영된 DOM과 CSSOM으로 새로운 Render Tree를 생성해서 화면을 다시 그린다.


## prop drilling
- prop drilling: 부모 컴포넌트에서 하위 컴포넌트로 데이터를 전달 할 때 props를 전달하는 것 외에 props를 팔요로하지 않는 다른 컴포넌트를 통해 내려주게 되는 것
- 컴포넌트를 리팩토링해, state를 가장 가까운 부모 컴포넌트와만 공유함으로서 회피한다. 너무 멀리 떨어진 경우는 React의 Context API, Redux를 이용한다.


## Redux
- React를 위한 써드파티 state 관리 라이브러리
- state 업데이트는 reducer를 통해 전달되는 store에 action을 보내는 것이다.
- reducer는 action과 현재의 state를 받고, 새로운 state를 반환하고, 구독된 컴포넌트를 다시 렌더링한다.


## 제어 컴포넌트와 비제어 컴포넌트의 차이
- form element는 고유한 state를 유지한다.
- 비제어 컴포넌트는 DOM을 이러한 input들의 state에 대한 진짜 근원을 추적하기 위해 사용된다.
- input 값이 변경되면 리액트는 input을 다시 렌더링한다.


## 생명주기 메서드
- 클래스 기반 컴포넌트는 mount, update, unmount등의 생명주기 특정 시점에 호출되는 특별한 메소드를 선언할 수 있다.
- 컴포넌트가 필요한 셋팅을 헤제하거나 타이머를 설정하거나 브라우저 이벤트에 바인딩 할 때

- componentWillMount: 컴포넌트가 생성된 후 DOM에 렌더링되기 전에 호출됩니다.
- componentDidMount: 처음으로 렌더링이 끝나고 컴포넌트의 DOM 엘리먼트가 사용 가능할 때 호출됩니다.
- componentWillReceiveProps: props가 업데이트 될 때 호출됩니다.
- shouldComponentUpdate: 새로운 props를 받았을 때 호출되며, 성능 최적화를 위해 리랜더링을 막을 수 있습니다.
- componentWillUpdate: 새로운 props를 받았고 shouldComponentUpdate가 true를 리턴할 때 호출됩니다.
- componentDidUpdate: 컴포넌트가 업데이트된 후에 호출됩니다.
- componentWillUnmount: 컴포넌트가 DOM에서 제거되기 전에 호출되어 이벤트리스너 등을 정리할 수 있게 해줍니다.


## HOC
- 컴포넌트 로직을 재사용하기 위한 기술
- 컴포넌트를 받아 컴포넌트를 반환함

## FLUX 설명
- 프론트엔드에서 적용된 MVC 패턴에 대한 문제로 나온 패턴
( 양방향, 규모가 클수록 데이터가 어떻게 변경되는지 추적하기 어렵고 많은 Model을 전부 제어하는 것도 어려워짐)
- 단방향 데이터 흐름 모델의 개념을 따르는 아키텍쳐
- Action => controller => Model 변경/ view 변경

## Redux의 3가지 원칙
- Single source of truth(하나의 진실): redux는 애플리케이션 상태를 한 곳에서 관리하기 위해 단 한 개의 store를 사용
- state is ReadOnly(상태는 읽기 전용): view에서 state를 직접 접근하여 변경할 수 없다.
- Changes are made with Pure Functions ( 변화는 순수 함수로 만들어져야한다. ): reducer는 순수 함수로만 되어야 한다.
