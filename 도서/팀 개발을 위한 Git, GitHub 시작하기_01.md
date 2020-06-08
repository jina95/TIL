# 팀 개발을 위한 Git, GitHub 시작하기
<hr/>

## CHAPTER 1 : GUI를 위한 버전 관리 환경 구축하기

**🖊01.소스트리 설치하기**
- 설치했을때 호스팅 계정 편집(원격저장소) > 호스팅서비스 :  GitHub / 선호 프로토콜 : HTTPS / 인증 : OAuth

**🖊03.GitHub 둘러보기**

<img src="https://github.com/jina95/TIL/blob/master/images/github%20%EB%91%98%EB%9F%AC%EB%B3%B4%EA%B8%B0.png" width="80%"/>

- Add .gitnore : .gitnore 파일 추가 / 이 옵션에서 선택한 항목에 따라 해당 프로젝트에서 GitHub 에 올리지 않기를 바라는 파일이 자동으로 목록에 추가된다.추후에도 언제든지 .gitnore 파일 만들 수 있음.


## CHAPTER 2 : 혼자서 Git 으로 버전 관리하기

**🖊01.로컬저장소를 소스트리에 불러오기**

<img src="로컬저장소 추가">

**🖊02.소스트리로 커밋 만들고 푸시하기**

- 기존 폴더에 새로운 파일들을 만들고 푸시를 하게되면 밑에와 같은 상황을 확인 할 수있다.

<img src="master origin">

- master 은 로컬저장소버전,  origin/master 은 원격저장소버전이다.
- 우리는 이전에 

<pre><code>- git remote add origin 주소 </pre></code>

- 라는 명령어를 입력했었다. 만약 origin 에 myOrigin 으로 입력했었더라면, origin/master > myOrigin/master 였을것이다.
- origin 이라는 꼬리표는 원격저장소의 현재버전상태를 가리킨다.
- master 이란 우리가 커밋을 올리는 '줄기'의 이름이다. 따로 줄기를 생성하지 않으면 Git 은 master 이라는 기본줄기에 커밋을 올린다.
- 새로만든 커밋을 원격저장소로 업로드 할때는 푸시를 해준다. 이 동작은 

<pre><code>- git push origin master </pre></code>

- 와 같다.

<img src="원격저장소로 push 완료">

**🖊03. 그림으로 Git 뜯어보기**
- 커밋은 Subversion - 델타(차이점만 저장)이 아닌 Git - 스냅샷(전체를 저장)!




