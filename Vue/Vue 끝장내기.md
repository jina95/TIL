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


