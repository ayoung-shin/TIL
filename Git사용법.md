# Git

> Git은 분산형버전관리시스템(DVCS)이다
>
> 소스코드 형상 관리 도구로, 코드의 이력을 관리 할 수 있다.

## Git 로컬 저장소 활용하기

> git은 `repository(저장소)`로 각각 프로젝트를 관리한다.

### 0. 기본 설정

Git에 이력을 남기기 위해 작성자(author) 정보를 추가한다. 매 컴퓨터에서 최초로 한 번만 설정 하면 된다.

``` bash
$ git config --global user.name {유저네임}
$ git config --global user.email {이메일}
```

* 일반적으로 `{유저네임}`, `{이메일}` 에는 github 정보를 넣는다.

```bash
$ git config --global -l
```

* 연결된 github 계정을 확인할 수 있다.

### 1. 저장소  생성

* git 초기화 성공 했을 경우 뜨는 말

```bash
$ git init
Initialized empty Git repository in C:/Users/student/Desktop/새 폴더 (2)/.git/

```

* git 상태를 보는 코드와 결과
  * 오류가 났을 경우 어떤 상태인지 볼 수 있음.

```bash
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        "Git\354\202\254\354\232\251\353\262\225.md"
        image/
        "\353\247\210\355\201\254\353\213\244\354\232\264 \355\231\234\354\232\251\353\262\225.md"

nothing added to commit but untracked files present (use "git add" to track)
```

*  git에 추가하고 다시 상태보기

```bash
$ git add .

student@M13031 MINGW64 ~/Desktop/TIL (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   "Git\354\202\254\354\232\251\353\262\225.md"
        new file:   "image/\353\247\210\355\201\254\353\213\244\354\232\264.png"
        new file:   "\353\247\210\355\201\254\353\213\244\354\232\264 \355\231\234\354\232\251\353\262\225.md"
```

* `보기>숨긴항목표시`하여 `.git` 파일이 있는 폴더에서 `Git Bash Here` 실행

## 2. add

> 커밋 대상 파일을 `staging area` 로 이동 시킨다.
>
> 즉, 이력을 남길 파일을 담아 놓는 것이다.

