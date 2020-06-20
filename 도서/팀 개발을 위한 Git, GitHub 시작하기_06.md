---


---

<h1 id="팀-개발을-위한-git-github-시작하기">팀 개발을 위한 Git, GitHub 시작하기</h1>
<hr>
<h2 id="chapter-6--part-1에서-수행했던-기본-명령어">CHAPTER 6 : PART 1에서 수행했던 기본 명령어</h2>
<p><strong>🖊01. 왜 CLI를 사용할까?</strong></p>
<p><strong>🖊02. Git Bash를 시작하자</strong></p>
<ul>
<li>$ 기호와 표시된 경로등을 합쳐서 : 프롬프트(prompt)</li>
<li><strong>프롬프트</strong>는 CLI에서 가장 기본적인 정보를 보여준다.</li>
<li>프롬프트 끝에 브랜치명이 보인다면 Git 작업 폴더임을 의미</li>
</ul>
<p><strong>Git Bash 명령어</strong></p>

<table>
<thead>
<tr>
<th>명령어</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>pwd</td>
<td>현재 폴더 위치 확인</td>
</tr>
<tr>
<td>ls -a</td>
<td>현재 폴더 위치 확인</td>
</tr>
<tr>
<td>cd</td>
<td>홈 폴더로 이동(홈 폴더는 사용자 이름과 폴더명이 같고 내 문서 폴더의 상위폴더)</td>
</tr>
<tr>
<td>cd 폴더이름</td>
<td>특정 위치의 디렉토리로 이동</td>
</tr>
<tr>
<td>cd …/</td>
<td>현재 폴더의 상위폴더로 이동</td>
</tr>
<tr>
<td>mkdir 새폴더이름</td>
<td>현재 폴더의 아래에 새 폴더를 만듬</td>
</tr>
<tr>
<td>echo “Hello Git”</td>
<td>메아리라는 뜻, 화면에 ""안의 문장인 "Hello Git"을 표시</td>
</tr>
<tr>
<td>git status</td>
<td>Git 워킹트리의 상태를 보는 명령으로, 매우 자주 사용 / 워킹트리가 아닌 폴더에서 사용하면 오류 발생</td>
</tr>
<tr>
<td>git status -s</td>
<td>git status 명령보다 짧게 요약해서 상태를 보여주는 명령으로, 변경된 파일이 많을 때 유용</td>
</tr>
<tr>
<td>git init</td>
<td>현재 폴더에 Git 저장소를 생성. 현재 폴더에는 [ .git ] 이라는 숨김 폴더가 생성되는데 사실 이 폴더가 로컬저장소이다.</td>
</tr>
<tr>
<td>git reset 파일명</td>
<td>스테이지 영역에 있는 파일을 스테이지에서 내린다.(언스테이징), 워킹트리의 내용은 변경되지 않으며 옵션을 생략할 경우 스테이지의 모든변경사항을 초기화한다.</td>
</tr>
<tr>
<td>git log</td>
<td>현재 브랜치의 커밋 이력을 보는 명령어(HEAD와 관련된 커밋이 자세히 나온다)</td>
</tr>
<tr>
<td>git log -n숫자</td>
<td>전체 커밋 중에서 최신 n개의 커밋만 살펴본다</td>
</tr>
<tr>
<td>git log --oneline</td>
<td>간단한 커밋 해시와 제목만 보고싶을때</td>
</tr>
<tr>
<td>git log --online --graph --decorate</td>
<td>HEAD와 관련된 커밋을 조금 더 자세히 보고싶을때</td>
</tr>
<tr>
<td>git log --online --graph --all --decorate</td>
<td>모든 브랜치를 보고 싶을때</td>
</tr>
<tr>
<td>git help 명령어</td>
<td>ex git help commit, git help status 처럼 명령어의 도움말이 표시함</td>
</tr>
<tr>
<td>git remote add 원격저장소이름 원격저장소주소</td>
<td>원격저장소 등록, 같은 별명의 원격저장소는 하나만 가질 수 있고 통상 첫번째는 원격저장소를 origin 으로 저장</td>
</tr>
<tr>
<td>git remote -v</td>
<td>원격저장소 목록을 살펴봄</td>
</tr>
</tbody>
</table><p><strong>Git 용어정리</strong></p>

<table>
<thead>
<tr>
<th>용어</th>
<th>설명</th>
</tr>
</thead>
<tbody>
<tr>
<td>워킹트리</td>
<td>워킹트리, 워킹 디렉토리, 작업 디렉토리, 작업 폴더 모두 같은 뜻으로 사용.일반적으로 사용자가 파일과 하위폴더를 만들고 작업 결과물을 저장하는 곳을 Git에서는 워킹트리라고 부름. 공식문서에서는 워킹트리를 '커밋을 체크아웃 하면 생성되는 파일과 디렉토리’로 정의. 정확하게는 작업 폴더에서 [ .git ] 폴더(로컬저장소)를 뺀 나머지 부분이 워킹트리 / <strong>일반적인 작업이 일어나는 곳</strong></td>
</tr>
<tr>
<td>로컬 저장소</td>
<td>Git init 명령으로 생성되는 [ .git ] 폴더가 로컬저장소. 커밋, 커밋을 구성하는 객체, 스테이지가 모두 이 폴더에 저장 / <strong>.git 폴더, 커밋은 여기에 들어있다.</strong></td>
</tr>
<tr>
<td>원격 저장소</td>
<td>로컬저장소를 업로드 하는곳을 원격저장소라고 함. 우리가 사용하고 있는 GitHub 저장소가 원격저장소</td>
</tr>
<tr>
<td>Git 저장소</td>
<td>Git 명령으로 관리할 수 있는 폴더 전체를 일반적으로 Git 프로젝트 혹은 Git 저장소라고 부름. 일반적으로 Git 저장소를 워킹트리 + 로컬저장소의 느낌으로 사용하지만 공식문서에서는 로컬저장소와 Git 저장소를 같은 뜻으로 사용. / <strong>엄밀하게는 로컬저장소를 의미하지만 넓은의미로 작업폴더를 의미하기도 함</strong></td>
</tr>
</tbody>
</table><ul>
<li>작업폴더 = 워킹트리 + 로컬저장소</li>
</ul>
<p><strong>Git 로컬저장소를 위한 새폴더 만들기</strong></p>
<pre><code>$ mkdir 폴더이름     # 새폴더를 만든다
$ cd 만든폴더이름/     # 만든 폴더로 이동한다
$ pwd     # 현재 어디에 있는지 확인</code></pre>
<p><strong>Git 저장소 초기화</strong></p>
<pre><code>$ git init     # git 저장소를 생성
$ ls -a     # 무슨 파일이 있는지 목록 확인
$ git status     # 워킹트리 상태 확인</code></pre>
<ul>
<li>git init 을 하기전에 status 를 했을때는 에러가 떳었다. 단, 기존 git 폴더 밑 하위폴더라면 status 에러가 뜨지 않는다.</li>
</ul>
<p><strong>Git 전역옵션 설정</strong></p>
<pre><code>$ git config --global user.name     
#기존에 나는 설정을 해놔서 이렇게 치면 내 이름이 뜨는데 안 뜰 경우엔 
$ git config --global user.name "이름"   # 로 설정해줘야한다.</code></pre>
<p><strong>Git 기본에디터 확인</strong></p>
<pre><code>$ git config core.editor     
$ git config  --global core.editor   
$ git config  --system core.editor       </code></pre>
<blockquote>
<p>-비쥬얼 스튜디오 코드랑 git 이 연결이 안되서 헤맸는데 vscode 에서 보기 &gt; 명령팔레트 &gt; shell command &gt; 셸 명령 PATH에 ‘code’ 명령 설치를 눌러주고 나서는 해결되었다</p>
</blockquote>
<p><strong>🖊03. 기본 CLI 명령어 살펴보기</strong></p>
<p><strong>간단한 텍스트 파일 생성하고 확인하기</strong></p>
<pre><code>$ echo "hello git"     # 화면에 큰 따옴표("")안에 텍스트를 보여준다.     
$ echo "hello git" &gt; file1.md     # 큰 따옴표 안의 텍스트로 파일 생성
$ ls     # 현재폴더 파일 목록 확인
$ git status     # 상태를 확인할 수 있다
#현재는 위에서 파일이 생성됬지만, 스테이지에 올라가지 않은것을 알 수 있다.     </code></pre>
<p><strong>생성한 파일 스테이지에 추가하기</strong></p>
<pre><code>$ git add file1.md     
$ git status     # 파일이 스테이지 영역에 추가 된 것을 알 수 있다.     </code></pre>
<p><strong>스테이지에서 파일 언스테이징 하기</strong></p>
<pre><code>$ git status     # 현재 파일이 올라간 상태라면     
$ git reset file1.md     # 언스테이징
$ git status     # 파일이 내려간것을 볼 수있다.
$ cat file1.md     # cat 을 앞에 붙여주면 뒤에 파일을 터미널 화면에 뿌려준다.   </code></pre>
<p><strong>첫번째 커밋 생성</strong></p>
<pre><code>$ git commit     # 커밋 실행, vscode가 열리면 커밋메세지 입력후 저장&amp;닫기   </code></pre>
<ul>
<li>vscode 가 열리고 첫째줄에는 작업내용의 요약(제목), 다음줄에는 자세하게 작업내용을 기록(본문)하는데 첫번째 줄과 둘째줄 사이에는 반드시 한줄을 비워야 한다.</li>
<li>vscode 종료</li>
<li>만약 vscode가 열렸는데 커밋하고 싶지 않아진다면, 그냥 vscode를 종료해도 된다 (커밋 취소됨)</li>
</ul>
<p><strong>커밋 확인해보기</strong></p>
<pre><code>$ git status     #깨끗한상태임을 알려준다
$ git log --oneline --graph --all --decorate </code></pre>
<img src="git log">
<p><strong>좋은 커밋 메세지의 7가지 규칙</strong></p>
<ol>
<li>제목과 본문을 빈 줄로 분리한다.</li>
<li>제목은 50자 이내로 쓴다.</li>
<li>제목을 영어로 쓴 경우 첫 글자는 대문자로 쓴다.</li>
<li>제목에는 마침표를 넣지 않는다.</li>
<li>제목을 영어로 쓴 경우 동사원형(현재형)으로 시작한다.</li>
<li>본문을 72자단위로 줄바꿈한다.</li>
<li>어떻게 보다 무엇과 왜를 설명한다.</li>
</ol>
<p><strong>🖊04. 원격저장소 관련 CLI 명령어</strong></p>
<p><strong>원격저장소 등록 및 push</strong></p>
<pre><code>$ git remote add origin 주소     
$ git remote -v
$ git push </code></pre>
<ul>
<li>위와 같이 push를 하게 되면 밑에와 같은 에러가 뜬다.</li>
</ul>
<img src="git push error">
<ul>
<li>업스트림 브랜치는 로컬저장소와 연결된 원격저장소를 일컫는 단어이다.</li>
<li>업스트림 브랜치 설정을 위해 에러메세지가 알려준대로 --set-upstream 을 쓰거나 단축 명령인 -u 옵션을 사용</li>
<li>이후에는 origin 저장소의 master 브랜치가 로컬저장소의 master 브랜치의 업스트림으로 지정되어 에러없이 push 가능해진다.</li>
</ul>
<p><strong>git push 재시도</strong></p>
<pre><code>$ git push -u origin master      # push 와 동시에 업스트림 지정     
$ git log --oneline -n1
$ git push </code></pre>
<p><strong>git clone 사용해보기</strong></p>
<pre><code>$ pwd     
$ cd ../     # 반드시 상위 디렉토리로 이동할 것!
$ git clone 클론할주소 새로운폴더명
$ ls
$ cd 새로운폴더명
$ git log --oneline
$ git remote -v     # 원격저장소 목록 확인</code></pre>
<p><strong>추가 commit and push</strong></p>
<pre><code>$ echo "second" &gt; file1.md     # 파일에 내용 한 줄 추가    
$ cat file1.md   
$ git commit -a     # 스테이징 없이 바로 커밋
$ git push
$ git log --oneline </code></pre>
<p><strong>git pull</strong></p>
<pre><code># 처음저장소로 이동     
$ git log --oneline      # 결과물을 보면 커밋은 하나뿐  
$ git pull
$ git log --oneline     # 첫번째, 두번째 커밋 확인 가능
$ cat file1.md     # 클론, 기존 내용이 합쳐진 것을 확인할 수 있다.
</code></pre>

