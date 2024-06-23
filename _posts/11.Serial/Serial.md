
## Serial 통신 프로토콜

### 시리얼 통신

- 컴퓨터와 컴퓨터 또는 컴퓨터와 주변기기 간에 데이터를 주고 받을 때 비트 단위로 데이터를 주고 받는 방식
- 1비트 이상의 데이터 신호와, 필요시 클록, 선택, GND 등의 신호 가 사용됨
- 전송속도는 패러랠(Pararell) 통신보다는 느리나 구현이 간단하고 효율성이 좋아 대부분의 통신에 사용됨

### 대표적인 시리얼 통신
- USART
- I2C (Inter Integrated Circuit) 또는 TWI (Two Wire Interface)
- SPI (Serial Peripheral Interface)
- USB (Universial Serial Bus)


## peripheral (device) 주변 장치

- 컴퓨터가 정보를 외부로 전송하는 데 사용하는 보조 하드웨어 장치
- 컴퓨터에 액세스하고 제어할 수 있지만 컴퓨터의 핵심 구성 요소는 아닌 하드웨어 구성 요소
- Input device : keyboard/마우스/ 스위치 등등
- output device : 모니터/ 프린터 /led 등등
- input/output device : disk drive, USB 등

## SPI(Serial Peripheral Interface)

 - 동기식 직렬 통신을 위한 표준(다양한 변형 포함)으로 통합 회로 간 단거리 유선 통신용 내장 시스템에 주로 사용
 
![[Pasted image 20240615000441.png]]

### ATmega128의 SPI 특징

-  전이중(Full-duplex), 3선(Three-wire) 동기 데이터 통신
- 마스터 또는 슬레이브 동작
- LSB 또는 MSB 순서로 데이터 통신
- 3비트의 프리스케일 비트를 이용한 7개의 전송 속도 선택
- 전송 완료 인터럽트 플래그

![[Pasted image 20240615000840.png]]

- SPI 블록도

![[Pasted image 20240615000935.png]]

## I2C (Inter-Integrated Circuit)

- 마스터(또는 여러 마스터)와 단일 슬레이브(또는 여러 슬레이브) 장치 간에 데이터를 전송하는 방법으로 임베디드 시스템에서 자주 사용되는 간단한 통신 프로토콜

![[Pasted image 20240615001101.png]]


### ATmega128의 TWI(Two-Wire Interface) 특징

- 2개의 라인(SDA, SLA)으로 양방향 직렬 통신
- 마스터와 슬레이브 동작 지원
- 7비트 주소로 최대 128개의 슬레이브 주소와 통신
- 멀티-마스터 조정(arbitration) 기능
- 최대 400KHz 데이터 전송속도 지원

![[Pasted image 20240615001230.png]]

- 블록도
![[Pasted image 20240615001250.png]]

### 데이터 송수신 포맷

![[Pasted image 20240615001351.png]]