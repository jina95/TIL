# React 에서 왜 복사를 해서 값을 리턴해야 하는가 ?

- 알아봐야 할 키워드 → 내부 hook 구조 때문 , value type, reference type, shallow & deep copy

### Shallow copy | Deep copy

- 얕은복사와 깊은 복사인데, 얕은 복사는 원본을 참조하는것이라 실제로 복사라기 보다는 복사한 값을 수정했을때 원본값과 복사값 둘다 변경되는 불상사가 일어난다!!!!!
    - 얕은 복사( 언뜻 1차원에서는 깊은복사처럼 보이지만 2차원 에서는 얕은복사임을 확인할 수 있다.) : Object.assign(), Spread Operator , 할당( ' = ')

        ```tsx
        const obj = {
          a: 1 ,
          b: {
            c: 2
          }
        }

        const assignObj = Object.assign({}, obj)
        const spreadObj = { ...obj }

        obj.b.c = 3 
        console.log(assignObj) // { a: 1, b: { c : 3 }}
        console.log(spreadObj) // { a: 1, b: { c : 3 }}
        ```

    - 깊은 복사 ( 전부 복사해서 새 주소에 담기 때문에 참조를 공유하지 않는다): lodash → deepClone, JSON.parse(JSON.stringify) → 단 성능적으로 좋지 못하고, 복사하는 객체 속성중에 값이 함수이거나 undefined 일때는 완전한 복사를 하지 못함, 커스텀 함수 생성

### State 의 Immutability (불변성)

- 불변성이란 어떠한 값을 직접 변경하지 않고 새로운 값을 만들어내는 것
- 필요한 값을 변형해서 사용하고 싶다면, 어떠한 값의 사본을 만들어서 사용해야만 함
- 이유 :

    ### 이전 state 와 바뀐 state 를 구분하는 방법이 참조값이 바뀌었는지 확인하기때문이다!

    [state.name](http://state.name) = [action.payload.name](http://action.payload.name) 이런식으로 직접적으로 바꾸게 된다면 참조값이 변하지 않기때문에 값이 바뀌었다고 인지하지 못하고 리렌더링 되지 않는다.

    즉 state 를 바꾸고 돔을 다시 만들려면 새로운객체, 배열을 만들어 새로운 참조값을 만들고 react 에게 이 값은 이전값과 다른 참조값임을 알려야만 한다. 

### React 의 기본속성으로 얕은 비교를 통해 새로운 값인지 아닌지를 판단 후 새로운 값이라면 리렌더링 한다.

- 얕은비교를 통해서 → 참조가 동일한지 아닌지를 확인한다 .
- 즉 새로운 참조 값일때만 리렌더링된다.

## 즉 우리가 state 를 변경할때 깊은복사를 해야하는 이유는, 값이 변경됨을 react 에게 알려줘야하는데, 참조값이 동일한 얕은복사를 하게되면 react 가 알지 못하기 때문이다.  불변성이란 새로운 참조를 만들어내는 것이기 때문!