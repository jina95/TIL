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
