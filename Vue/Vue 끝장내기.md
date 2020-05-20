# Vue 끝장내기
### Vue 강의 들으면서 내용 정리하기 !
- 추후 업데이트 할 예정
<hr/>

**현대 웹 서비스 개발 절차**
- 요구사항 > 서비스 기획 > UI&UX 상세 설계 > GUI 디자인 > 퍼블리싱 > 백엔드 API 개발 > 프런트엔드 개발 > QA

**preset**
- 플러그인의 집합

**ESLint**
- 자바스크립트 코드에서 에러가 날 수 있는 것들에 대한 가능성들을 모두 제거
- 자바스크립트 코드, 문법 보조 도구
- rules 에 만약 "no-console" : "error" 로 해놓고, 콘솔을 사용한다면 error 가 뜬다. But off 라고 하면 run serve 가 된다.

**도구의 설정파일들을 바꿨을때는 서버를 항상 내렸다 올려줘야 한다.**

**Prettier**
- 코드 정리 도구
- .prettierrc = 프리티어 설정 파일
- 설정 파일로 정의 할 수 있지만 , eslint에 rules 와 충돌이 날 수도 있기 때문에 eslint rules 안에 들어가야 한다.
- ex "prettier/prettier": ['error', {
    프리티어의 속성
    printwidth : 80
    }]

**preitter 와 eslint 설명 글 > [Vue.js 개발 생산성을 높여주는 도구 3가지](https://joshua1988.github.io/web-development/vuejs/boost-productivity/)**

**파일의 절대 경로**
- 상대경로는 폴더의 레벨이 깊어질 수록 파일을 거슬러 올라가는 앞의 코드가 붙게된다 > 많이 번거로워 짐
- @/ 로 절대경로로 사용 할 수 있다. (특정 위치를 기준으로/ 밑에와 같이 설정해 줘야 한다.)
- **단, vscode 개발툴 기준**
- 1. 뷰 cli 로 생성한 프로젝트 폴더만 vscode로 열기
- 2. jsconfig.json 파일 생성 (프로젝트를 위한 파일이 아닌, vscode 내부 기능을 활용하기 위한 파일) / [파일링크](https://github.com/joshua1988/vue-til/blob/complete/jsconfig.json) / exclude란 위쪽 컴파일러옵션에 해당하지 않을 폴더들.

**[스타일 속성 읽어보기](https://kr.vuejs.org/v2/style-guide/index.html)/ 필수&매우추천함**

**VueRouter**
- Vue.use : 플러그인을 실행하기 위해서 초기화 하기 위한 코드
- new VueRouter 의 routes > vue router 에 의해서 제어되는, 페이지의 정보를 담는 라우팅 정보를 담는 속성.

**url 변경은 router-link / url 변경 됬을때 페이지 컴포넌트 떠야 하는 영역은 router-view**

**코드 스플리팅**
- router index 에서  component: () => import('파일경로')
- 이동할때마다 필요한 자바스크립트 파일을 그때그때 들고 오는것 (처음부터 전부 들고있는 것이 아니라!)
- 초기에 애플리케이션 로딩 속도가 줄어든다.

**리다이렉트**
- {path: '/', redirect: '/특정페이지',} // 맨위에 써준다.
- 초기 진입할때 특정 페이지로 바로 가게 하려면, 그때 쓸수있는 속성이 리다이렉트

**라우터의 폴백**
- {path: '*',component: () => import('@/views/NotFoundPage.vue'),}, // 맨끝에 써준다.
- path: * > 위쪽 글을 제외한 모든 url 에 반응하겠다. 그럴때에 연결해주는 component ! 
- 정해지지 않은 라우터에 반응 하는 라우터

**history 모드로 설정 하고 배포할때에는 [공식문서](https://router.vuejs.org/guide/essentials/history-mode.html)에서 url에 대한 우회, 필터링 같은 기능들을 넣어주어야 한다**

**views 파일은 깨끗하게 두는 편이 좋다 > 컴포넌트를 연결하는 방식이 기능적으로 더 좋음 !**

[async await 정리글](https://joshua1988.github.io/web-development/javascript/js-async-await/) | [ES6 Destructuring 정리글](https://joshua1988.github.io/es6-online-book/destructuring.html#%ED%8A%B9%EC%A0%95-%EA%B0%9D%EC%B2%B4%EC%9D%98-%EA%B0%92%EC%9D%84-%EA%BA%BC%EB%82%B4%EC%98%A4%EB%8A%94-%EB%B0%A9%EB%B2%95)

**axios.create()**
- axios.create({baseurl:''})
- 요청할때 공통설정을 모두 여기에 넣을 수 있다.
- 이때 .post 를 하게 될때, 주소 전체를 담는것이 아니라 뒷부분만 담으면 되기때문에 뒤로 갈수록 훨씬 코드가 간결해 진다.
- ex return axios.post(url, userData); | return instance.post('signup', userData);
- 위에 instance 는 axios.create() 를 const instance 에 할당한 것.


**env 파일**
- 키=값 형태로 정의할 수 있는 환경 변수 파일
- .env.development > 개발할때, 로컬서버
- .env.production > 배포할때, 도메인주소
- .env > development 나 production 이 없을때 공통으로 들어가야하는 부분들에 대해 넣음.(두개가 없을때 가장 높은 우선순위 )
- [Vue CLI env 파일 규칙 문서](https://cli.vuejs.org/guide/mode-and-env.html#modes-and-environment-variables)

**"VUE_APP_"접두사가 붙은 변수는 자동로드 / 사용시에는 process.파일명.이름(ex process.env.VUE_APP_API_URL)**
