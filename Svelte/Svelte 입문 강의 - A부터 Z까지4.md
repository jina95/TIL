# Svelte 입문 강의 - A부터 Z까지 💻 

## 4️⃣
### 🖥 Store
#### 9 - 2. Writable stores
- writable 의 인자값은 공유할 자원의 초기값을 지정
- writable 의 return 값은 공유할 store
- store : set update subscribe 세개를 포함하는 객체

```javascript
// src/ stores.js
import { writable } from 'svelte/store'

export const count = writable(0);

// src/ App.svelte
<script>
	import { onDestroy } from 'svelte'
	import { count } from './stores.js'

	import Incrementer from './Incrementer.svelte'
	import Decrementer from './Decrementer.svelte'
	import Resetter from './Resetter.svelte'

	let countValue ;

	const unSubscribe = count.subscribe(value => countValue = value);
	onDestroy(unSubscribe)
</script>
	// subscribe 는 count에 값이 변경될때마다 subscribe에 전달될 함수가 콜백된다 ?  
	// 무슨말인지 잘 모르겠다..
	// resetter 나 incrementer 등에서 버튼이 눌려져서 count의 값이 업데이트 됬을때 subcscribe에 인자로 전달된 함수가 호출된다...?

	// count에 값이 변경될때마다 함수가 호출되기때문에 onDestroy를 통해 subscribe 를 해지해야한다고 하는데,
	// 실습을 해봐야확실히 알것같다.. 왜 해지해야하는지..!?

<p>count : { countValue } </p>

<Incrementer></Incrementer>
<Decrementer></Decrementer>
<Resetter></Resetter>
```

#### 9 - 3. Store 자동 구독
- 자동구독이란 ?
- count 값 변경 -> 변수 업데이트 -> 화면 노출 -> 컴포넌트제거 -> onDestroy에서 관찰함수 제거 
- => 위의 과정을 자동구독이 대신해주게 된다.
- count -> $count 로 대체
- 기존 incrementer 과 같은 함수에서 업데이트 해주던 부분을 ex $count = $count - 1 이런식으로 변경해 줄 수 있다.
- 그렇기 때문에 스벨트는 변수 선언시, 변수명 앞에 $ 를 붙일수 없다.

#### 9 - 4. Readable stores
- 사용자가 수정할 필요 없는 스토어를 만들어야 할 때 사용

<pre><code>-   `initial`: 첫 번째 파라미터는 초깃값입니다. 초깃값을 설정할 필요가 없을 경우,  `null`이나  `undefined`를 사용할 수 있습니다.
-   `start`: 두 번째 파라미터는 첫 구독자가 발생했을 때 호출되는 함수입니다.  `set`  콜백 함수를 파라미터로 가지고  `stop`  함수를 리턴하는 함수입니다.
-   `set`: 관찰하고 있는 값을 변경하는 콜백 함수입니다.
-   `stop`: 모든 구독자가 구독을 중단하면 호출되는 함수입니다.  `start`  함수에서 사용된 자원들이 있다면, 이 함수 내에서 자원을 해제해야 합니다.</code></pre>

```javascript
// src/ stores.js
import { readable } from 'svelte/store'

export const time = readable(new Date(), function (set) {
    const interval = setInterval(()=> {
        set(new Date())
    }, 1000)
    return function stop () {
        clearInterval(interval)
    }
})
```

#### 9 - 5. Derived stores
- Derived stores를 이용하면 기존의 스토어들을 이용해서 새로운 스토어를 만들어 낼 수 있다.

<pre><code>-   첫 번째 파라미터는 참고하는 store입니다. 참고하는 store가 하나라면  `derived(a, ...)`으로 객체가 됩니다. 참고하는 store가 여러 개라면  `derived([a, ...b], ...)`로 배열이 됩니다.
-   두 번째 파라미터는 새로운 store의 값을 리턴하는 콜백 함수입니다. 콜백 함수의 파라미터는 참고하는 store입니다. 콜백 함수의 마지막 파라미터는  `set`  함수입니다.  `derived([a, ...b], ([$a, ...$b], set) => ...)`와 같은 형태입니다.
-   세 번째 파라미터는 새로운 store의 초깃값입니다. </code></pre>

```javascript
// src/ stores.js

// 페이지에 접속하고 나서 몇초가 지났는지 알려주는 함수
const start = new Date();
export const elapsed = derived(time, ($time) => {
  return Math.round(($time - start) / 1000);
});
// 전 9-4에서 사용했던 time 이용
```

#### 9 - 6. Custom stores

```javascript
// src/ stores.js
import { writable } from 'svelte/store'

function createCount() {
    const { set, subscribe, update } = writable(0)

    return {
        subscribe,
        increment: () => update(x => x + 1),
        decrement: () => update(x => x - 1),
        reset: () => set(0),
    }
}

export const count = createCount();
// 위와 같이 count라는 커스텀스토어를 만들수 있다.

// src/App.svelte
<script>
import { count } from './stores.js'
console.log(count);

</script>

<p>{ $count }</p>
<button on:click={count.increment}>+</button>
<button on:click={count.decrement}>-</button>
<button on:click={count.reset}>reset</button>
```

#### 9 - 7. Store bindings


```javascript
// src/ stores.js
import { writable, derived } from 'svelte/store'

export const name = writable('james')

export const greeting = derived(
    name,
    $name => `Hello, ${$name}`
)

// src/App.svelte
<script>
import { name, greeting } from './stores.js'
</script>

<p>{ $greeting }</p>
<input type="text" bind:value={$name} />

<button on:click={()=> $name += '!'}>Add!!!</button>
```

### 🖥 Motion
#### 10 - 1. Motion 이란
- 스벨트는 변수를 돔에 바인딩하고, 돔이 업데이트되면 자동으로 바인딩된 변수의 값을 업데이트 한다.
- 바인딩된 변수의 값이 업데이트 되었을때 애니메이션을 사용할 수 있게 하는 기능이 모션이다.
- **Motion은 Store 이다** 
- 모션의 종류 : Tweened, Spring => 둘다 easing함수를 이용해서 애니메이션을 동작한다.

#### 10 - 2. Tweened

`tweened`  함수는 2개의 파라미터를 가집니다. 첫 번째 파라미터는 변경되는 값이고 두 번째 파라미터는 옵션입니다.  `tweened`  함수는 store를 리턴합니다.  `options`에 설정할 수 있는 값을 살펴보겠습니다.

-   `delay`  (number, default 0): 단위는 ms로, 설정한 시간 후에 시작됩니다.
-   `duration`  (number, default 400): 단위는 ms로, 설정한 시간 동안 실행됩니다.
-   `easing`  (function, default t => t):  `easing`  함수입니다. Svelte는 기본으로 30가지 템플릿([https://svelte.dev/docs#svelte_easing](https://svelte.dev/docs#svelte_easing)  참고)을 제공합니다. 커스텀 하게 만들 수도 있습니다.
-   `interpolate`  (function): 두 값 사이를 보간하여 좀 더 부드럽게 보여주기 위해서 사용되는 옵션입니다.  `(a, b) => t => value`  형태가 와야 합니다.  `a`는 시작 값,  `b`는 목푯값,  `t`는 0과 1사이의 숫자이고,  `value`는 결과 값입니다.

`store.set`과  `store.update`의 두 번째 파라미터에  `options`(위에서 설명한 옵션)를 전달할 수 있습니다. 전달된 옵션은 기본값(인스턴스를 생성할 때 사용한  `tweened(value, options)`의  `options`가 기본값입니다.)에 오버라이드(override) 됩니다.  `set`과  `update`  함수의 리턴 값은 Promise입니다. tween 작업이 완료되면 Promise가 resolve 됩니다.

```javascript
// src/App.svelte
<script>
import { tweened } from 'svelte/motion'
import { cubicOut } from 'svelte/easing'

const progress = tweened(0, {
	delay: 200,
	duration: 400,
	easing: cubicOut
})

console.log(progress, $progress);

</script>

<progress value={$progress}></progress>

<button on:click={() => $progress = 0}>0%</button>
<button on:click={() => $progress = 0.25}>25%</button>
<button on:click={() => $progress = 0.5}>50%</button>
<button on:click={() => $progress = 0.75}>75%</button>
<button on:click={() => $progress = 1}>100%</button>
```

#### 10 - 3. Spring
- spring motion은 자주 변경되는값을 사용하는것이 좋다.
- 스프링처럼 튕기는 애니메이션 사용 가능 
- 2개의 파라미터를 가지는데, 첫번째는 변경되는값 / 두번째는 옵션

### 🖥 트랜지션
#### 11 - 1. 트랜지션 사용하기

```javascript
// src/App.svelte
<script>
import { fade } from 'svelte/transition';
let visible = true;
</script>

<label for="">
	<input type="checkbox" bind:checked={visible}>
	visible
</label>


{#if visible}
	<p transition:fade={{ delay:1000, duration: 1000}}>Fade out</p>
{/if}
```

#### 11 - 2. 트랜지션 종류
- fade : 투명에서 불투명 (delay, duration)
- blur : 흐렷했다가 뚜렷해짐 (delay, duration, easing, opacity, amount)
- fly : 날라오면서 추가되고 날라가면서 제거 (delay, duration, easing, x, y, opacity)
- slide : 위에서 아래로 슬라이드 (delay, duration, easing)
- scale : 날라오는 ..? (delay, duration, easing, start, opacity)
- draw : svg요소에만 사용가능, 선 그리듯이 화면에 나타내고 제거 (delay, speed, duration, easing)
- crossfade : 엑스자로 추가되거나 제거

#### 11 - 3. 트랜지션 In/Out
- 요소가 화면에 추가됬을때, 제거됬을때 각 각 다른 트랜지션을 줄 수 있다.

```javascript
// src/App.svelte
<script>
	import { fly, fade } from 'svelte/transition'
	let visible = true;
</script>

<label>
	<input type="checkbox" bind:checked={visible} />
	checkbox
</label>

{#if visible }
	<p
	in:fly={{ duration: 2000, y: 200}}
	out:fade
	>Transition</p
		>
{/if}
```

#### 11 - 4. 커스텀 트랜지션
- [사이트 참고하기](https://beomy.github.io/tech/svelte/transition/)

#### 11 - 5. 트렌지션 이벤트
- 트렌지션이 언제 시작되고 언제 끝나는지 알려주는 이벤트
- on:introstart : 요소가 화면에 출력되기 시작했을때
- on:introend : 화면에 추가된 트랜지션이 끝났을 떄
- on:outrostart : 화면에 제거되기 시작했을 때
- on:outroend : 화면에 제거된 트랜지션이 끝났을 때

```javascript
// src/App.svelte
<script>
	import {fly} from 'svelte/transition'
	let visible = true;
	let status = '기다리는중..'
</script>

<p>{status}</p>

<lable>
	<input type="checkbox" bind:checked={visible} >
</lable>

{#if visible}
	<p 
		transition:fly={{ duration: 2000, y: 200}} 
		on:introstart={()=> status='intro start'} 
		on:introend={()=> status='intro end'}
		on:outrostart={()=> status='outro start'}
		on:outroend={()=> status='outro end'}
	>
	transition
	</p>
{/if}
```

#### 11 - 6. 트렌지션 수식어
- 로컬 수식어를 사용할 수 있다.
- 로컬 수식어를 사용하면 상위 블록에 요소가 추가될 경우에만 트랜지션이 동작한다.

```javascript
// src/App.svelte
<script>
import { slide } from 'svelte/transition';
let items = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
let showItems = true;
let i = 5 ; // 리스트에 몇번째까지 표시할지 정하는 
</script>

<label>
	<input type="checkbox" bind:checked={showItems} />
	show list
</label>

<label>
	<input type="range" bind:value={i} max="10"/>
</label>

{#if showItems}
	{#each items.slice(0,i) as item,index (index)}
	<div transition:slide|local>
		{item}
	</div>
	{/each}
{/if}

<!-- div가 추가될 경우에만 슬라이드가 먹는다 : local때문에 -->
```











