---


---

<h1 id="💡협업프로젝트-pull--push">💡협업프로젝트 pull &amp; push</h1>
<blockquote>
<p>내가 정리한 사이트를 기반으로 함 : <a href="https://github.com/jina95/TIL/blob/master/project/moneyboo_202006-08/5st_0719.md">https://github.com/jina95/TIL/blob/master/project/moneyboo_202006-08/5st_0719.md</a></p>
</blockquote>
<ol>
<li>remote / 포크 해 온 상태라면, origin 저장소 밖에 없을 것. upstream 저장소를 추가해 주자!</li>
</ol>
<blockquote>
<p><strong>$ git remote -v</strong> 하면 origin 만 있는것을 확인 할 수 있다. 이때 상대방 ( 원본저장소) 의 저장소도 필요하기 때문이다</p>
</blockquote>
<ol start="2">
<li><strong>$ git remote add upstream 원본저장소주소(상대방).git</strong> 명령어로 upstream 저장소를 추가 해 준다.</li>
<li>프로젝트 규칙에 따라 이후 브랜치를 생성해 준다 <strong>$ git checkout -b 브랜치이름</strong> ( 이렇게 하면 생성과 동시에 체크아웃을 함)</li>
<li>이후 add, commit 을 해주고 push를 한다. <strong>$ git push origin 브랜치이름(ex feature/jina)</strong></li>
<li>풀 리퀘스트 요청 후, 충돌 확인 후 merge(병합)한다.</li>
<li>이 과정이 끝나면, 내 터미널로 가서 발전된 코드를 업데이트 시켜줄 브랜치로 체크아웃을 한다.</li>
<li>해당 브랜치에서 pull 을 받아온다, <strong>$ git pull upstream 브랜치이름(ex develop)</strong></li>
<li>이후 기존 push 한 브랜치를 삭제하거나 ( <strong>$ git branch -d feature/jina</strong>), 프로젝트 규칙에 맞게 하면 끝~!</li>
</ol>
<hr>
<h3 id="😈😈😈😈😈">😈😈😈😈😈</h3>
<ul>
<li>이때 코드를 수정해서, 기존 코드 상태와 다를때 pull 을 받으려고하면 충돌이 일어난다.</li>
<li>commit || stash 를 해주라는 안내창이 뜨는데, stash 관련 내용은 여기서 확인 가능하다 👉<a href="https://github.com/jina95/TIL/blob/master/%EC%B0%B8%EA%B3%A0%20%EC%9E%90%EB%A3%8C/git-stash.md">https://github.com/jina95/TIL/blob/master/%EC%B0%B8%EA%B3%A0%20%EC%9E%90%EB%A3%8C/git-stash.md</a></li>
</ul>
<hr>

