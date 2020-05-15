# Vue
## 20200512
### Vue 강의 들으면서 내용 정리하기 ! 3
- [실습내용](https://github.com/jina95/vueStudy_learnVueJs)

**watch**
- 데이터를 대상으로 넣을 수 있다. 데이터의 변화에 따라서 특정 로직을 실행할 수 있는 뷰의 속성 
>> 여기 자체에서 콘솔로그를 찍으면 안되는건가?? 데이터를 바라보고 메소드를 실행시켜야 하는가?
- watch 는 계속해서 값의 변화를 추적하기 때문에 이전 값과 갱신된 값 두개 다 인자로 받을 수 있다

**watch 와 computed의 차이점은 ?**
- copmuted 는 단순한 텍스트의 입력을 받아서 값을 계산 (간단한 텍스트 연산)
- watch 무거운 로직, 매번 실행되는게 부담스러운 로직 (ex 데이터 요청)
- [왠만하면 computed 를 사용하는게 좋다. 간단한 값 계산시!](https://vuejs.org/v2/guide/computed.html#ad)

**vue cli**
- cd 특정 폴더 위치로 이동하는 기본 터미널 명령어
- ctrl + c 서버종료 명령어
- localhost : 컴퓨터로 간단한 서버를 하나 띄움 . 자기 ip 를 가리킴

**싱글파일컴포넌트란 ?**
- 특정영역에 해당하는 html, js, css 를 한 파일에 관리 하겠다.

**컴포넌트 태그는 최소한 두단어이상으로 조합하고, 한단어로 할때는 html 표준태그와 충돌하지 않게! (파스칼케이스 ex AppHeader.vue)**

**싱글페이지에서 props**
- 상위 app 에서 하위 태그에 <v-bind:프롭스 속성이름 = "상위컴포넌트의 데이터 이름">
- 하위 컴포넌트에 인스턴스 옵션을 넣어준다 ex props:['프롭스 속성이름'] 
- 이후 하위컴포넌트 template 에서 {{ 프롭스 속성 이름 }} 로 사용 

**싱글페이지에서 event emit**
- 하위 컴포넌트 메소드에서 this.$emit('보낼 이벤트의 이름')
- 상위컴포넌트에서 받는 태그에(하위컴포넌트) v-on:'보낼 이벤트의 이름'(하위컴포넌트에서 보낸 이름) = "실행할 메소드"

**axios.post()**
- .post 는 데이터를 생성하거나 조작할 때 사용하는 http 방법, 메소드
- 규칙 : axios.post(url, data)
- 이후 .then 과 .error 로 성공 실패여부 확인 가능


**꼭 읽어봐야 할 !**
- [vue공식문서](https://vuejs.org/v2/guide/) > 영어로 읽을 것
- [Vue.js 스타일 가이드](https://vuejs.org/v2/style-guide/) > 한글 상관 X
- [Vue.js Cookbook](https://vuejs.org/v2/cookbook/)
- [Vuex 공식 문서](https://vuex.vuejs.org/)
- [VueRouter 공식 문서](https://router.vuejs.org/)
- [Vue CLI 공식 문서](https://cli.vuejs.org/) 

