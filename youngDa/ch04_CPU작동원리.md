# CH 04. CPU 작동 원리
## 4-1 ALU와 제어장치
- ALU의 input : 피연산자(from 레지스터), 제어신호(수행할 연산, from 제어장치)
- ALU의 output : 특정 숫자/문자/메모리주소

- CPU 접근 속도 : 레지스터 >>(빠름)>> 메모리
  - ALU가 결과값을 메모리가 아닌 레지스터에 우선 내보내는 이유

- 플래그(flag) : 연산결과의 추가적인 상태
  - 부호플래그, 제로플래그, 캐리플래그, 오버플로우플래그, 인터럽트 플래그, 슈퍼바이저 플래그 등...
  - CPu가 프로그램 실행하는 도중 반드시 기억해야 하는 참고정부
  - 플래그 래지스터에 저장

### 제어장치
- 제어장치 : 제어신호 내보내고 명령어 해석하는 부품
- 제어신호 : 컴퓨터 부품 관리하고 작동시키기 위한 전기신호\

제어장치가 받아들이는 정보
1. 클럭신호를 받아들임
   - 클럭(clock): 컴퓨터 부품 움직이게 하는 시간 단위
2. 해석해야 할 명령어를 받아들임
   - 명령어 레지스터에 저장도니 값
3. 플래그 레지스터 속 플래그값 받아들임
4. 시스템 버스, 그 중 제어버스로 전달된 제어신호 받아들임

제어장치가 내보내는 정보
- CPU 외부
  - 메모리, IO, ...
- CPU 내부
  - ALU에 전달하는 제어신호
  - 레지스터에 전달하는 제어신호

## 4-2 레지스터
### 반드시 알아야 할 레지스터
1. 프로그램 카운터 : 메모리에서 가져온 명령어 주소(메모리에서 읽어들일 명렁어 주소)
2. 명령어 레지스터 : 해석할 명령어. 메모리에서 읽어들인 명령어
3. 메모리주소 레지스터 : 메모리 주소 저장하는 레지스터
4. 메모리버퍼 레지스터 : 메모리와 주고받을 값(데이터와 명령어) 저장하는 레지스터
5. 플래그 레지스터 : APU연산결과, CPU 상태 부가정보 저장하는 레지스터
6. 범용 레지스터 : 다양하고 일반적인 상황에서 사용되는 레지스터
7. 스택 포인터
8. 베이스 레지스터

### 특정 레지스터 이용한 주소 지정 방식 : 스택 주소 지정 방식
- 스택포인터 : 스택주소 지정방식
- 프로그램카운터, 베이스레지스터 : 변위주소지정방식

스택주소 지정방식
- 스택과 스택포인터를 이용한 주소 지정방식
- 스택포인터 : TOP
- 메모리 내부의 스택영역

### 특정 레지스터 이용한 주소 지정 방식 : 변위 주소 지정방식
오퍼랜드 필드 값(변위)과 특정 레지스터값 더해서 유효주소를 얻는 주소 지정 방식
- 상대주소지정방식 : 오퍼랜드와 프로그램 카운터 값을 더해서 유효주소를 얻는 방식
- 베이스 레지스터 주소 지정 방식 : 오퍼랜드와 베이스 레지스터 값을 더해서 유효 주소를 얻는 방식

## 4-3 명령어 사이틀과 인터럽트
- 명령어 사이클 : 명령어를 처리하는 정형화된 흐름
- 인터럽트 : 명령어 흐름이 끊어지는 상황

### 명령어 사이클
- 프로그램속 각각의 명령어들이 일정 주기가 반복되어 실행됨
- 인출사이클 : 메모리에 있는 명령어를 CPU에서 가지고 오는 단계
- 실행사이클 : CPU로 가져온 명령어를 실행하는 단계
- 간접사이클 : 명령어를 실행하기 위해 메모리 접근을 한번 더 함

### 인터럽트
- CPU 작업 방해하는 신호
  - 동기 인터럽트 : CPU에 의해 발생하는 신호
  - 비동기 인터럽트 : 입출력장치에 의해 발생하는 인터럽트 (=하드웨어 인터럽트)

비동기 인터럽트(하드웨어 인터럽트) 처리 순서
1. 입출력장치가 CPU에 인터럽트 요청 신호 전송
2. CPU 실행사이클 끝나고 명령어 인출 전 인터럽트 여부 확인
3. CPU 인터럽트 요청 확인, 인터럽트 플래그를 통해 인터럽트 받을 수 있는지 여부 확인
4. 인터럽트 받아들일 수 있다면 CPU가 작업 백업
5. CPU는 인터럽트 벡터를 참조하여 인터럽트 서비스루틴을 실행
6. 인터럽트 서비스루틴 실행이 끝나면 4번 과정에서 백업해둔 작업을 복구하여 실행 재개


# 내 생각
한번 더 읽어볼만한 단원인듯 하다. CPU 작업 처리 방식을 대략적으로 알 수 있었다.

# 논의 내용
코드단에서 CPU 작동 방식을 제어할 수 있는지, 제어할 수 있다면 어떤 식으로 튜닝할 수 있는지
