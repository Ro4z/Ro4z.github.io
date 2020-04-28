
> React Hook이란 무엇인가?

## React Hook의 등장
한마디로 표현하자면 class 형태의 React Component의 방식을 대체하는 방식입니다.

기존에 Class기반의 Component는 재사용을 위해 [render props](https://ko.reactjs.org/docs/render-props.html#gatsby-focus-wrapper) 그리고 [HOC(higher-order components)](https://ko.reactjs.org/docs/higher-order-components.html#gatsby-focus-wrapper)방식을 택하였습니다.

이는 곧 wrapper 지옥을 불러오기 때문에, **계층 변화 없이 상태 관련 로직을 재사용할 수 있도록** 도와주는 기능이 필요했습니다.
또한 API 호출, 이벤트 등록도 하는 복잡한 Component가 있다고 가정했을 때, 여러 로직이 componentWillUnmount, componentDidMount와 같은 생명주기 함수에 흩어지게 됩니다.

로직을 분리하면서도 wrapper 지옥을 피하며, React 생명주기 함수에 종속적이지 않도록 하는 코딩 방법을 제시한 것이 
바로 Hook 입니다.

## React Hook의 사용

Hook은 한마디로 class 없이 state 값과 여러 React 기능을 이용하는 것입니다.
즉, 기존 constructor, componentWillMount 같은 메소드에서 벗어나 오로지 render() 단계에 해당하는 로직에 집중하면 됩니다.

setState는 useState, React 생명주기에 해당하는 로직들은 useEffect를 이용하여 hook 할 수 있습니다.
useEffect는 기존 생명주기 함수인 componentDidMount, componentDidUpdate, componentWillUnmount를 합쳐놓은 것에 해당합니다.
이름이 useEffect인 이유는 주로 data를 fetch하는 등의 작업들이 side effect에 해당하기 때문이라고 합니다.

예를 들어, 기존에 아래와 같은 방식으로 구현이 됐다면,
<script src="https://gist.github.com/Ro4z/6b66ba8aa77e1d27e2d63dec1206ebb1.js"></script>

useEffect를 이용하여 다음과 같이 조금 더 간결하게 구현할 수 있는 것입니다.
<script src="https://gist.github.com/Ro4z/f074914c800dbb1ac4e4dd0ad077d0c0.js"></script>

useEffect에 넘겨준 effect는 render할 때 마다 매번 호출되게 되는데,
```function useEffect(effect: EffectCallback, inputs?: InputIdentityList)```
두 번째 파라미터인 input으로 특정 state가 변경된 경우에만 effect가 실행되게 지정할 수 있습니다.
예를 들어, ```useEffect(() => func(), [count]);```와 같이 쓴다면 count state가 변경될 때만 실행됩니다.

마지막으로 useEffect에서의 componentDidUnmount는 어떻게 처리되는지 알아봅시다.
<script src="https://gist.github.com/Ro4z/912b83bd6e11aca783e6b75460a16f0a.js"></script>
이와 같이 useEffect 인자로 넘겨주는 effect 함수에 return 값이 존재하는 경우, hook의 cleanup 함수로 인식하고 다음 effect가 실행되기 전에 실행해줍니다.


useState, useEffect 밖에도 직접 hook을 custom할 수 있다고 하는데, 오픈 소스들을 참고해보며 hook을 더 확실히 이해해야 할것 같습니다.



