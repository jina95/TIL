---


---

<h1 id="💡netlify로-배포하기">💡Netlify로 배포하기</h1>
<ul>
<li>git hub repository 를 선택한 후,</li>
</ul>
<img src="https://github.com/jina95/TIL/blob/master/images/%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C/Netlify%EB%A1%9C%20%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0_1.png" width="80%">
<img src="https://github.com/jina95/TIL/blob/master/images/%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C/Netlify%EB%A1%9C%20%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0_3.png">
<ul>
<li>위와 같이 입력해 준다.</li>
<li>이후 본인의 코드에 가서 <strong>$ npm run build</strong> 를 하고 dist 폴더 생성을 확인한 후, git 에 push 해 준다.</li>
</ul>
<blockquote>
<p>만약 dist가 있는 위치가 폴더 안에 위치한다면 ,  아래와 같이 셋팅해 주어야 한다.</p>
</blockquote>
<img src="https://github.com/jina95/TIL/blob/master/images/%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C/Netlify%EB%A1%9C%20%EB%B0%B0%ED%8F%AC%ED%95%98%EA%B8%B0_2.png">
<ul>
<li>이후에, 작업을 추가해서 변동이 생기더라도 dist에 자동적으로 업데이트가 되어서, 배포한 사이트에도 업데이트 된 내용이 적용되는 것을 확인할 수 있다.</li>
</ul>
<hr>
<h3 id="😈새로고침시-page-not-found-가-뜬다-">😈새로고침시 page not found 가 뜬다 !</h3>
<ul>
<li>redirect 옵션을 줘야 한다!</li>
<li>public / _redirects 파일 생성</li>
</ul>
<pre><code>/* /index.html 200.</code></pre>
<ul>
<li>해당 파일에 위의 내용을 추가해 준다.</li>
</ul>
<p>&lt; hr&gt;</p>
<ul>
<li>참고 사이트 : <a href="https://13akstjq.github.io/react/2019/09/01/React-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-Netlify%EC%97%90-%EB%B0%B0%ED%8F%AC%ED%96%88%EC%9D%84%EB%95%8C-NotFound-%EC%9D%B4%EC%8A%88-%ED%95%B4%EA%B2%B0.html">https://13akstjq.github.io/react/2019/09/01/React-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-Netlify%EC%97%90-%EB%B0%B0%ED%8F%AC%ED%96%88%EC%9D%84%EB%95%8C-NotFound-%EC%9D%B4%EC%8A%88-%ED%95%B4%EA%B2%B0.html</a></li>
<li>참고 사이트 : <a href="https://medium.com/@ishoshot/page-not-found-on-reload-vuejs-netlify-c71716e97e6">https://medium.com/@ishoshot/page-not-found-on-reload-vuejs-netlify-c71716e97e6</a></li>
<li>참고 사이트 : <a href="https://docs.netlify.com/routing/redirects/redirect-options/#placeholders">https://docs.netlify.com/routing/redirects/redirect-options/#placeholders</a></li>
</ul>

