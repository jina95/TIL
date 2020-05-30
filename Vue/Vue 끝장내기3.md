# Vue 끝장내기3
### Vue 강의 들으면서 내용 정리하기 !
- 추후 업데이트 할 예정
<hr/>

## 섹션15 : 학습 노트 데이터 수정

**🔎다이나믹 라우터 매칭**

<img src="다이나믹라우터매칭" width=""/>
<img src="아이디연결">
<img src="route id path 확인">
- route 에 path 를 정의할때 파라미터로 id를 받아서 해당 페이지로 진입했을때 그 아이디로 접근할 수 있는 형태

## 섹션16 : 데이터 포맷팅

**🔎VUe filter**
- [뷰 필터 안내 문서](https://vuejs.org/v2/guide/filters.html#ad)
<pre><code>
<!-- in mustaches --><br/>{{ message | capitalize }}
<pre><code>

- |(파이프) 를 이용해서 필터함수 이름만 넣어주게 되면 데이터에 필터함수의 내용을 결합하여 필터함수를 돌려서 나온 결과를 화면에 뿌려준다.

<img src=formatdate>
- filter 적용방법
- 위와 같이 적용한다면 해당 컴포넌트에서만 사용 가능한 filter 이다.

**🤔만약 여러컴포넌트에서 이용하고 싶다면?**
- **전역** 필터로 사용하면 된다!

<img src="utils filter">
- utils > filter 
<img src="format main js">
- main.js 에서 전역으로 연결

**앞으로도 특정 텍스트를 형식화할 일 이 있을때는 filter 기능 사용할 것!**


## 섹션17 : 라우터 심화

**🔎라우터 네비게이션 가드란?**
- [라우터 네비게이션 가드 문서](https://router.vuejs.org/guide/advanced/navigation-guards.html)
- 로그인하지 않은 사용자가 특정 url 페이지로 이동했을때 이동을 막는것. : router.beforeEach
- 특정 라우터에 진입 하기 전에 beforeEnter 와 같은 라우터네비게이션 가드를 이용해서 데이터 먼저 호출후 받아왔을때만 로딩하게 함.

<img src="라우터 네비게이션가드 기초 코드">
-  new VueRouter 인스턴스가 router 변수에 담기게 끔 한다.
- export default 로 router 를 내보내야 한다.
- next 를 호출했을때만 beforeEach 의 특정로직 예를 들어 위와 같은 코드에서는 로그를 찍고 이동하는 로직을 확인 할 수있다.
- next 호출해줘야지만 다음페이지로 이동할 수 있다.







