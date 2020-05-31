# Vue 끝장내기3
### Vue 강의 들으면서 내용 정리하기 !
- 추후 업데이트 할 예정
<hr/>

## 섹션15 : 학습 노트 데이터 수정

**🔎다이나믹 라우터 매칭**

<img src="https://github.com/jina95/TIL/blob/master/images/%EB%8B%A4%EC%9D%B4%EB%82%98%EB%AF%B9%20%EB%9D%BC%EC%9A%B0%ED%84%B0%20%EB%A7%A4%EC%B9%AD.png"/>
<img src="https://github.com/jina95/TIL/blob/master/images/%EC%95%84%EC%9D%B4%EB%94%94%EC%97%B0%EA%B2%B0.png"  width="50%"> <img src="https://github.com/jina95/TIL/blob/master/images/route%20id%20path%20%ED%99%95%EC%9D%B8.png" width="50%">

- route 에 path 를 정의할때 파라미터로 id를 받아서 해당 페이지로 진입했을때 그 아이디로 접근할 수 있는 형태

## 섹션16 : 데이터 포맷팅

**🔎VUe filter**
- [뷰 필터 안내 문서](https://vuejs.org/v2/guide/filters.html#ad)
<pre><code>
<--in mustaches-->
{{ message | capitalize }}
</pre></code>

- |(파이프) 를 이용해서 필터함수 이름만 넣어주게 되면 데이터에 필터함수의 내용을 결합하여 필터함수를 돌려서 나온 결과를 화면에 뿌려준다.

<img src="https://github.com/jina95/TIL/blob/master/images/formatDate.png" width="70%">
- filter 적용방법
- 위와 같이 적용한다면 해당 컴포넌트에서만 사용 가능한 filter 이다.

#### 🤔만약 여러컴포넌트에서 이용하고 싶다면?
- **전역** 필터로 사용하면 된다!

<img src="https://github.com/jina95/TIL/blob/master/images/utils%20filter.png" width="70%">

- utils > filter 

<img src="https://github.com/jina95/TIL/blob/master/images/format%20main%20js.png" width="70%">

- main.js 에서 전역으로 연결

**앞으로도 특정 텍스트를 형식화할 일 이 있을때는 filter 기능 사용할 것!**



## 섹션17 : 라우터 심화


**🔎라우터 네비게이션 가드란?**
- [라우터 네비게이션 가드 문서](https://router.vuejs.org/guide/advanced/navigation-guards.html)
- 로그인하지 않은 사용자가 특정 url 페이지로 이동했을때 이동을 막는것. : router.beforeEach
- 특정 라우터에 진입 하기 전에 beforeEnter 와 같은 라우터네비게이션 가드를 이용해서 데이터 먼저 호출후 받아왔을때만 로딩하게 함.

<img src="https://github.com/jina95/TIL/blob/master/images/%EB%9D%BC%EC%9A%B0%ED%84%B0%20%EB%84%A4%EB%B9%84%EA%B2%8C%EC%9D%B4%EC%85%98%EA%B0%80%EB%93%9C%20%EA%B8%B0%EC%B4%88%20%EC%BD%94%EB%93%9C.png" width="70%">

- new VueRouter 인스턴스가 router 변수에 담기게 끔 한다.
- export default 로 router 를 내보내야 한다.
- next 를 호출했을때만 beforeEach 의 특정로직 예를 들어 위와 같은 코드에서는 로그를 찍고 이동하는 로직을 확인 할 수있다.
- next 호출해줘야지만 다음페이지로 이동할 수 있다.

<img src="https://github.com/jina95/TIL/blob/master/images/meta%20auth%20true.png" width="70%">
<img src="https://github.com/jina95/TIL/blob/master/images/meta%20auth%20true%20if.png" width="70%">

- 라우터 페이지 속성에 meta 안에 auth 속성이 true 면 인증이 필요하다가 뜰 것.
- meta auth 를 통해 권한을 부여했다.
- meta auth true 를 이용해서 이 페이지는 권한이 필요하다까지 정의함.

**로그인 하지 않은 사용자를 인증이 필요한 페이지에 접근 할 수 없도록 라우터 네비게이션 가드 코드 추가**
<img src="https://github.com/jina95/TIL/blob/master/images/meta%20auth%20store.getters.isLogin.png" width="70%">

**로그아웃 시 쿠키 지우는 코드**

<img src="https://github.com/jina95/TIL/blob/master/images/appheader%20%ED%86%A0%ED%81%B0%20%EC%BF%A0%ED%82%A4%20%EC%82%AD%EC%A0%9C.png" width="70%">
<img src="https://github.com/jina95/TIL/blob/master/images/store%20%ED%86%A0%ED%81%B0%EA%B0%92%20%EC%A7%80%EC%9A%B0%EA%B8%B0.png" width="50%">

- appheader 와 store 에 코드 수정
- store 에 토큰값을 지우는 코드를 추가해주고, utils/cookies.js 에 있는 { deleteCookie } 를 이용해서 appheader 에서 쿠키값을 지워준다.
- deleteCookie 에서는 til_auth & til_user 필요! 





