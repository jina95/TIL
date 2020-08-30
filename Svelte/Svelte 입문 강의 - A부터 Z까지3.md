# Svelte 입문 강의 - A부터 Z까지 💻 

## 3️⃣
### 🖥 데이터 바인딩 기초
#### 6 - 1. input 태그

```javascript
<script>
	// type="text"
	let name = 'bill'; 
	// type="number", "range"
	let a = 1;
	// type="checkbox" & if
	let yes = false;
	// type = "radio" 
	let picked = null;
	// type="checkbox" & each
	const names = ['bill', 'test', 'world']
	let checkedNames = [];
</script>

<input type="text" bind:value={name}>
<h1>{name}</h1>

<input type="number" bind:value={a} min="0" max="10">
<input type="range" bind:value={a} min="0" max="10">

<h1>{a}</h1>

<input type="checkbox" bind:checked={yes}>
{#if yes}
	<p>YES</p>
{:else}
	<p>NO</p>
{/if}


<label>
	<input type="radio" value="One" bind:group={picked}>
	One
</label>
<label>
	<input type="radio" value="Two" bind:group={picked}>
	Two
</label>

<h1>{picked}</h1>


{#each names as name, index (index)}
<label>
	<input type="checkbox" value={name} bind:group={checkedNames}>
	{name}
</label>
{/each}

<h1>{checkedNames}</h1>
```

- 위의 코드는 아래와 같이 구현 된다.

<img src="svelte_input 태그" width="50%">


#### 6 - 2. textarea 태그

```javascript
<script>
	let value = 'skarsgard'
</script>

<textarea bind:value={value}></textarea>
// 아래와 같이 생략할 수 있다.
<textarea bind:value></textarea>
<p>{value}</p>
```

#### 6 - 3. select 태그

```javascript
<script>
	let list =[
		{id:1, text:'james'},
		{id:2, text:'bill'},
		{id:3, text:'tom'},
	]
	let selected= [];
</script>


<select bind:value={selected} multiple>
	{#each list as item }
	<option value={item}>{item.text}</option>
	{/each}
</select>

<p>선택함 : {selected ? selected.id : '기다리는중...'}</p>
<p>선택함 : {selected ? selected.map(x => x.id).join(',') : '기다리는중...'}</p>
```

- selected 값에는 number, 객체, 등 타입을 가리지 않는다
- 현재 selected 에 값을 초기화 해주지 않았는데도 값이 정해져있는것을 볼 수 있다. (ex let selected;)
- 그 이유는 svelte 자체에서 사용자가 초기값을 정하지 않았을때, 첫번째 값을 설정해주기 때문
- multiple : 여러개 선택 가능

#### 6 - 4. contenteditable 기능
- contenteditable : 사용자가 요소를 편집할 수 있는지 나타내는 열거형 특성
- [MDN contenteditable](https://developer.mozilla.org/ko/docs/Web/HTML/Global_attributes/contenteditable)

```javascript
<script>
	let html = '<p>billl</p>'
</script>

<div 
	contenteditable="true"
	bind:innerHTML={html}
></div>

<pre>{html}</pre>

<style>
	[contenteditable] {
		padding: 10px;
		border: 1px solid blue;
	}
</style>
``` 

- style 에서 [contenteditable] 처럼 ~한 속성을 가지고 있는 경우만을 따로 묶어서 style을 줄 수 있다.

#### 6 - 5. Each 블록 바인딩
- todo 만들기 ! 

```javascript
<script>
	let todos = [
		{ done:false, text:''}
	]
	$ : remaining = todos.filter(x => !x.done).length

	function add(){
		todos = todos.concat({done:false, text: ''})
	}

	function clear(){
		todos = todos.filter(x => !x.done)
	}
	
</script>

{#each todos as todo, index (index)}
	<div class:done={todo.done}>
		<input type="checkbox" bind:checked={todo.done}>
		<input type="text" bind:value={todo.text}>
	</div>
{/each}
<p>남은 할일 : {remaining}</p>

<button on:click={add}>추가</button>
<button on:click={clear}>완료한 애들 삭제~</button>

<style>
	.done {
		opacity: 0.4;
	}
</style>
```

### 🖥 데이터 바인딩 고급
#### 7 - 1. Media 태그
- [svelte 공식문서](https://svelte.dev/tutorial/media-elements)

> 강의내용이 부족해서.. 문서확인하는게 좋을 것 같다.

- **8가지 Readonly 속성**

아래 목록은 read only로 바인딩 할 수 있는 8가지 속성입니다.

-   `duration`  _Number_  (readonly): 총 재생 길이(초 단위)
-   `buffered`  _Array_  (readonly):  `{start, end}`  객체들의 배열로, 버퍼 된 위치를 표시함
-   `seekable`  _Array_  (readonly):  `{start, end}`  객체들의 배열로, 위치를 찾을 수 있는 범위를 표시함
-   `played`  _Array_  (readonly):  `{start, end}`  객체들의 배열로, 재생했던 위치들을 표시함
-   `seeking`  _Boolean_  (readonly): 찾는 중인지를 표시하는 플래그
-   `ended`  _Boolean_  (readonly): 재생이 끝났는지를 표시하는 플래그
-   `videoWidth`  _Number_  (readonly):  `<video>`  태그에서 사용할 수 있는 속성으로  `<video>`  태그의 너비를 나타냄.
-   `videoHegiht`  _Number_  (readonly):  `<video>`  태그에서 사용할 수 있는 속성으로  `<video>`  태그의 높이를 나타냄.

> binding은 가능하지만 수정은 할 수 없는 8가지 속성

<hr>

- **4가지 Read, Write 가능한 속성**

아래 목록은 write와 read 둘 다 가능한 4가지 속성입니다.

-   `currentTime`  _Number_: 현재 재생 위치를 나타냄(초 단위)
-   `playbackRate`  _Number_: 재생 속도를 나타냄(normal: 1)
-   `paused`  _Boolean_: 일시정지됐는지 표시하는 플래그
-   `volume`  _Number_: 음량의 크기를 나타냄(0과 1 사이의 값)


- 참고자료: [데이터 바인딩 고급](https://beomy.github.io/tech/svelte/bindings-in-depth/)

#### 7 - 2. Dimension 바인딩

```javascript
<script>
	let w;
	let h;
	let size = 42;
	let text = 'skarsGard'
</script>

<input type="range" bind:value={size}>

<p>너비 : {w}, 높이 : {h}</p>

<div bind:clientWidth={w} bind:clientHeight={h}> 
	<span style="font-size: {size}px;">{text}</span>
</div>

<style>
	div{
		display: inline-block;
	}
</style>
```

- 주의 할 점 
- 1. 성능 이슈 : clientWidth 를 계산하기 위해서 돔은 계속 재랜더링하는데, 거기서 오버헤드(어떤 처리를 하기 위해 들어가는 간접적인 처리 시간 · 메모리등 / 어떤처리를 위해 메모리사용이 많으면 오버헤드가 발생했다고 한다)가 발생될 수 있기때문에 dimension요소 바인딩하는것을 추천하지 않음
- 2. dimension요소는 div, p 와 같은 블럭요소에만 가능 / inline 으로 변경시 높이와 너비를 가져올 수 없다.
- 3. 캔버스와 같이 자식요소를 가질수 없는 요소들도 dimension 속성을 바인딩 할 수 없다. 

#### 7 - 3. this 바인딩
- this를 바인딩 한다 == 자기 자신을 특정변수에 할당한다 
- html 에서 바인딩 하면, 그 변수는 html 엘리먼트가 되고 컴포넌트에서 바인딩하면 그 변수는 컴포넌트가 된다.(?) 

```javascript
// 부모 
<script>
	import Child from './Child.svelte'
	let first;
	let second;

	function handleClick(){
		console.log(first);
		console.log(second);
		
		
	}
</script>

<button on:click={handleClick}>ddd</button>
<div bind:this={first}>DIV</div>
<Child bind:this={second}></Child>

// 자식 
<span>Child</span>
```

#### 7 - 4. 컴포넌트 Props 바인딩

```javascript
// 부모 컴포넌트
<script>
	import Child from './Child.svelte'
	let number = 3;
</script>

<Child bind:number={number}></Child>
<p>{number}</p>

// 자식 컴포넌트
<script>
    export let number;

    function handleClick(){
        number *= number 
    }
</script>

<button on:click={handleClick}>제곱하기</button>
```

- 부모 컴포넌트에서 bind:number={number} 을 해주었는데, 이렇게 되면 부모, 자식 컴포넌트 모두에서 number에 값을 변동시킬 수 있기 때문에 (양방향 통신) 남발하면 좋지 않다
- 에러를 파악하기가 어려워질수 있기 때문 ! 


### 🖥 라이프 사이클
#### 8 - 1. 라이프 사이클이란
- 1. onMount / 컴포넌트가 화면에 그려졌을때 호출
- 2. onDestroy / 컴포넌트가 화면에 제거되었을때 실행
- 3. beforeUpdate / 화면이 업데이트되기 직전
- 4. afterUpdate / 화면에 값이 업데이트된 이후 호출 
- Svelte의 라이프 사이클 함수들은 import { 라이프 사이클 함수 이름 } from 'svelte'로 라이프 사이클 함수를 가져올 수 있습니다.

#### 8 - 2. onMount
- 컴포넌트가 처음으로 돔에 랜더링 됬을때 실행되는 함수
- 네트워크를 통해 데이터를 가져와야할 경우 onMount 추천

```javascript
// 부모컴포넌트
<script>
	import Child from './Child.svelte'
	let condition =true;
</script>

<button on:click={()=> condition = !condition}>toggle</button>

{#if condition}
<Child></Child>
{/if}

// 자식컴포넌트
<script>
    import { onMount } from 'svelte';
    let photos = [];

    // 아래는 데이터를 불러올때
    onMount(async()=> {
        const res = await fetch('https://jsonplaceholder.typicode.com/photos?_limit=20');
        photos = await res.json();
        console.log(photos);
    })

    // 아래는 데이터를 불러오고, 사라졌을때의 처리까지 해줄때
    onMount(()=> {
        fetch('https://jsonplaceholder.typicode.com/photos?_limit=20')
        .then (async(res)=>{
            photos = await res.json();
        })
        
        return ()=>{
            console.log('사라졌다')
        }
    })
</script>

{#each photos as photo (photo.id)}
<figure>
    <img src={photo.thumbnailUrl} alt={photo.title}>
    <figcaption>{photo.title}</figcaption>
</figure>
{:else} 
<p>is loading....</p>
// 반복문에서도 else 를 사용할 수 있다. 상위 컴포넌트에서 if 를 썻기때문인듯!
{/each}
```

#### 8 - 3. onDestroy
- 컴포넌트가 화면에 제거되기 직전에 호출되는 라이프사이클 함수
- onMount, onDestroy  둘다 console.log() 찍었을때, 제거되기전인 onDestroy 먼저 콘솔에 찍히고 그 이후에 onMount 가 찍히는 것을 확인할 수 있다.

```javascript
// 부모 컴포넌트
<script>
	import Child from './Child.svelte'
	let condition = true;
</script>

<button on:click={()=> condition = !condition}></button>

{#if condition}
<Child></Child>
{/if}

// 자식 컴포넌트
<script>
    import { onMount } from 'svelte'
    import { onDestroy } from 'svelte'
    let seconds = 0;

    const interval = setInterval(() => {
        seconds += 1;
        console.log(seconds);   
    }, 1000);

    onDestroy(()=>{
        console.log('onDestroy');
        clearInterval(interval)
    })
    onMount(()=>{
        return () => {
            console.log('onMount');
        }
    })
</script>

<p>{seconds}초</p>
```

#### 8 - 4. 라이프 사이클 모듈화
- 일반적 js 파일에서도 사용 가능

```javascript
// 기존 자식 컴포넌트 
<script>
    import { onInterval } from './utils.js'
    let seconds = 0;

    onInterval(()=> seconds += 1, 1000 )
</script>

<p>{seconds}초</p>

// utils.js 파일 생성
import { onDestroy } from 'svelte'

function onInterval(seconds, ms){
    const interval = setInterval(seconds, ms);
    onDestroy(() => {
        console.log('onDestroy');
        clearInterval(interval)
    })
}

export { onInterval}
```

#### 8 - 5. beforeUpdate와 afterUpdate
- beforeUpdate 는 mount 되기 전에 호출되기 때문에 undefined가 찍힌다
- 그렇기 때문에 beforeUpdate 를 사용할때는 데이터 바인딩으로 p 를 가져오고, p && p.innerText 로 예외처리 해준다. ( DOM 이 존재하는지 체크하는 로직)

```javascript
<script>
	import { onMount, afterUpdate, beforeUpdate } from 'svelte'
	let number = 0
	let p;

	beforeUpdate(()=>{
		console.log("beforeUpdate", p&&p.innerText);
	})
	onMount(()=>{
		console.log("onMount" );
	})
	afterUpdate(()=>{
		console.log("afterUpdate", p.innerText);
	})

</script>

<button on:click={()=> number += 1}>Add</button>
<p bind:this={p}>{number}</p>
```

#### 8 - 6. tick
- 언제든지 사용할 수 있는 라이프사이클 함수
- svelte 는 데이터의 변경을 즉각적으로 처리하지 않고 쌓아두었다가 한번에 바꾸게 됨으로써 불필요한 동작을 줄이고 브라우저가 효율적으로 작업할 수 있다.

```javascript
<script>
	import {tick} from 'svelts'
	let text = 'what the fuck!!!!!!'

	async function handleKeyDown(event){
		if(event.which !== 9) return;

		const { selectionStart, selectionEnd, value } = this;
		const selection = value.slice(selectionStart, selectionEnd)

		// 만약 소문자면 대문자로 , 대문자면 소문자로
		const replacement = /a-z/.test(selection)
			? selection.toUpperCase()
			: selection.toLowerCase();

		// 선택하지 않은 값은 그대로 + 선택한 값은 소문자 || 대문자로 + 선택하지 않고 남은부부분 그대로 
		text = (value.slice(0, selectionStart) + replacement + value.slice(selectionEnd))

		await tick(); 
		// 스크롤한 부분 유지시켜주기 위한 
		this.selectionStart = selectionStart
		this.selectionEnd = selectionEnd

	}
</script>

<textarea bind:value={text} on:keydown|preventDefault={handleKeyDown}></textarea>
```






