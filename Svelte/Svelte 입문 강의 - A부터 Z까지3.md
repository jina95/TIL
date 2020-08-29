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



