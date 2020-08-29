# Svelte 입문 강의 - A부터 Z까지 💻 

## 2️⃣
### 🖥 Props
#### 3 - 1. 정의 방법

```javascript
// 부모 컴포넌트
<script>
import Child from './Child.svelte'
</script>

<Child test="JJ입니다." />

// 자식 컴포넌트
<script>
export let test;
</script>

<p>{test}</p>

// 부모컴포넌트에서 자식 컴포넌트로 props 전달이 가능하다
```

- svelte에서 export 는 부모컴포넌트 -> 자식컴포넌트로 값을 전달받았다 라는 의미로 사용

#### 3 - 2. 기본값 설정
- props 의 기본값을 설정해 주지 않으면 , undefined 라는 값이 출력 된다.

```javascript
// 부모 컴포넌트
<script>
import Child from './Child.svelte'
</script>

<Child name="JJ"></Child>
<Child></Child>

//자식 컴포넌트
<script>
export let name = "nope";
</script>

<p>이름은 {name} 입니다</p>
```

- 만약 위에서 'export let name' 이었다면, undefined 라는 값이 출력되지만 
- 위와 같이 기본값을 설정한다면 출력되는 값은 아래와 같다

<pre><code>이름은 JJ 입니다
이름은 nope 입니다</code></pre>

#### 3 - 3. Spread 문법 사용하기
- Spread : 펼치기
- props 에 spread 문법을 사용하면 많은 양의 props를 하위 컴포넌트로 전달해야할때 코드양을 줄일 수 있는 장점이 있다.

```javascript
// 부모 컴포넌트
<script>
	import Child from './Child.svelte'

	let name = "jj";
	let job = "developer"
	let website = "https://jina95.github.io/"
</script>

<Child {name} {job} {website}></Child>

// 자식 컴포넌트
<script>
export let name;
export let job;
export let website;
</script>

<p>{name}, {job}, {website}</p>
```

- name = {name} 해야하지만(속성이름 = {변수이름}), 속성이름과 변수이름이 동일할때는 생략 가능 !

> <Child name = {name} {job} {website}></Child>

- 스프레드 방식으로 바꾼다면 부모컴포넌트를 아래와 같이 바꿀 수 있다.

```javascript
// 부모 컴포넌트
<script>
    import Child from './Child.svelte'
    let info = {
		name : "jj",
		job : "developer",
		website : "https://jina95.github.io/"
	}
</script>

<Child {...info}></Child>
```


### 🖥 논리 블록
#### 4 - 1. 조건문 블록
- svelte 에서 if 문을 사용할때는 {#if}, {:else} 를 사용한다 
- 모든 조건문이 끝났을때는 {/if} 로 마무리 해준다.

```javascript
{#if x > 10}
	<p>{x}는 10보다 큽니다</p>
{:else if x > 5}
	<p>{x}는 5보다 큽니다</p>
{:else}
	<p>{x}는 5보다 작습니다</p>
{/if}
```

#### 4 - 2. 반복문 블록
- 반복문은 이용할때는 {#each 리스트 as item} , 닫을때는 {/each}
- 반복문 인덱스를 이용할때는 {#each 리스트 as item, i}


```javascript
<script>
	let list = [
		{id: 1, text: 'test 1'},
		{id: 2, text: 'test 2'},
		{id: 3, text: 'test 3'},
	]
</script>


<ul>
	{#each list as item, i}
	<li>{i}: {item.id}, {item.text}</li>
	{/each}
</ul>

// 구조문법을 이용해서 아래와 같이 나타낼수도있다.
<ul>
	{#each list as {id, text}, i}
	<li>{i}: {id}, {text}</li>
	{/each}
</ul>
```

#### 4 - 3. 반복문 블록에 Key 지정하기

```javascript
<script>
	let list = [
		{id: 1, text: 'test 1'},
		{id: 2, text: 'test 2'},
		{id: 3, text: 'test 3'},
	]

	function addItem(){
		const id = Math.max(...list.map(x => x.id)) + 1;
		list = [...list, {id, text: `test${id}`}];
	}

	function removeItem(){
		list.shift();
		list = list;
	}

	function resetItem(){
		list = [
			{ id: 1, text: 'test 1' },
			{ id: 2, text: 'test 2' },
			{ id: 3, text: 'test 3' },
		]
	}
</script>

<button on:click={ addItem }>Add</button>
<button on:click={ removeItem }>Remove</button>
<button on:click={ resetItem }>Reset</button>

<ul>
	{#each list as item (item.id)}
	<li>{item.id}, {item.text}</li>
	{/each}
</ul>
```

- (id) key값을 주는것
- key값 없이 리스트를 삭제하다보면 전체를 업데이트를 해서 비효율적
- 해당하는 id 만 지우려면, key값을 지정해주면 된다.
- key 값에 객체도 올 수 있다. 하지만 key값은 스트링이나 넘버가 좋다! 

#### 4 - 4. await 블록
- {#await 프로미스객체} {:then data} {:catch error} 닫을때는 {/await}
- await 와 then 사이에는 응답이 올때까지 출력하는 html
- then 과 catch 사이는 응답결과를 출력

```javascript
<script>
	let promise;
	function sayHello(){
		return new Promise((resolve,reject) => {
			setTimeout(()=> {
				// resolve('Hello World');
				reject(new Error('에러발생!'))
			}, 1000)
		})
	}
	function handleClick(){
		promise = sayHello();
	}
</script>


<button on:click={handleClick}>인사하기</button>

{#await promise}
	<p>인사를 기다리는 중...</p>
{:then data}
	<p>{data}</p>
{:catch error}
	<p>{error.message}</p>
{/await}
```

- then 을 아래와 같이 생략 할 수도 있다.

```javascript
{#await promise then data}
	<p>{data}</p>
{/await}
```

- 위와 같이 생략하면, 응답을 기다리는 중에는 아무것도 뜨지 않는다 ( 공백 )



### 🖥 이벤트 다루기
#### 5 - 1. DOM 이벤트
- svelte 에서는 모든 DOM 이벤트가 가능해서 on:이벤트이름 을 적어주면 모든 이벤트 처리 가능하다.

```javascript
<script>
	let m = { x:0, y:0}
	let isEnter = false;
	function handleMousemove(event){
		m.x = event.clientX;
		m.y = event.clientY;
	}

	function handleMouseenter() {
		isEnter = true;
	}

	function handleMouseleave(){
		isEnter = false;
	}
</script>


<div on:mousemove={handleMousemove}>
	마우스 위치 : {m.x}, {m.y}
	<div 
		on:mouseenter={handleMouseenter}
		on:mouseleave={handleMouseleave}
		>
		{ isEnter ? 'Enter' : 'Leave'}
	</div>
</div>


<style>
	div {
		width: 100%;
		height: 100%;
	}
	div > div {
		width: 100px;
		height: 100px;
		background-color: yellow;
	}
</style>
```

#### 5 - 2. 인라인 핸들러

```javascript
<script>
	let m = { x:0, y:0}
</script>

<div on:mousemove={e => m = {x : e.clientX, y: e.clientY}}>
	마우스 위치 : {m.x}, {m.y}
</div>
```

- 인라인핸들러는 첫번째 인자의 돔이벤트이기 때문에 e 객체가 올것 
- 스벨트는 컴파일되면서 최적화 되기때문에 인라인핸들러 가능 ( 몇 프레임워크는 인라인핸들러가 성능상의 문제로 불가)

#### 5 - 3. 이벤트 수식어
- preventDefault() 이벤트 수식어
- on:돔이벤트 | 이벤트수식어 = {} ex(on:click|once={handleClick})
- once : 클릭이벤트가 한번만 일어남을 명시

```javascript
<script>
	function handleClick(){
		alert('CLICK')
	}
</script>

<button on:click|once={handleClick}>
	Click
</button>
```

<pre><code>preventDefault: 이벤트 핸들러가 실행되기 전 event.preventDefault()를 호출합니다. 태그의 기본 동작을 막는 이벤트 수식어입니다.
stopPropagation: event.stopPropagation()이 호출됩니다. 이벤트가 다음 요소로 흐르는 것을 막는 이벤트 수식어입니다.
passive: 터치 혹은 휠 이벤트로 발생하는 스크롤 성능을 향상시키는 이벤트 수식어입니다. Svelte는 안전한 곳(?)에 자동으로 추가합니다.
capture: 버블링 단계가 아닌 캡처 단계에서 이벤트 핸들러를 실행합니다.
once: 이벤트 핸들러를 단 한 번만 실행하도록 하는 이벤트 수식어입니다.
self: event.target과 이벤트 핸들러를 정의한 요소가 같을 때 이벤트 핸들러를 실행하도록 하는 이벤트 수식어입니다.

위의 이벤트 수식어를 on:click|once|capture={...}와 같이 체인(chain)으로 연결해 여러 개를 정의할 수도 있습니다
</code></pre>

- 참고사이트 : [svelte 이벤트다루기](https://beomy.github.io/tech/svelte/events/)

#### 5 - 4. 컴포넌트 이벤트

```javascript
// 부모 컴포넌트
<script>
import Child from './Child.svelte'

function handleMessage(event){
	alert(event.detail.text)
}
</script>

<Child on:message={handleMessage}></Child>

// 자식 컴포넌트
<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher();

    function sayHello(){
        dispatch('message', {
            text: 'hello!'
        });
    }
</script>

<button on:click={sayHello}>Click</button>
```

- createEventDispatcher 를 이용해서 이벤트를 상위 컴포넌트로 전달
- event.detail / detail 이라는 옵션 안에 자식컴포넌트에서 전달받은 값이 담겨 오게 된다.
- svelte 는 자식 -> 상위 이벤트 전달할때 자체적으로 CustomEvent() 생성자를 생성해서 이벤트 전달
- 참고사이트 : [CustomEvent()](https://developer.mozilla.org/ko/docs/Web/API/CustomEvent/CustomEvent)

#### 5 - 5. 컴포넌트 이벤트 발생시 주의사항
- dispatch 함수는 항상 최상위 스코프에 존재해야 함 ( ex sayhello 함수 안에 정의 되어서 사용되면 동작이 제대로 하지 X)
- 컴포넌트 이벤트는 돔이벤트와 달리 이벤트가 버블되지 않는다
- 하위에서 상위컴포넌트로 자동으로 전달되지 않는다. (그래서 하위에서 상위로 올리기 위해 dispatch를 이용한것)

```javascript
// 추가된 컴포넌트
<script>
    import Child from './Child.svelte'
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher();

    function handleMessage(event) {
        dispatch('message', event.detail.text)
    }
</script>

<Child on:message={handleMessage}/>
// 하지만 아래와 같이 수정해도 가능하다고 하는데, 내가 했을땐 뭔가 잘 안됬다..

<script>
    import Child from './Child.svelte'
</script>

<Child on:message/>
```