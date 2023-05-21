# 20233057-김유민 github 과제

***

# [TOP]

### [TOP 명령어란?]

현재 OS의 상태를 나타내주는 CLI 어플리케이션

메모리 사용량, CPU 사용량 등을 나타냄

top를 실행하는 동안에는 주기적인 업데이트로 실시간에 근접한 내용을 보여줌

***

### [실행 결과]

![image](https://github.com/yumin-20233057/yumin20233057/assets/133843588/568874b5-c89b-4b0b-8730-de9cc52caf60)

* System time : 시스템 현재 시간 GMT기준으로 표시 ㅤ(예제 GMT기준 16:58:55 / 한국시간기준 00:58:55)

* Uptime : OS가 살아있는 시간 day와 같은 시간으로 표시 ㅤ(예제 시간 7일 1시 15분)

* User sessions : 유저 세션 수

* Load Average : CPU Load의 평균을 표시 앞에서부터 1분, 5분, 15분에 대한 평균 값

* Task : 현재 프로세스들의 상태를 나타내는 주된 영역
```
* 실행(Runnable) - CPU에 의해서 명령어가 실행중인 Process
* 준비(Ready) - CPU의 명령어 실행을 기다리는 Process
* 대기(Waiting) - I/O operation이 끝나기를 기다리는 Process
* 종료(Terminated) - Ctrl + Z 등의 signal로 종료된 Process
```

* CPU사용량 : %Cpu(s)라는 영역 cpu가 어떻게 사용되고 있는지 그 사용률을 보여줌
```
* us : 프로세스의 유저 영역에서의 CPU 사용률
* sy : 프로세스의 커널 영역에서의 CPU 사용률
* ni : 프로세스의 우선순위(priority) 설정에 사용하는 CPU 사용률
* id : 사용하고 있지 않는 비율
* wa : IO가 완료될때까지 기다리고 있는 CPU 비율
* hi : 하드웨어 인터럽트에 사용되는 CPU 사용률
* si : 소프트웨어 인터럽트에 사용되는 CPU 사용률
* st : CPU를 VM에서 사용하여 대기하는 CPU 비율
```

* 메모리 사용량 : 첫째줄 ram의 메모리 영역으로 mem이라 표시되어있는 부분 / 아랫줄 swap  메모리 영역 mem이 가득 차면 사용
```
* total : 총 메모리 양
* free : 사용가능한 메모리 양
* used : 사용중인 메모리 양
```

* 디테일 영역
![image](https://github.com/yumin-20233057/yumin20233057/assets/133843588/ad97c20d-1ab3-4df2-b866-eb1a1b26f265)

```
* PID
    * PID는 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값
* USER
    * 해당 프로세스를 실행한 USER 이름 또는 효과를 받는 USER의 이름
* PR & NI
    * PR : 커널에 의해서 스케줄링되는 우선순위
    * NI : PR에 영향을 주는 nice라는 값
* VIRT, RES, SHR, %MEM
    * 해당 필드들은 프로세스의 메모리와 관련
    * VIRT : 프로세스가 소비하고 있는 총 메모리 프로그램이 실행중인 코드, heap, stack과 같은 메모리, IO buffer 메모리를 포함
    * RES : RAM에서 사용중인 메모리의 크기
    * SHR : 다른 프로세스와의 공유메모리(Shared Memory)
    * %MEM : RAM에서 RES가 차지하는 비율
* S : 프로세스의 현재 상태
* TIME+ : 프로세스가 사용한 토탈 CPU 시간
* COMMAND : 해당 프로세스를 실행한 커맨드
```

***
***

# [PS]

## [PS 명령어란?]
현재 실행중인 프로세스 목록과 상태를 보여줌

ps의 옵션은 유닉스에 따라 옵션이 다름
```
system V : - 사용
system BSD : - 사용 X 
system GNU : -- 두개 사용
>> 프로세스의 상태 출력할려면 정확한 옵션 사용 중요
```

***

## [PS 사용법]
$ ps [option]

![image](https://github.com/yumin-20233057/yumin20233057/assets/133843588/f7e9f6f8-4098-4a11-8c07-bcdc5d8aa167)

***

## [PS option]
```
-A : 모든 프로세스 출력
a (BSD계열) : 터미널과 연관된 프로세스 출력. 보통 x옵션과 연계하여 모든 프로세스 출력할때 사용
-a : 세션 리더(일반적으로 로그인 셀)을 제외하고 터미널에 종속되지 않은 모든 프로세스 출력
-e : 커널 프로세스를 제외한 모든 프로세스 출력 
-f : 풀 포맷으로 보여줌. 유닉스 스타일로 출력 UID, PID, PPID등이 표시
-l(sysV) : 긴 포맷으로 보여줌. 프로세스의 정보를 길게 보여주는 옵션 우선순위와 관련 PRL와 NI값 확인 가능 (BSD계열은 l로 사용)
-o 값 : 출력 포맷을 지정하는 옵션 값으론 pid, tty, time, cmd등을 지정
-M : 64비트 프로세스들을 보여줌
-m : 커널 스레드들도 보여줌
-p : 특정 PID를 지정
-r : 현재 실행중인 프로세서를 보여줌
u (BSD계열) : 프로세스 소유자를 기준으로 출력 (ps ax만 하면 USER 기준의 정보가 안뜸, aux 이렇게 사용)
-u : 특정 사용자의 프로세스 정보를 확인  (사용 사용자 지정X -> 현재 사용자 기준 출력)
x (BSD계열) : 터미널에 종속되지 않은 프로세스 출력 (보통 a옵션과 결합하여 모든 프로세스 출력할때 사용)
-x : 로그인 상태에 있는 동안 완료되지 않은 프로세서들을 보여줌
     사용자가 로그아웃 한 후에도 임의의 프로세서가 계속 동작하게 할 수 있음
```

***

## [PS 항목]
```
USER : BSD 계열에서 나타나는 항목으로 프로세스 소유자의 이름
UID : SYSTEM 계열에서 나타나는 항목으로 프로세스 소유자의 이름
PID : 프로세스의 식별 번호
PPID : 부모 프로세스 ID
%CPU : CPU 사용 비율의 추청치 (BSD)
%MEM : 메모리의 사용 비율의 추정치 (BSD)
VSZ : K단위 또는 페이지 단위의 가상 메모리 사용량
RSS : 실제 메모리 사용량
TTY : 프로세스와 연결된 터미널
S, STAT : 현제 프로세스의 상태 코드 (S:sys V, STAT : BSD)
TIME : 총 CPU 사용 시간
COMMAND : 프로세스의 실행 명령행
STIME : 프로세스가 시작된 시간 혹은 날짜
C, CP : 짧은 기간 동안의 CPU 사용률
F : 프로세스의 플래그
PRI : 실제 실행 우선 순위
NI : nice 우선순위 번호
```

***
***

# [JOPS]

### [JOPS 명령어란?]

백그라운드로 실행중인 프로세스 목록을 조회

현재 중지된 프로세스 목록을 조회

***

## [JOPS 사용법]
$ jops [옵션]

$ jops -x command [args]

***

## [JOPS option]
```
-l : 프로세스 그룹 ID를 state 필드 앞에 출력
-n : 프로세스 그룹 중에 대표 프로세스 ID를 출력
-p : 각 프로세스 ID에 대해 한 행씩 출력
command : 지정한 명령어를 실행
```

***

## [JOPS 상태값]
```
Running : 작업이 일시중단 되지 않았고 종료하지도 않고 계속 진행 중
Done : 작업이 완료되어 0을 반환하고 종료
Done (code) : 작업이 정상적으로 완료했으며, 0이 아닌 코드를 반환
Stopped : 작업이 일시 중단
Stopped (SIGTSTP) : SIGTSTP 신호가 작업을 일시 중단
Stopped (SIGSTOP) : SIGSTOP 신호가 일시 중단
Stopped (SIGTTIN) : SIGTTIN 신호가 작업을 일시 중단
Stopped (SIGTTOU) : SIGTTOU 신호가 작업을 일시 중단
```

***
***



