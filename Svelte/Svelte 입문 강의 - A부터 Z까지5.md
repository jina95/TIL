# Svelte 입문 강의 - A부터 Z까지 💻 

## 5️⃣
### 🖥 애니메이션
#### 12 - 1. 애니메이션 사용하기
- animate 라는 디렉티브를 제공
- flip : delay, easing, duration

```javascript
// src/App.svelte
<script>
	import { flip } from 'svelte/animate'

	let items = [1];
	function addItem(){
		items.unshift(Math.max(...items) + 1);
		items = items;
	}

	function removeItem(){
		items.shift();
		items = items;
	}
</script>

<button on:click={addItem}>add</button>
<button on:click={removeItem}>remove</button>

{#each items as item (item)}
	<p animate:flip={{delay:1000, duration:2000}}>{item}</p>
{/each}
```

#### 12 - 2. 커스텀 애니메이션
- 애니메이션은 3개의 파라미터 값을 가짐 
-   `node`: 첫 번째 파라미터는 애니메이션이 적용되는 HTML 요소입니다.
-   `{ from: DOMRect, to: DOMRect }`: 두 번째 파라미터는 애니메이션을 시작될 때의 정보  `from`과 애니메이션이 끝날 때의 정보  `to`를 속성으로 가지는 객체입니다.
    -   `DOMRect`: 애니메이션이 적용되는 요소의 위치 크기 등의 정보를 가지는 객체입니다.
-   `params`: 세 번째 파라미터는  `animate:애니메이션 이름={params}`의  `params`로 전달될 값입니다. 모든 형태의 값을 전달할 수 있습니다.

```
animation = (node: HTMLElement, { from: DOMRect, to: DOMRect } , params: any) => {
  delay?: number,
  duration?: number,
  easing?: (t: number) => number,
  css?: (t: number, u: number) => string,
  tick?: (t: number, u: number) => void
}

```

```
DOMRect {
  bottom: number,
  height: number,
  ​​left: number,
  right: number,
  ​top: number,
  width: number,
  x: number,
  y: number
}
```

- 애니메이션은 객체를 리턴해야 함
-   `delay`: 단위는 ms로 설정한 시간이 지난 후에 애니메이션을 시작합니다.
-   `duration`: 단위는 ms로 설정한 시간 동안 애니메이션이 동작합니다.
-   `easing`:  `p => t`  형태의 easing 함수입니다.  [https://svelte.dev/docs#svelte_easing](https://svelte.dev/docs#svelte_easing)  참고 바랍니다.
-   `css`:  `(t, u) => css`  함수입니다.  `t`는 0 ~ 1 사이의 값이고,  `u`는  `u === 1 - t`입니다. 요소가 추가될 때  `t`는 0에서 1로 증가하고, 요소가 제거될 때  `t`는 1에서 0으로 감소합니다.  `t`(혹은  `u`)의 변화에 따른 CSS 문자열을 리턴해야 합니다.
-   `tick`:  `(t, u) => {...}`  함수입니다. 매 tick마다 호출되는 콜백 함수입니다.

#### 12 - 3. 애니메이션 사용시 주의사항
- each 반복문에서 key값 필수 ! : animate 부분에 빨간줄 표시!
- 배열이 재정렬 될때 애니메이션이 트리거 되기때문에 주의해서 사용할 것

> 기존 unshift 일때는 제거될때도 애니메이션이 동작했지만, pop 을 이용했더니 제거될때 애니메이션이 먹지 않는다..!
> 여기서 트리거란 ? 트리거(Trigger)란 영어로 방아쇠라는 뜻인데, 방아쇠를 당기면 그로 인해 총기 내부에서 알아서 일련의 작업을 실행하고 총알이 날아갑니다. 이처럼 데이터베이스에서도 트리거(Trigger)는 특정 테이블에 INSERT, DELETE, UPDATE 같은 DML 문이 수행되었을 때, 데이터베이스에서 자동으로 동작하도록 작성된 프로그램입니다. 즉! 사용자가 직접 호출하는 것이 아니라, 데이터베이스에서 자동적으로 호출하는 것이 가장 큰 특징입니다. 
> 출처 : https://limkydev.tistory.com/154

- 반복문 animate 디랙티브가 직계자손에서 사용해야 한다. > div로 한번더 감싸게 되면 빨간줄뜬다!

### 🖥 액션
#### 13 - 1. 액션 만들기
- 커스텀 디렉티브를 만든다 ( 액션은 트렌지션, 애니메이션과 같은 동작이다. )

```
action = (node: HTMLElement, parameters: any) => {
  update?: (parameters: any) => void,
  destroy?: () => void
}
```

- 파라미터 : 첫번째 파라미터는 액션이 선언된 요소, 두번째는 use:액션 이름={parameters}로 전달되는 parameters
- 리턴값 : update, destroy 속성을 가진 객체를 리턴 / update, destroy 은 액션의 라이프사이클 함수
- update: 돔이 마운트 된 후 파라미터가 변경 될때마다 호출되는 라이플 사이클 함수
- destroy : 액션이 선언된 돔이 제거될때 호출되는 함수
- mount : 액션함수의 선언부분이 마운티드 됬을때 호출되는 부분 

```javascript
// src/App.svelte
<script>
	function longpress( node, duration){
		let timer;

		function handleMouseDown(){
			timer = setTimeout(()=>{
				node.dispatchEvent(new CustomEvent('longpress'))
			}, duration)
		}

		function handleMouseUp(){
			clearTimeout(timer)
		}

		node.addEventListener('mouseDown', handleMouseDown)
		node.addEventListener('mouseUp', handleMouseUp)
		// longpress 액션이 정의된 html 요소가 mount 됬을때 호출되는 부분 

		return {
			update(newValue){
				duration = newValue
			},
			destroy(){
				node.removeEventListener('mouseDown', handleMouseDown)
				node.removeEventListener('mouseUp', handleMouseUp)
			}
		}
	}
	let duration = 200;

	function handleLongpress(){
		alert('longpress')
	}
</script>

<input type="range" bind:value={duration} min='100' max="2000">

<button 
	use:longpress={duration}
	on:longpress={handleLongpress}
	>
	Click
</button>
```

### 🖥 Slot
#### 14 - 1. Slot 사용하기
- 슬롯을 사용하면 컴포넌트에 자식요소를 추가할 수 있다.

```javascript
// src/Box.svelte
<div class="box">
    <slot></slot>
</div>

// src/App.svelte
<script>
	import Box from './Box.svelte'
</script>

<Box>
	<!-- box컴포넌트 안에 slot을 넣어줬기 때문에, 자식컴포넌트를 가질 수 있게 된다. -->
	<h1>Box component</h1>
	<p>Hello</p>
</Box>
```

#### 14 - 2. Default Slot
- slot 태그를 사용했지만, 자식요소를 정의해주지 않으면 Default Slot이 보여지게 된다.

```javascript
// src/Box.svelte
<div class="box">
    <slot>
        <p>값이 없습니다!</p>
    </slot>
</div>

// src/App.svelte
<script>
	import Box from './Box.svelte'
</script>

<Box></Box>
```

- 위와 같은 상황일때 slot에 정해놓은 값이없습니다 라는 텍스트가 화면에 찍힌다. -> Default Slot

#### 14 - 3. Named Slot
- 컴포넌트 자식요소를 특정 위치에 위치시킬 수 있다

```javascript
// src/Box.svelte
<div>
    <slot name="title"></slot>
    <slot name="content"></slot>
    <slot name="detail"></slot>
</div>

// src/App.svelte
<script>
	import Box from './Box.svelte'
</script>

<Box>
	<p slot="title">title</p>
	<p slot="content">content</p>
	<p slot="detail">detail</p>
</Box>

<Box>
	<p slot="content">content</p>
	<p slot="detail">detail</p>
	<p slot="title">title</p>
</Box>

<!--  이렇게 순서를 섞어도, 출력 결과물은 같다. 이유는 box component에서 정한 위치값이 있기때문에, 기준이 box component이 된다. -->
```

#### 14 - 4. Slot props

```javascript
// src/Hoverable.svelte
<script>
    let hovering;
    function enter (){
        hovering = true;
    }
    function leave (){
        hovering = false;
    }

</script>

<div 
    on:mouseenter={enter}
    on:mouseleave={leave}
> 
    <slot hovering={hovering}></slot>
</div>

// src/App.svelte
<script>
	import Hoverable from './Hoverable.svelte'
</script>

<Hoverable let:hovering={active}>
	<!-- actvie라는 변수가 정의되어있지 않음을 확인할 수 있는데, 해당 태그 안에서만 사용 할 수 있다. -->
	<!-- 그렇기 때문에  Hoverable 태그가 또 있다고 하더라도, active는 독립적이다. -->
	<div class:active>
		{#if active}
		<p>active가 활성화 되었습니다.</p>
		{:else}
		<p>active가 비활성화 되었습니다.</p>
		{/if}
	</div>
</Hoverable>

<style>
	div {
		padding: 1em;
		background-color: #eee;
	}
	.active {
		background-color: hotpink;
		color: white;
	}
</style>
```

### 🖥 Context API
#### 15 - 1. Context 사용하기
- Context를 사용하면 컴포넌트와 자식컴포넌트끼리 데이터 공유가 가능해 진다.

```javascript
// src/context.js
const key = {}

export {
    key
}

// src/Box.svelte
<script>
    import { key } from './context.js'
    import { setContext } from 'svelte'

    const context = {
        name: 'Bill',
        job: 'actor',
        age: 30
    }

    setContext(key, {
        context
    })
</script>

<div>
    <slot></slot>
</div>

// src/Child.svelte
<script>
    import { key } from './context.js'
    import { getContext } from 'svelte'

    const { context } = getContext(key);
</script>

<p>{context.name}</p>
<p>{context.job}</p>
<p>{context.age}</p>

//src/App.svelte
<script>
	import Box from './Box.svelte'
	import Child from './Child.svelte'
</script>

<Box>
	<Child></Child>
</Box>

```

- 위에처럼 context.js 에 빈 key 값을 저장해주고, Box에서 key 값 저장후 Child 에서 그 key 값을 받아오는것이 가능하다.
- 이때 svelte에  setContext 와 getContext 를 이용한다 ! 

#### 15 - 2. Context와 Store
- Context와 Store :  데이터를 공유한다는 점에서 유사하다 
- Store 는 어플리케이션 어느 위치에서도 사용 가능 
- Context 는 Context 를 선언한 해당 컴포넌트와 그 하위 컴포넌트에서만 사용할 수 있는 차이
- Context / 하나의 컴포넌트로 여러 인스턴스를 생성하게 될때 각각의 인스턴스가 하나의 상태를 공유하는 것이 아닌, 각각의 상태를 가진다는 장점
- Context는 반응형으로 동작하지 않기때문에, 반응형 동작을 원할 경우 store를 사용하는 것이 맞다.
- Context는 컴포넌트가 생성될때 호출되어야 한다. ( 클릭이벤트 함수 안에 set, getContext를 넣으면 정상적으로 동작하지 않는다. )

### 🖥 Svelte 요소
#### 16 - 1. <svelte:self>
- 6가지의 내장 요소를 제공한다 .
- self : 자기자신을 다시 사용하겠다 ex svelte:self {...flies}
- 자세한 설명 : [스벨트 공식문서](https://svelte.dev/tutorial/svelte-self), [<svelte:self>](https://beomy.github.io/tech/svelte/svelte-elements/)

#### 16 - 2. [실습] <svelte:self> - JSON parser 만들기

```javascript
// src/jsonItem.svelte
<script>
    export let json;
    export let key = 'JSON';

    const obj = JSON.parse(json)
    let expended = false;
    const entries = Object.entries(obj)
    // Object.entries -> [key, value] 쌍의 배열을 반환합니다
    const type = Object.prototype.toString.call(obj)
    // 어떤 타입인지 확인 ! 
    let value;
    if(type === '[object Array]'){
        value = `[${entries.length}]`
    }else if(type === '[object Object]'){
        value = `{${entries.length}}`
    }else {
        value = json
    }
</script>

<div>
    <span>{key}</span>: <span on:click={()=> expended = !expended}>{value}</span>
    {#if expended}
        {#each entries as [key, value], index (index)}
        <svelte:self {key} json={JSON.stringify(value)}></svelte:self>
        {/each}
    {/if}
</div>

// src/App.svelte
<script>
	import JsonItem from './JsonItem.svelte'
	let json = JSON.stringify({
		a: 1,
		b: [
			1,
			2,
			3
		],
		c: {
			d: 1,
			e: 2
		},
		f : 'test'
	})
</script>

<JsonItem {json}></JsonItem>
```

#### 16 - 3. <svelte:component>

```javascript
// src/App.svelte

<script>
	import Green from './Green.svelte'
	import Blue from './Blue.svelte'
	import Red from './Red.svelte'

	const options = [
		{color: 'green', component: Green},
		{color: 'blue', component: Blue},
		{color: 'red', component: Red},
	]

	let selected = options[0]
</script>

<select bind:value={selected}>
	{#each options as option (option.color)}
	<option value={option}>{option.color}</option>
	{/each}
</select>

<!-- {#if selected.color === 'red'}
<Red />
{:else if selected.color === 'green'}
<Green />
{:else if selected.color === 'blue'}
<Blue />
{/if} -->

<!-- 위와 같은 코드를 component 를 이용하면 더 간결히 표현할 수 있다. -->

<svelte:component this={selected.component}/>

<!-- 똑같은 화면이 구현된다. -->

// 다른 컴포넌트에서는 각 div 와 배경색을 준 상태
```

#### 16 - 4. <svelte:window>
- 윈도우객체에 간편하게 값을 바인딩 할 수있고, 이벤트도 등록할 수 있다.
- 바인딩 가능 목록 : innerWidth, innerHeihgt, outerWidth, outerHeight, scrollX, scrollY, online( window.navigator.onLine )
- scrollX와 scrollY를 제외한 모든 값은 readonly

```javascript
// src/App.svelte
<script>
	let key;
	let keyCode;
	let innerWidth;
	let innerHeight;
	let scrollY;
	function handleKeyDown(event){
		key = event.key
		keyCode = event.keyCode
	}
</script>

<svelte:window 
	on:keydown={handleKeyDown}
	bind:innerWidth={innerWidth}
	bind:innerHeight={innerHeight}
	bind:scrollY={scrollY}
/>

<p>{innerWidth}, {innerHeight}</p>
<div>
	{key}, {keyCode}
</div>

<button on:click={()=> scrollY = 0}>TOP({scrollY})</button>

<style>
	div {
		height: 200vh;
	}
	button {
		position: fixed;
		bottom: 0;
		right: 0;
	}
</style>
```

#### 16 - 5. <svelte:body>
- body 와 window 는 사용법이 비슷하다!

```javascript
// src/App.svelte
<script>
	let isEnter;
	function handleMouseenter(){
		isEnter = true;
	}
	function handleMouseleave(){
		isEnter = false;
	}
</script>

<svelte:body
	on:mouseenter={handleMouseenter}
	on:mouseleave={handleMouseleave}
/>

{isEnter}
// 이렇게 바디에 들어오면 true, 나가면 false 를 찍는것을 볼 수 있다.
```

#### 16 - 6. <svelte:head>

```javascript
// src/App.svelte
<svelte:head>
	<meta name="James">
</svelte:head>
```

- 위와 같이 추가해주면, 기존 index html 에 없는 meta 태그가 생긴것을 확인할 수 있다.

#### 16 - 7. <svelte:options>
- 컴파일옵션을 지정할 수 있다.
- immutable, accessors, namespace, tag -> 4가지 속성이 있다.
- immutable : 불필요한 반응성을 줄이기 위해 사용됨

```javascript
// src/App.svelte
<script>
	import Todo from './Todo.svelte'

	let todos = [
		{id:1, done: false, text: '공부하기'},
		{id:2, done: false, text: '밥먹기'},
		{id:3, done: false, text: '운동하기'},
	]

	function toggle(toggled){
		todos = todos.map( x => {
			return x === toggled ? {id: x.id, done: !x.done, text: x.text} : x
		})
	}
</script>

{#each todos as todo (todo.id)}
	<Todo {todo} on:click={()=> toggle(todo)}></Todo>
{/each}

// src/Todo.svelte
<script>
    import { afterUpdate } from 'svelte'
    export let todo;

    let updateCount = 0;
    afterUpdate(()=> {
        updateCount += 1;
    })
</script>

<svelte:options immutable={true}/>
<!-- 위에처럼 정의해주지 않으면, 하나만 변경되도 횟수가 모두 업데이트된다. -->

<div on:click>
    <!-- 부모 요소로 클릭이벤트를 전달해준다. -->
    {todo.done}, {todo.text} / {updateCount}회
</div>
```

### 🖥 Module context
#### 17 - 1. Module context

```javascript
// src/App.svelte
<script>
	import Child from './Child.svelte'
</script>

<Child></Child>
<Child></Child>

// src/Child.svelte
<script context="module">
    //  context="module" -> 스크립트 태그내에 정의된 태그는 동일한 컴포넌트로 생성된 인스턴스 내에서 공유된다.
    //  반응형으로 동작하지는 않지만, 콘솔로그에서는 변경되는것을 확인할 수 있다.
    let count = 0;
</script>

<script>
    function handleClick(){
        count += 1;
    }
</script>

{count}
<button on:click={handleClick}>add</button>
```

#### 17 - 2. 코드 내보내기
-  Module context 를 이용해서 코드를 내보내는 방법

```javascript
// src/App.svelte
<script>
	import Child, { printCount } from './Child.svelte'
</script>

<Child></Child>
<Child></Child>
<button on:click={printCount}>Show</button>

// src/Child.svelte
<script context="module">
    let count = 0;
    export function printCount(){
        alert(count);
    }
</script>

<script>
    function handleClick(){
        count += 1;
    }
</script>

{count}
<button on:click={handleClick}>add</button>
```



















