# Vue
## 20200510
### Vue 강의 들으면서 내용 정리하기 !

object.defineproperty(대상객체, 객체의 속성, {

// 정의할 내용이 들어간다.

// 속성에 접근했을때의 동작을 정의<br/>
get<br/>
// 속성에 값을 할당했을때의 동작을 정의<br/>
set >> new value 라는 새로 할당 된 값이 인자로 필요.

})

객체의 동작을 재정의 하는 api ( 동작을 우리 맘대로 바꿀 수 있다는 뜻)

<b>할당할때마다 값이 reactivity 된다. 뷰의 핵심 !! <br/>
데이터의 변화를 라이브러리에서 감지해서 알아서 화면을 자동으로 그려주는것이 리액티비티</b>

<hr/>

[즉시실행함수 MDN](https://developer.mozilla.org/ko/docs/Glossary/IIFE)
- 역할 : 기본적으로 어플리케이션 로직에 노출되지 않게 또다른 스코프,유효범위에 넣어주는것. 일반적인 오픈소스라이브러리에서 변수를 이런식으로 관리.

함수의 이름이 대문자다 >> 생성자 함수를 의미
함수를 이용해서 어떤 정보를 담은 객체를 생성하는게 객체생성패턴

[생성자 함수 MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Obsolete_Pages/Core_JavaScript_1.5_Guide/Creating_New_Objects/Using_a_Constructor_Function) / 
[prototype MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)

<hr/>

vue 인스턴스에서는
key : value 형식으로 존재
생성자 안에 인자는 객체

