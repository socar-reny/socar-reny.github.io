---
layout: post
title:  "CPU Scheduling, Process 이해하기"
subtitle:   "CPU Scheduling, Process 이해하기"
categories: development
tags: os
comments: true
---

CPU Scheduling, Process에 대해 작성한 글입니다

- OS의 역할
	- Process management
		- CPU scheduling
		- Synchronization
	- Memory management
	- File System
	- IO
	- ...
---

---

	- Preemptive : CPU가 어느 프로세스를 실행하고 있는데(아직 끝나지도 않았고 IO를 만난 것도 아닌데) 강제로 쫓아내고 새로운 것이 들어갈 수 있는 스케쥴링(응급실)
	- Non-preemptive : 프로세스가 끝나거나 IO를 만나기 전엔 안됨(은행)
	- Throughput (처리율) : 시간당 몇 개의 작업을 처리하는가
	- Turnaround time (반환시간) : 작업이 레디큐에 들어가서 나오는 시간의 차이(병원에서 진료 받을 때..대기하고 CT 찍고, ... 나오는 시간 차) 짧아야 좋음
	- Waiting time (대기시간) : CPU가 서비스를 받기 위해 Ready Queue에서 얼마나 기다렸는가
	- Response time (응답시간) : Interactive system에서 중요. 클릭-답, 타이핑-답. 첫 응답이 나올 때 까지 걸리는 시간

- 먼저 온 놈 먼저 서비스. 세상에서 많이 사용
- 꼭 좋은 성능을 내는 것은 아님
	- P1, P2, P3순일 경우 (0+24+27)/3 = 17
	- P3, P2, P1순일 경우 (6+3+0)/3 = 3
	- Gantt Chart
	
		| Process | Burst Time |
		|:-------:|:----------:|
		|    P1   |     24     |
		|    P2   |      3     |
		|    P3   |      3     |	
- Convoy Effect (호위효과) : 왕 뒤에 시중들이 따라다님. 다른 프로세스들이 시중들같이 따라다님
- 실행 시간이 짧은 놈을 먼저 실행
- 대기 시간을 줄이는 관점에선 SJF가 제일 좋음
- Example:

	| Process | Burst Time |
	|:-------:|:----------:|
	|    P1   |     6      |
	|    P2   |     8      |
	|    P3   |     7      |
	|    P4   |     3      |	
|:-------:|:------------:|:----------:|
|    P1   |       0      |      8     |
|    P2   |       1      |      4     |
|    P3   |       2      |      9     |
|    P4   |       5      |      5     |

 
|:-------:|:----------:|:--------:|
|    P1   |     10     |     3    |
|    P2   |      1     |     1    |
|    P3   |      2     |     4    |
|    P4   |      1     |     5    |
|    P5   |      5     |     2    |


- AWT = P2, P5, P1, P3, P4 = (6+0+16+18+1)/5 = 8.2
- Priority
- 수건 돌리기하듯 돌아가며 진행
- 시간을 쪼개서 프로세스 진행
- 쪼갠 동일한 시간을 Time Quantum, Time Slice라 부름	
	- Time quantum 시간양자 = time slice (10 ~ 100msec)
|:-------:|:----------:|
|    P1   |     24     |
|    P2   |      3     |
|    P3   |      3     |

| Process | Burst Time |
|:-------:|:----------:|
|    P1   |      6     |
|    P2   |      3     |
|    P3   |      1     |
|    P4   |      7     |

- Average Turnaround Time
- 데이터에 따라 성능이 다름

### Multilevel Queue Scheduling
	- 프로세스를 그룹화. 은행에서 간단한 업무 / 대출 업무 구분해서 받는 것과 유사
	- 그룹에 따라 다르게 스케줄링
	- 한 Queue에만 있지 않고 옮겨가는 방식
	- 제일 첫 프로세스는? 부팅하고 OS가 첫 프로세스(init)를 생성
	- 해당 프로세스가 가졌던 모든 자원은 O/S에게 반환 (메모리, 파일, 입출력장치 등)

## 쓰레드(Thread)

```

- 요즘 프로그램들은 Context 변화하는 단위가 프로세스가 아닌 쓰레드
	- 주요 메소드
```

```



## Reference
- [양희재 교수님 운영체제 강의](http://kocw.net/home/search/kemView.do?kemId=978503)
- [introduction to Operating System](https://www.slideshare.net/LukaXavi/introduction-to-operating-system-10938506)










