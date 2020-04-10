# Azure DNS

- directory = Tenant

- directory 마다  따로 Setting 을 해줘야 한다.

- Group 만들기
  - 일일히 role을 권한을 주는게 아니라 한번에 권한을 주기 위하여 사용
  - 해당 group에 속한 사람은 group에 할당 된 role이 자동적으로 할당 됨

> 해당 AAD -> Gourp -> New Group ->
>
> ![image-20191213133318468](C:/Users/student/Desktop/TIL/Azure/image/image-20191213133318468.png)
>
> -> Create

- RBAC(Role Base Access Control) : 모든 서비스는 Role Base로 관리된다.

- ARM은 Full RBAC이고, Classic에서는 제한된 RBAC 사용

> Home -> DNS Zone -> 해당 Zone ->access control (IAM) -> Add -> Add role assignment -> 
>
> ![image-20191213133935282](C:/Users/student/Desktop/TIL/Azure/image/image-20191213133935282.png)
>
> -> Save
>
> => IT_Adimin rm그룹에 속한 멤버 모두에게 해당 Role이 할당 된다.



- CNAME 레코드
  - 도메인 이름 -> Alias에 입력해 놓은 도메인이름으로 연결해줌

