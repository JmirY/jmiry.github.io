---
title: 사용자와 그룹
date: 2019-05-15 20:20
tags: [Linux, User, Group]
---
리눅스 시스템에서의 사용자와 그룹 그리고 권한의 분할에 대해 알아보자.  
<!--more-->
### 다중 사용자 시스템 Multi User System  
리눅스 시스템은 어째서 여러 사용자가 동시에 사용할 수 있도록 만들었을까?  
옛날 옛적엔 컴퓨터 가격이 상당했기에 한 컴퓨터를 여러 인원이 사용했기 때문이다.  
  
중요한 시스템 파일은 일반 사용자가 접근할 수 없도록 하는 것이 안전하다.  
따라서 다중 사용자 시스템은 시스템 보안을 위해서 필수적이다.  
### 권한 Permission 의 분할  
리눅스 시스템에선 사용자별로 읽기/쓰기/실행 가능한 파일이 다르다.  
모든 파일에 대하여 읽기/쓰기/실행 작업이 가능한 사용자가 바로 슈퍼 유저,  
다시 말해 root 다.  
### 그룹 Group  
각 사용자는 최소 한 개 이상의 그룹에 소속돼야 하며  
그룹에는 다수의 사용자가 소속될 수 있다.  
사용자가 생성됐을 때 소속되는 최초의 그룹을 기본 그룹이라고 한다.  
사용자 생성 시 별도의 설정을 하지 않으면  
기본적으로 사용자명과 동일한 그룹이 생성되고 이것이 사용자의 기본 그룹이 된다.  
기본 그룹 외에 추가로 소속되는 그룹을 부가 그룹 Supplementary group 이라 한다.  
groups 명령어를 통해 사용자가 속한 그룹을 확인할 수 있다.  
![groups](https://user-images.githubusercontent.com/17706039/57773585-51cea980-7753-11e9-9399-2dcbbc2490e5.png){:.rounded}
  
id 명령어를 통해 사용자 ID와 기본/부가 그룹 ID를 확인할 수 있다.  
![id](https://user-images.githubusercontent.com/17706039/57773737-ad993280-7753-11e9-9517-84a91b2b7ee2.png){:.rounded}
  
/etc/group 파일을 통해 시스템 내 그룹들을 확인할 수 있다.  
![/etc/group](https://user-images.githubusercontent.com/17706039/57773815-dcafa400-7753-11e9-8430-3346ea31a27e.png){:.rounded}
  
/etc/group 파일의 각 라인은  
  
그룹명 : 비밀번호 : 그룹 ID : 해당 그룹을 부가그룹으로써 갖는 사용자
{:.info}  
형식으로 적혀있다.  
비밀번호가 x로 적혀 있는 이유에 대해선 게시물의 말미에 다루겠다.  
### 권한  
다음 세 집단에 대해 서로 다른 권한을 설정 가능하다.  
1. 파일을 소유하는 사용자
2. 파일을 소유하는 그룹에 속한 사용자
3. 그 외 사용자
  
권한의 종류는 다음과 같다.  
1. 읽기 r
2. 쓰기 w
3. 실행 x
  
ls -l 명령어를 통해 파일의 메타 데이터를 확인해보자.  
![meta](https://user-images.githubusercontent.com/17706039/57774360-4ed4b880-7755-11e9-89a3-aa1e291b267d.png){:.rounded}
  
각 파일의 메타 데이터 중 빨간 네모 부분이 바로 권한을 나타낸다.  
총 9개의 문자로 표현하였는데 의미는 다음과 같다.  
![meaning](https://user-images.githubusercontent.com/17706039/57774607-f0f4a080-7755-11e9-8bff-4657b29c0589.png){:.rounded}
  
문자 - 는 해당 작업을 해당 집단에게 불허한다는 의미다.
예시를 들어보겠다.  
  
rw-r--r-- : 파일을 소유한 사용자만 읽기/쓰기가 가능하며 다른 사용자는 읽기만 가능하다.
{:.info}  
  
디렉토리 파일의 권한은 일반 파일과 다르게 적용된다.  
1. 읽기 권한이 있으면 ls 명령어 등으로 디렉토리의 파일 목록을 확인할 수 있다.
2. 쓰기 권한이 있으면 그 디렉토리 내에 새로운 파일을 생성하거나 삭제할 수 있다.
3. 실행 권한이 있으면 그 디렉토리에 접근할 수 있다.
  
### 자격 증명 Credential  
리눅스 시스템 상에서 활동의 주체는 프로세스이다.  
프로세스는 '특정 사용자의 대리인으로 동작하고 있다'는 증명서를 지닌다.  
커널이 그 증명서를 보고 파일에 대한 접근을 허가한다.  
ps -f 명령어를 통해 프로세스 별 UID를 확인할 수 있는데,  
UID가 바로 증명서이다.  
### 사용자 ID User ID  
/etc/passwd 파일에 사용자 이름과 사용자 ID의 정보를 기록한다.  
![/etc/passwd](https://user-images.githubusercontent.com/17706039/57775361-cd325a00-7757-11e9-8e43-f05102da39ed.png){:.rounded}
  
각 라인의 의미는 다음과 같다.  
  
사용자명 : 비밀번호 : 사용자 ID : 속한 그룹 ID : 정보 : 홈 디렉토리 : 쉘 환경
{:.info}
  
왜 /etc/의 group, passwd 파일에서 비밀번호는 모두 x로 저장돼 있을까?
{:.warning}
  
보안을 위해 비밀번호를 /etc/shadow 파일에 암호화하여 저장했기 때문이다.  
/etc/shadow 파일을 root 권한으로 열어보았다.  
![shadow](https://user-images.githubusercontent.com/17706039/57775558-45008480-7758-11e9-853e-61195ce4549e.png){:.rounded}
  
내 계정의 비밀번호가 암호화되어 기록돼 있는 것을 확인했다.