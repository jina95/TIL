# 팀 개발을 위한 Git, GitHub 시작하기
<hr/>

<h2 id="chapter-8--git-내부-동작-원리">CHAPTER 8 : Git 내부 동작 원리</h2>
<p><strong>🖊01. git add 명령의 동작 원리</strong></p>
<p><strong>git-test 폴더 생성 후 로컬저장소 생성</strong></p>
<pre><code>$ pwd     # 현재폴더
$ mkdir git-test    # 빈 폴더 생성
$ cd git-test 
$ git init    # Git 로컬저장소 생성
$ ls -al     # .git 폴더 생성 확인
$ ls -al .git/     # .git 폴더 내부 확인 </code></pre>
<ul>
<li>$ ls -al 명령으로 다양한 폴더가 생성된것을 알 수 있다.</li>
</ul>
<pre><code>-rw-r--r-1 cat-hanbit 197121 23 6월 3 01:00 HEAD </code></pre>

<table>
<thead>
<tr>
<th>명령어</th>
<th>의미</th>
</tr>
</thead>
<tbody>
<tr>
<td>-rw-r–r-1</td>
<td>첫번째 칸은 파일의 권한과 상태, 크게 중요하지 X. '-'로 시작하면 일반파일, 'd’로 시작하면 폴더</td>
</tr>
<tr>
<td>cat-hanbit</td>
<td>파일 소유자의 아이디</td>
</tr>
<tr>
<td>23</td>
<td>파일의 크기, 바이트로 표시, 폴더는 0</td>
</tr>
<tr>
<td>6월3 01:0</td>
<td>파일 생성 시간</td>
</tr>
<tr>
<td>HEAD</td>
<td>파일 이름, 폴더의 경우 / 가 붙음</td>
</tr>
</tbody>
</table><p><strong>git add 와 git status 다시 보는 실습을 위한 저수준의 명령어</strong></p>

<table>
<thead>
<tr>
<th>명령어</th>
<th>의미</th>
</tr>
</thead>
<tbody>
<tr>
<td>git hash-object &lt;파일명&gt;</td>
<td>일반 파일의 체크섬을 확인할때 사용</td>
</tr>
<tr>
<td>git show &lt;체크섬&gt;</td>
<td>해당 체크섬을 가진 객체의 내용 표시</td>
</tr>
<tr>
<td>git ls-files --stage</td>
<td>스테이지 파일의 내용 표시, 스테이지 파일은 git add 명령어를 통해 생성되는데, .git/index 파일이 스테이지 파일임</td>
</tr>
</tbody>
</table><ul>
<li>위의 명령어들은 실제로 많이 쓰이는 명령어는 아니고, 동작 원리를 이해하기 위해 사용하는 명령어</li>
</ul>
<p><strong>파일 생성 및 워킹트리 상태 확인</strong></p>
<pre><code>$ echo "cat-hanbit" &gt; cat.md     # 파일 생성, 내용을 동일하게 만들것
$ git status </code></pre>
<ul>
<li>위와 같이 파일을 생성하고 $ git status 를 하면 파일의 상태가 Untracked라는 것을 알 수 있다.</li>
<li>git status 란 워킹트리와 스테이지, HEAD 커밋 세가지 저장공간의 차이를 비교해서 보여준다.</li>
<li>파일을 생성한 현재상태에서는 working tree 에만 해당파일이 있고, stage 는 비어져 있는 상태이며 한번도 커밋하지 않았기 때문에 HEAD 커밋은 없다.</li>
</ul>
<p><strong>파일 체크섬 확인</strong></p>
<pre><code>$ git hash-object cat.md     # 파일의 체크섬 확인</code></pre>
<p><strong>스테이지에 파일 추가</strong></p>
<pre><code>$ git add cat.md    # 스테이지에 파일 추가
$ git status     # 파일 상태 확인
$ ls -a .git     # .git  폴더 확인, index 가 생성되었다.
$ file .git/index     # .git/index 파일의 정체 확인
$ git ls-files --stage    # 스테이지 파일의 내용 확인  </code></pre>
<ul>
<li>.git 폴더를 보면 index 라는 파일이 생긴것을 알 수 있는데, file 명령어를 통해 .git/index 의 정체를 확인하면 Git index 인것을 알 수 있다.</li>
<li>index 는 스테이지의 다른 이름으로 이 index 파일이 바로 Git의 스테이지 이다.</li>
<li>$ git ls-files --stage 로 스테이지의 내용을 확인하고, <a href="http://cat.md">cat.md</a> 가 들어가 있으며 이전에 확인했던 체크섬과 일치한다.</li>
</ul>
<p><strong>.git 폴더를 이용하여 객체 내용을 확인</strong></p>
<pre><code>$ ls -a .git/objects/     # .git/objects/ 폴더 확인
$ ls -a .git/objects/ff     # .git/objects/ff/ 폴더 확인
$ git show ff5bda     # ff5bda 의 내용을 본다 </code></pre>
<p>-.git/objects/ 밑에 ff 폴더가 생긴것을 확인할 수 있는데, 그 폴더 아래는 아까 확인했던 체크섬과 일치하는 파일명이 존재한다.</p>
<ul>
<li>objects 폴더안에 존재하는 파일들은 Git의 객체이다.</li>
<li>$ git show 명령어로 cat-hanbit 이라는 파일임을 알 수 있다.<br>
<strong>체크섬을 이용해서 객체의 종류와 내용 확인</strong></li>
</ul>
<pre><code>$ git cat-file -t ff5bda     # 체크섬으로 객체의 종류 알아보기 
$ git cat-file blob ff5bda     # 해당 객체의 내용 들여다 보기 </code></pre>
<ul>
<li>$ git cat-file -t &lt;체크섬&gt; 명령어로 객체의 타입을 알려주고, 현재에는 blob 라는 것을 알 수 있다.</li>
<li>blob 란 binary large object 의 줄임말로 스테이지에 올라간 파일은 객체는 blob 이 된다.</li>
<li>$ git cat-file &lt;객체타입&gt; &lt;체크섬&gt; 명령어로 객체의 내용을 들여다 본다. ( 해당 파일의 내용을 표시해 줌)</li>
</ul>
<p><em><strong>git add 명령이 워킹트리에 존재하는 파일을 status 에 추가하는데, 해당 파일의 체크섬 값과 동일한 이름을 가지는 blob 객체가 생성되고 이 객체는 .git/objects 파일에 저장된다. 그리고 스테이지의 내용은 .git/index에 기록된다!!!</strong></em></p>


<p><strong>🖊02. git commit 명령의 동작 원리</strong></p>

**커밋상태 확인**

<pre><code>$ git commit
$ git log
$ git status      # clean 한 상태인것을 알 수 있다
$ ls -a .git/objects     # .git/objects/ 변화 확인
$ ls -a .git/objects/42     # 42b5fe 오브젝트 존재 확인
$ git show 42b5fe     # 42b5fe 오브젝트의 정채는 ? </code></pre>

- 방금 만든 커밋은 .git/objects/42 아래에 있다.
- $ git show 명령어를 통해 42b5fe 객체가 커밋인 것을 알 수 있다.

**스테이지확인**
<pre><code>$ git ls-files --stage     # 스테이지가 비어있지 않다!!
$ git status </code></pre>

- git status 명령은 워킹트리, 스테이지, HEAD 커밋 세 저장공간을 비교한다고 했는데 사실 clean 하다는 말의 뜻은 **워킹트리와 스테이지, 그리고 HEAD 커밋의 내용이 모두 똑같다** 라는 뜻이다.

**수상한 객체 확인**
<pre><code>$ ls -a .git/objects
$ ls -a .git/objects/76/      # object 폴더 내용확인
$ git show 76f6787     # 76f6787 객체는 무엇인가?
$ git ls-tree 76f6787     # 트리 객체의 내용은?
$ git ls-files --stage     # 스테이지도 확인
$ git log --oneline -n1     # 커밋 체크섬 확인
$ git cat-file -t 42b5fed     # 커밋 객체 타입 확인
$ git cat-file commit 42b5fed     # 커밋 객체 내용 확인 </code></pre>

> 책에서는 모두가 7a 일거라고 했는데 나는 76 이었다...
- $ git show 명령어를 통해 tree 임을 확인.  tree 객체 내용을 확인해 봤을 때 내용이 스테이지와 동일.
- 커밋 객체의 체크섬을 이용해 타입을 확인해 보면 commit 임을 알 수 있다
- 이 커밋객체의 내용에는 커밋메세지와 트리 객체로 구성 되어 있음을 알 수 있고, 트리 객체의 체크섬은 위에 $ ls -a .git/objects/76/ 에서 확인한 내용과 같다.

**위의 내용 요약**
1. 커밋을 하면 스테이지의 객체로 트리가 만들어 진다.
2. 커밋에는 커밋메세지와 트리객체가 포함된다.

<img src="https://github.com/jina95/TIL/blob/master/images/%EB%8F%84%EC%84%9C/%EC%BB%A4%EB%B0%8B%EB%8B%A4%EC%9D%B4%EC%96%B4%EA%B7%B8%EB%9E%A8.png"  width="70%">


**🖊03. 수동 커밋하며 살펴보기**

**파일 내용 수정하고 파일 체크섬 확인**
<pre><code>$ cat cat.md
$ git hash-object cat.md     # 체크섬(ff5bda)
$ echo "Hello, cat-hanbit" >> cat.md     # cat.md 파일에 텍스트 추가
$ git hash-object cat.md     # 변경된 체크섬 확인(f3e6fa)
$ git ls-files --stage     # 스테이지의 파일 확인
100644 ff5bda20472c44e0b85e570185bc0769a6adec68 0  cat.md (위에 변경된 체크섬과 다른것을 알 수 있다, 기존 체크섬)
$ git ls-tree HEAD     # 헤드 커밋의 내용 확인 </code></pre>
- 아직 변경사항을 스테이지에 추가하지 않았기 때문에 현재폴더, working tree의 체크섬만 다르다.
- 변경된 파일을 "modified" 라고한다. 스테이지와 워킹트리의 내용이 다른 파일을 일컫는 말.

**변경내용 스테이지에 추가**
<pre><code>$ git add cat.md
$ git ls-files --stage </code></pre>

<img src="https://github.com/jina95/TIL/blob/master/images/%EB%8F%84%EC%84%9C/add-stage%EA%B9%8C%EC%A7%80%20%EC%98%AC%EB%9D%BC%EA%B0%84.png" width="70%">

**수동으로 트리만들기**
<pre><code>$ git write-tree     # 트리 생성 (da5c3)
$ git ls-tree da5c3     # 생성된 트리 객체 확인 
100644 blob f3e6fa5c881ffb692cf2f2353dc2e90ce5a207f8  cat.md </code></pre>

- 생성된 트리객체를 확인해 보면, 스테이지의 내용과 같다는것을 알 수 있다.

**트리로 커밋하기**
<pre><code>$ echo "트리로 커밋하기" | git commit-tree da5c3 -p HEAD     # 트리로 커밋 생성
ddb2751801b9c3d7dc5cee87c54f5ad034cd4f0d
$ git cat-file commit ddb27     # 생성된 커밋 확인
$ git log --oneline    # 커밋 로그 확인 </code></pre>

- $ git commit-tree 명령을 이용하면 트리객체를 이용해서 직접 커밋을 생성할 수 있다. 
- echo = 커밋메세지 생성 / da5c3 = 트리 객체 체크섬  / -p HEAD = 부모커밋이 HEAD임을 알려준다. / -p (부모를 지정해주는 옵션)
- 하지만 커밋 로그 확인을 했을때 우리가 생성한 커밋이 나오지 않는다. 
- 이유는 HEAD가 갱신되지 않았기 때문!!!
- git commit 명령은 이전 HEAD를 부모로하는 커밋 객체를 생성한 후 방금만든 새 커밋이 새로운 HEAD가 된다.그런데 우리가 만든 커밋은 HEAD를 갱신하지 않는다. 아래와 같이 갱신해보자.

**HEAD 갱신하기**
<pre><code>$ ls .git     # .git 폴더 목록 확인
$ cat .git/HEAD     # HEAD 파일의 내용 확인
$ cat .git/refs/heads/master     #  refs/heads/master 내용 확인
$ git update-ref refs/heads/master ddb27     # 직접 커밋한 객체로 업데이트
$ cat .git/refs/heads/master     # 업데이트 확인
$ git log --oneline     # 로그 확인 
ddb2751 (**HEAD ->** **master**) 트리로 커밋하기
42b5fed 커밋 확인용 커밋 </code></pre>

- update 전 refs/heads/master 내용은 HEAD 커밋의 체크섬과 같은 값(42b5fed)
- $ git update-ref 명령어를 이용해서 위의 내용을 새로운 커밋의 체크섬값으로 변경

<img src="https://github.com/jina95/TIL/blob/master/images/%EB%8F%84%EC%84%9C/HEAD%EA%B0%B1%EC%8B%A0%ED%95%98%EA%B8%B0.png" width="70%">

**중복파일 관리**
- 같은 내용의 커밋 관리하기
<pre><code>$  cp cat.md  cat2.md     # 파일복사
$ echo "cat-hanbit" > cat3.md     # 이전 버전과 같은 내용의 파일 생성
$ git add cat2.md cat3.md     # 전부 스테이지에 추가
$ git ls-files --stage    # 스테이지 내용 확인
100644 f3e6fa5c881ffb692cf2f2353dc2e90ce5a207f8 0  cat.md
100644 f3e6fa5c881ffb692cf2f2353dc2e90ce5a207f8 0  cat2.md
100644 ff5bda20472c44e0b85e570185bc0769a6adec68 0  cat3.md
$ git commit     #  커밋 </code></pre>

- git 에서는 파일이 blob으로 관리가 되는데, git 의 blob은 생성날짜와는 상관없이 내용이 같을경우 같은 체크섬을 가지게 된다.

**git add 명령은 워킹트리의 내용을 스테이지에 반영하는 것이고, git commit 명령은 스테이지의 내용을 가지고 트리객체를 만들고 이 트리객체를 기반으로 기존 HEAD커밋을 부모로 하는 새로운 커밋을 만든다. 마지막으로 생성된 커밋은 다시 HEAD가 된다.**


**🖊04. 브랜치 작업 살펴보기**

**브랜치 생성하고 확인해보기**
<pre><code>$ git branch test     # 브랜치 생성
$ git log --oneline     # 생성된 브랜치 확인
$ ls .git/refs/heads/    # .git 폴더 내부
master  test
$ cat .git/refs/heads/test     # 실제 파일 내용 확인
7776ba95364d949cd9b9dbd2b3c512083906277b </code></pre>

- 브랜치를 생성할 때 커밋을 지정하지 않았기 때문에 HEAD 커밋으로부터 test가 생성됨.
- $ ls .git/refs/heads/ 로 폴더를 살펴보았을때, test 파일이 생긴것을 알 수 있다.
- test 에 HEAD커밋의 전체 체크섬 내용이 들어있음.
- <strong>브랜치는 커밋의 참조일 뿐이다. </strong> 위의 텍스트 한줄이 브랜치의 전부. $ git branch test <커밋 체크섬> 명령을 실행하면 내부적으로는 <커밋 체크섬> 내용을 가지는 .git/refs/heads/test 텍스트 파일 하나를 생성하는 것.

> 아직 이 부분이 잘 이해가 되지 않는다....

**브랜치 삭제 및 재생성**
<pre><code>$ git branch -d test     # test 브랜치 삭제
$ ls .git/refs/heads/     # 브랜치 폴더 목록 확인
master
$ git branch test2     # test2 브랜치 생성
$ ls .git/refs/heads/     # 브랜치 폴더 목록 확인
master test2
$ git log --oneline -n1     # 로그 확인
$ rm .git/refs/heads/test2     # 브랜치 파일 삭제
$ git log --oneline -n1      # 다시 로그 확인 </code></pre>
- rm명령으로 파일 삭제


**브랜치 체크아웃**
**git checkout 관찰하기**
<pre><code>$ git branch test HEAD^     # 현재 HEAD의 부모 커밋으로부터 test3 브랜치를 만든다.
$ git log --oneline -n2     # 로그 확인
$ cat .git/HEAD     # 체크아웃 전 HEAD 파일 확인
refs/heads/master
$ git checkout test3     # 체크아웃
$ cat .git/HEAD     # HEAD 파일 변경사항 확인
refs/heads/test3
$ git stauts      # 워킹트리 확인 </code></pre>

- HEAD^ 와 HEAD~ 둘다 HEAD의 부모커밋의미
- $ cat .git/HEAD 로 내용을 살펴봤을때 refs/heads/master 와 refs/heads/test3 의 차이점을 볼 수있다.
- $ git stauts 명령을 보면 clean 한 상태로 워킹트리, 스테이지 모두 test3 내용으로 변경된 것을 알 수 있다.
-  <strong>체크아웃은 ' 해당 브랜치로 HEAD를 이동시키고 스테이지와 워킹트리를 HEAD가 가리키는 커밋과 동일한 내용으로 변경하는것</strong>


**수동 체크아웃**
<pre><code>$ echo "ref: refs/heads/master" > .git/HEAD     # HEAD 파일 직접 수정
$ git log --oneline -n1     # 로그 확인
$ git status     # 상태보기
$ git reset --hard     # hard reset 수행
$ git status     #  다시 상태 확인</code></pre>

- $ git reset --hard 명령을 하게 되면, 커밋 스테이지 워킹트리 의 내용이 모두 같아지게 된다.
- $ git checkout master 명령을 수행한 것과 동일한 상태.

**이번장에서 배운 것들**
1. git add 명령을 수행하면 워킹트리의 내용을 스테이지에 추가한다.
2. git commit 명령을 수행하면 스테이지의 내용으로 새로운 커밋을 만든다.
3. 커밋 이후 git status 명령을 내리면 clean 한 상태임을 표시해주는데, 이것은 working tree, stage, HEAD 커밋들이 모두 동일한 내용을 담고있다는 뜻.
4. 커밋객체는 트리객체와 blob 객체들의 조합을 이루어져 있다.
5. 커밋객체는 부모커밋에 대한 참조를 가지고 있다.
6. 브랜치를 생성하면 단순히 브랜치 파일 하나를 추가한다.
7. 브랜치를 체크아웃하면 HEAD를 해당 브랜치로 변경하고 브랜치가 참조하는 커밋의 내용으로 스테이지와 워킹트리의 내용을 변경한다.


## CHAPTER 9 : 인증 기능 살펴보기

**🖊01. 인증 관련 기능 사용하기**
