# 10979 module4 WordPress 생성

- [WordPress 만들기(Azure)](#wordpress-만들기(azure))
- [Azure에서 사용한 비용보기](#azure에서-사용한-비용보기)
- [클라우드 없이 WordPress 설치하기](#클라우드-없이-wordpress-설치하기)
- [WP slot 추가하기](#wp-slot-추가하기)
- [WP Swap 하기](#wp-swap-하기)

----

- WordPress : WebApp
- WebApp : Pass 서비스(웹서버까지 올라가 있음)

![image-20191209184705562](image/image-20191209184705562.png)

## WordPress 만들기(Azure)

  > Create -> 
  >
  > > App name : 이니셜-WP (도메인 주소 : 이니셜-VP.azurewebsites.net)
  > >
  > > Subscription : Azure Pass -스폰서쉽
  > >
  > > Resource Group : say-WP-test
  > >
  > > Database Provider : Azure Database for MySQL
  >
  > App Service plan/Location  -> Create new -> 
  >
  > > App Service plan : 이니셜-EastUS
  > >
  > > Location : East US
  > >
  > > Pricing tier
  > >
  > > > Dev/Test(개발&테스트)
  > > >
  > > > Production(실제서비스)
  > > >
  > > > Isolated(전용서버, 서버를 분리시켜줌)
  > >
  > > Production : S1 -> Apply -> OK ->
  > >
  > > Data base
  > >
  > > > Server name : say-wp-mysqldbserver
  > > >
  > > > Server admin login name : mysqldbuser
  > > >
  > > > Password : Pa55w.rd
  > > >
  > > > Version : 5.7
  > > >
  > > > Pricing tier : vCore:2, Strage:33GB
  > > >
  > > > Database name : mysqldatabase7442
  > >
  > > -> OK
  >
  > -> Create


## Azure에서 사용한 비용보기

  - 메뉴 -> Subscription
  - www.azure.com/free : 12개월동안 무료로 사용가능한 계정 생성가능, 20만원 가량 가능(단, 신용카드 등록 필요)
    - 12개월 이상 되거나 한도를 넘는 경우 자동으로 신용카드 결제 진행

## WordPress 시작하기(Azure)

  > Home -> 이니셜-WP-test -> 이니셜-WP -> URL 복사해서 인터넷에 복사해서 넣기 
  >
  > -> 한국어 -> 계속 -> 정보 입력하기 -> 워드프레스 설치하기 -> 로그인 -> 구글 참조해서 원하는데로 setting 가능

## 클라우드 없이 WordPress 설치하기

  > Aparche설치 -> PHP 설치 -> SQL 설치 
  >
  > -> WordPress 설치(개발하기 위해서 최소 3년 필요)

  APM = Apache + PHP + mySQL

  cf ) 워드프레스 사용 동호회 존재

  cf )

  - Visual Studio : 유료이지만 여러회사에서 협업하여 개발하기 좋다.
  - Visual Studio Code : 무료로, 협업할 수 있는 기능이 없다.

  > 메뉴 -> extension -> 원하는 코드 기능 받아서 사용가능 -> azure 검색 -> Azure Tools 다운
  >
  > -> azure 클릭 -> sign in to Azure
  >
  > => 별도의 설정 필요없이 확장프로그램 설치로 해당 언어를 사용할 수 있다.

  ## WP slot 추가하기

  > Azure portal -> Home -> 이니셜-WP-test -> 이니셜-WP -> Deployment slots -> Add a slot ->
  >
  > > Name : new-slot
  > >
  > > Clone settings from : 이니셜-wp
  >
  > -> close

Deployment slots

  -  slot에서 업데이트 할 내용을 한번에 저장해서 서비스 페이지와 순식간에 swaping(바꿔치기)하여 끊김없이 업데이트 서비스를 제공할 수 있게 도와준다.

cf ) visual studio에서 실시간으로 바로 수정 가능 하지만, 여러 페이지에 걸쳐 수정하여야 할 때 실시간으로 업데이트를 할 경우 에러가 나는 경우가 발생할 가능성이 높다.

cf ) production 표시가 들어간 slot이 서비스 중인 slot이다.

  ## WP Swap 하기

  > new-slot -> Swap -> Source : 이니셜-wp-new-slot, Target : 이니셜-wp -> Swap -> Close

  > Azure -> WP-test -> Deployment slots
  >
  > > Custom domains : 신청한 도메인을 WP에 적용시키는 것 (production 이상에서 제공되는 서비스)
  > >
  > > Scale up : 서비스 plan을 높이는 것(성능을 높이는 것)
  > >
  > > Scale out : 동일한 내용을 복사해서 여러 개 더 많드는 것
  > >
  > > > Manual scale : 개발자가 직접 갯수를 정함
  > > >
  > > > Custom autoscale : custom의 수에 따라 자동적으로 변경 됨
  > > >
  > > > > Rules : Add a rule -> 적용할 규칙 설정
  >
  > -> Add