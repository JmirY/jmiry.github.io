---
title: 프로세스, 스트림
date: 2019-05-09 20:00
tags: [Linux, Process, Stream]
---
리눅스 시스템의 중요한 개념들인  
프로세스와 스트림에 대해 알아보자.  
<!--more-->
### 프로세스 Process  
메모리에 올려진 상태의 프로그램을 프로세스라고 한다.
{:.info}  
프로그램은 여러 개의 프로세스를 가질 수 있다.  
터미널에서 ps -ef 명령어를 입력해보았다.  
![ps](https://user-images.githubusercontent.com/17706039/57449298-7976cb00-7296-11e9-86e8-74c6a74bdfab.png){:.rounded}
  
현재 실행 중인 프로세스 목록이 출력된다.  
위의 표에서 PID는 Process ID이며  
이는 프로세스 고유의 번호로 같은 프로그램의 프로세스는  
PID를 통해 구별 가능하다.  
### 스트림 Stream  
스트림은 바이트의 흐름이다.
{:.info}  
데이터가 이동하는 통로라고 할 수 있겠다.  
프로세스는 커널에게 시스템 콜을 통해 스트림 연결을 요청하고  
시스템 콜을 사용하여 연결된 스트림을 통해 데이터를 읽고 쓴다.  
![stream](https://user-images.githubusercontent.com/17706039/57449506-0752b600-7297-11e9-970c-e04ca551b032.png){:.rounded}
  
위 그림은 프로세스와 일반 파일 간에 스트림이 연결된 것을 묘사한 것이다.  
스트림은 바이트가 흘러갈 수 있는 곳이면 어디든 연결 가능하므로  
SSD, HDD, 키보드와 같은 장치와도 연결이 가능하다.  
  
이 스트림이 프로세스와 연결되면 파이프 Pipe라는 명칭으로 불린다.
{:.info}  
그렇다면 스트림이 다른 컴퓨터의 프로세스/파일과 연결되면 어떨까?  
이것이 네트워크 통신이다.  
  
네트워크 통신과 파이프 같이 프로세스 간에 스트림을 통해  
데이터를 주고받는 것을 IPC InterProcess Communication이라고 한다.
{:.info}  
  
---
  
리눅스를 구성하는 세 가지 중요 개념인  
파일 시스템, 프로세스, 그리고 스트림에 대해 간략히 알아보았다.  
각 개념들의 관계를 표현한 그림을 아래에 첨부한다.  
이는 리눅스를 이해하는 데 있어 매우 중요하다.  
![3concepts](https://user-images.githubusercontent.com/17706039/57449774-bc856e00-7297-11e9-97e3-c0c740f00e22.png){:.rounded}