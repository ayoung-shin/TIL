# Virtual Machine scale set

- [Virtual Machine scale set 생성하기](#virtual-machine-scale-set-생성하기)
- [Web Server 허용하기](#web-Server-허용하기)

----

- Virtual Machine
  - IaaS로, scale up은 가능하나 out은 자동으로 안된다.
  - Virtual Machine scale sets을 통해 자동화할 수 있다.
- WordPress
     - PaaS로, scale up & out 자동으로 가능

## Virtual Machine scale set 생성하기

> Add ->
>
> > Virtual machine scale set name : VMscale
> >
> > Operating system disk image : 최신 버전들은 scale sets을 지원하지 않음
> >
> > Resource group : 지우기 쉽게하기 위해 VM과 다른 group에 저장
> >
> > Autoscale : Enabled
> >
> > Maximum number of VMs : 최대 1000까지 가능
> >
> > Scale out
> >
> > > CPU threshold(%) : 75; 5분동안 CPU가 75%이상일 때 늘려감
> > >
> > > Number of VMs to increase by : 2; 2개씩 늘림
> > >
> > > > Increase count by ~ : ~씩 늘려가라
> > > >
> > > > Increase count to ~ : ~까지 늘려라
> >
> > Scale in
> >
> > > CPU threshold(%) : 25; 5분동안 CPU가 25%이하일 때 줄여감
> >
> > Choose Load balancing options : None
> >
> > Virtual network -> Create new
> >
> > > Name : myVNe
> > >
> > > Address space, Subnets : 있는거 사용
> >
> > Public IP address per instance : On; 각 instance 마다 Public IP를 매칭한다.
> >
> > Public inbound ports : Allow sellected ports ; 방화벽에서 입장가능
> >
> > Select inbound ports : RDP (3389)
>
> -> Create

- cf ) 
  - Application Gateway :L7의 부하분산장치 ;적용하기 전에 먼저 만들어야 한다.
  - Load balancer : L4의 부하분산장치

- VM scale sets 생성을 통해 생성된 Resource: 
   - VirtualNetwork
   - VMscale2( = Virtual machine scale set)
   - VMscale2nsg( = Network security group)

  

- CPU stress test tool
  
- CPU를 부하시켜 제대로 작동하는지 확인하기 위한 프로그램
  
> VM scale set -> Instances -> VMscale_1 -> IP 획득 -> cmd을 통해 VMsclae_1에 원격접속
>
> -> cpu stress test tool .zip파일 다운 -> .zip 파일 풀기 -> prime95 실행 -> Run -> Just Stress Testing 
>
> -> OK -> scale set이 최대치 까지 늘어난 것 확인 -> 메뉴 Test -> Stop -> scale 줄어드는 것 확인

  

- VMscale의 메뉴

  - Scaling : Scale up
  - Size : Scale out

- VMscale -Networking

  - inbound : VM으로 들어오는  control

  - outbound : VM에서 바깥으로 내보내는 control(random port사용, control 불가)

  - 방화벽 setting 시 Outbound port rules은 setting 하지 않고, Inbound port rules만 setting 한다.

  - protocol : TCP, UDP

  - Priority의 숫자가 낮을 수록 우선 순위가 높다.

  - 웹서비스시 80번 port 열기

    > Add inbound port rule ->
    >
    > > Source : Any ; 어떤 Client든 들어올 수 있다.
    > >
    > > Destination port ranges : 80
    > >
    > > Protocol : TCP
    > >
    > > Priority : 250
    > >
  > > Name : Port_80
  >
  > -> Add
  
     
  
    cf ) 방화벽을 안열고 VM을 만든 경우 Networking에서 열어주면 된다.

- cmd
  
  - netstat -na : 열린 port 확인하기
    - Local Address : 내 컴퓨터
      - 목적지에 가기 위하여 내컴퓨터에서 random으로 발생시키는 포트번호(ex-70.12.113.131:139 중 139)
    - Foreign Address : 목적지 컴퓨터

## Web Server허용하기

> 해당 VM의 Server Manger의 Manager -> add Roles and Features -> next -> next -> next 
>
> -> Server Roles : Web Server (IIS) 체크 -> Add Features -> next.... -> install -> close

>  -> Tools -> IIS Manager -> vm 왼쪽 화살표 클릭 -> Sites 왼쪽 화살표 클릭 -> Default Document 
>
>  -> Default Document 순서 확인 -> "Default.htm" 최우선 확인 
>
>  -> `C:\inetpub\wwwroot` 에 "This is my first web site (이니셜) 을 "Default.htm"으로 저장 
>
>  -> 인터넷에 IP주소 입력해서 문장 뜨는지 확인

- IIS(Internet Information Server) : MS
  - Web Server
  - FTP Server
  -  SMTP Server
- Apache : Linux/ Unix ; 무료
- NGINX  : Linux/ Unix ; Apache보다 성능, 보안 좋음