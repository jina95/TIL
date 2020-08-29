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


