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

```bash
$ git commit -m 'Git 기초'
[master (root-commit) ff907cd] Git 기초
 3 files changed, 89 insertions(+)
 create mode 100644 "Git\354\202\254\354\232\251\353\262\225.md"
 create mode 100644 "image/\353\247\210\355\201\254\353\213\244\354\232\264.png"
 create mode 100644 "\353\247\210\355\201\254\353\213\244\354\232\264 \355\231\234\354\232\251\353\262\225.md"
```

```bash
student@M13031 MINGW64 ~/Desktop/TIL (master)
$ git add .

student@M13031 MINGW64 ~/Desktop/TIL (master)
$ git status
On branch master
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   "Git\354\202\254\354\232\251\353\262\225.md"


student@M13031 MINGW64 ~/Desktop/TIL (master)
$ git commit -m 'Git 기초'
[master f0ff3a3] Git 기초
 1 file changed, 81 insertions(+)
```



`.` 은 현재 디렉토리(폴더)를 뜻한다.

```bash
$ git add .       # 특정 디렉토리 모두 stage
$ git add git.md  # 특정 파일만 stage
$ git add images/ # 특정 폴더만 stage
```

항상 `git status` 명령어를 통해 상태를 확인하자.

## 3. commit

> git에서 이력을 남기기 위해서는 커밋을 진행

* 파일을 추가한 경우

```bash
$ git commit -m 'Git 기초'
[master (root-commit) ff907cd] Git 기초
 3 files changed, 89 insertions(+)
 create mode 100644 "Git\354\202\254\354\232\251\353\262\225.md"
 create mode 100644 "image/\353\247\210\355\201\254\353\213\244\354\232\264.png"
 create mode 100644 "\353\247\210\355\201\254\353\213\244\354\232\264 \355\231\234\354\232\251\353\262\225.md"
```

* 파일 추가 없이 변경된 경우

``` bash
$ git commit -m 'Git 기초'
[master f0ff3a3] Git 기초
 1 file changed, 81 insertions(+)
```

> 이력을 확인하기 위해서는 `git log` 를 활용한다.

```bash
$ git log
commit f0ff3a3fc01949a82b2a5131b646885ecef7b0e8 (HEAD -> master, origin/master)
Author: ayoung-shin <ayoungs486@naver.com>
Date:   Thu Dec 5 12:40:07 2019 +0900

    Git 기초

commit ff907cdafe78fa376219a15b88a1120355ecf78f
Author: ayoung-shin <ayoungs486@naver.com>
Date:   Thu Dec 5 12:37:02 2019 +0900

    Git 기초
```

# Git 원격 저장소 활용하기

## 0. 기존 설정

> 원격 저장소를 생성한다. (예 - github)

## 1. 원격 저장소 등록

`origin` 이라는 이름으로 해당 url을 원격 저장소로 등록

최초에 한번만 하면 된다.

```bash
git remote add origin https://github.com/ayoung-shin/TIL.git # 원격 저장소를 저장
```

```bash
$ git remote -v # 원격 저장소 이름 확인
origin  https://github.com/ayoung-shin/TIL.git (fetch)
origin  https://github.com/ayoung-shin/TIL.git (push)
```

## 2. 원격 저장소 push

앞으로 변경되는 사항이 있으면 항상 add, commit, push를 진행한다.

```bash
$ git push -u origin master
Enumerating objects: 9, done.
Counting objects: 100% (9/9), done.
Delta compression using up to 4 threads
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 4.13 KiB | 1.38 MiB/s, done.
Total 9 (delta 0), reused 0 (delta 0)
To https://github.com/ayoung-shin/TIL.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```

* 코드 복사해서 add, commit, push 한 번에 진행하기

```bash
git status  
```

  입력하여 먼저 상태 확인하고 다음 진행하기

```bash
git add .
git commit -m 'Git 기초'
git push -u origin master
```



# 강사님 github

<https://github.com/edutak/TIL-a>

# 참고 MOOC

coursera - ML/DL (대학원론수업 느낌)

udacity - ML (조금 쉽게 다가감)

edx

모두를 위한 딥러닝