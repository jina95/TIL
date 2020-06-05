# 팀 개발을 위한 Git, GitHub 시작하기
<hr/>

## CHAPTER 1 : 빠른 실습으로 Git, GitHub 감 익히기

**🖊01.Git, 그리고 GitHub**
- Git은 소스코드 버전 사이를 오고가는 시간 여행이상의 기능을 제공
- 이렇게 Git 으로 관리하는 프로젝트를 올려둘 수 있는 Git 호스팅 사이트 중 하나가 바로 GitHub
- 누구든지 기여할 수 있는 공개저장소 프로젝트 > 오픈소스

**🖊02.Git을 설치하고 로컬저장소에서 커밋 관리하기**
- git 설치하는 페이지로 들어갔는데, homebrew 를 설치해야 할 것 같아서 [homebrew](https://brew.sh/index_ko) 에서 설치함
- 책과는 약간 달라서 이 [주소](https://nillk.tistory.com/1) 코드를 참고하였다.
- 그랬더니 책과 같이 git 을 쳤을때 화면이 같아짐!
- 터미널에서 파일 경로로 들어갈때 커맨드누르면서 폴더를 드래그 하면 경로가 자동으로 입력!
- bash 에서 실행 : 

<pre><code>
- git init
- git config --global user.email "내이메일"
- git config --global user.name "내이름"
</pre></code>

- 위에 부분에서 해맸다.. user.email 이후에 내 이메일을 넣어야함!

<pre><code>
- git add README.text
- git commit -m "사이트 설명 추가"
내용을 수정한다. 
- git add README.text
- git commit -m "설명 업데이트"
</pre></code>


<pre><code>
- git log 
</pre></code>

- 하면 위에 커밋한 두개를 확인할 수있고 앞의 아이디를 복사해서 

<pre><code>
- git checkout 8081393(아이디 전체 넣어도 됨) 
- git checkout -
</pre></code>

- 첫번째 처럼 하면 해당 아이디, 즉 책에서 말하는 시간여행이 가능하다 (해당하는 아이디의 상태로 돌아갈 수 있다.)
- 두번째처럼 하면 최신커밋으로 돌아간다.


