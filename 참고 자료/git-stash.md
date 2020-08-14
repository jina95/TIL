# 💡Git  Stash

- 브랜치에서 파일을 수정하거나, 추가한 후 커밋하지 않고 pull 을 받으려고 하면 commit 또는 stash 를 하라는 알림을 볼 수 있다.

- 이때 stash 를 이용하면, 내용을 따로 보관 한 뒤, pull 이후에 적용할수도, 삭제할수도 있다.

<pre><code>$ git stash # 스테이시로 안전하게 보관

$ git stash list # 스테이시 목록 조회

$ git stash pop # 저장내용 복구, 저장내용을 현재 브랜치에 적용

$ git stash apply # 스테이시에 저장된 가장 최근의 내용을 복원

$ git stash apply stashID(해당아이디) # 스테이시에 저장된 목록중 해당 아이디를 복원

$ git stash drop # 스테이시에 저장된 가장 최근의 내용을 삭제

$ git stash clear # 스테이시 기록 모두 제거

$ git stash -u # 새롭게 추가한 파일도 스테이시에 저장 </code></pre>

<hr>
  
### 😈😈😈😈😈😈

<img src="https://github.com/jina95/TIL/blob/master/images/%EC%B0%B8%EA%B3%A0%EC%9E%90%EB%A3%8C/git%20stash%20list%20.png" width="80%">

  

- $ git stash list 를 입력하면, 위와 같은 화면을 볼 수 있다.

- 이때 drop 하고 싶다면, $ git stash drop stash@{0} 이런식으로 특정 아이디를 입력해 줘야 한다.

- 그렇지 않다면, 나중에 저장한 것 부터 차례대로 지워진다.

  
<hr>

### 😈😈😈😈😈😈

- $ git stash -u >> stash 는 git add 로 한번 이라도 영역에 트래킹 된 파일만 저장 가능하기 때문에, 새로운 파일은 해당 명령어를 통해 저장해 줘야 한다.

<hr>
  

- 참고사이트 : https://suwoni-codelab.com/git/2018/04/06/Git-stash/

- 참고사이트 : https://mylko72.gitbooks.io/git/content/_stash.html
