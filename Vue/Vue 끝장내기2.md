# Vue 끝장내기2
### Vue 강의 들으면서 내용 정리하기 !
- 추후 업데이트 할 예정
<hr/>

## 섹션10 : 브라우저 저장소를 이용한 인증값 관리

**🔎새로고침할때 문제점 해결하기**

<img src="https://github.com/jina95/TIL/blob/master/images/%ED%86%A0%ED%81%B0%EA%B0%92_%EC%9C%A0%EC%A0%80%EC%9D%B4%EB%A6%84%20%EC%A0%80%EC%9E%A5.png">
- 토큰저장하고, 라우터 저장할때 단순히 자바스크립트에 저장하는게 아니라 브라우저 저장소를 이용해서 토큰값을 저장하면 새로고침을 하더라도, 브라우저 저장소에서 토큰값을 꺼내와서 사용가능.

**이때 쿠키를 저장하는 방법 👇**

<img src="https://github.com/jina95/TIL/blob/master/images/%EC%BF%A0%ED%82%A4%EC%A0%80%EC%9E%A5%ED%95%98%EB%8A%94%EB%B0%A9%EB%B2%95.png"/>


**쿠키 패널에서 확인하는 방법**

<img src="https://github.com/jina95/TIL/blob/master/images/%ED%8C%A8%EB%84%90%EC%97%90%EC%84%9C%20%EC%BF%A0%ED%82%A4%EA%B0%92%20%ED%99%95%EC%9D%B8.png"/>

- 하지만 이렇게 되어도 새로고침할땐 값이 리셋된다. 그 이유는 스토어에 값이 전달 되지 않았기 때문인데 그때 cookies 의 { getAuthFromCookie, getUserFromCookie } 를 사용한다


<img src="https://github.com/jina95/TIL/blob/master/images/%EC%BF%A0%ED%82%A4%EC%99%80%EC%8A%A4%ED%86%A0%EC%96%B4%EC%9D%98%EC%97%B0%EA%B2%B0.png"/>


**컴포넌트단의 무거운 비지니스 로직이 많이 노출되기 보다는 다른파일에 코드로 옮기는 것이 좋다** 

<img src="https://github.com/jina95/TIL/blob/master/images/actions%20%EB%A1%9C%20%EB%84%98%EA%B8%B4%20%EC%BD%94%EB%93%9C.png"/>

- store > index > actions 로 넘기는것이 좋다


<img src="https://github.com/jina95/TIL/blob/master/images/await-dispatch.png"/>

- index의 LOGIN 비동기처리 끝나고나면 라우더로 메인페이지로 진입을 하기 때문에 await 가 꼭 필요하다.

- await 를 빼게되면 순서처리가 맞지 않는다 

- 그 이유는 토큰을 받아서 스토어에 저장한 후 라우터로 진입을 해야하는데 await가 없으면 dispatch 가 끝나기도 전에 라우터에 진입하게 되서 비동기처리가 되지 않는다.

- **await 필수!!**



