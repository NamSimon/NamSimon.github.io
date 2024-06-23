# 마이크로프로세서

![alt text](Atmega128/1.Microprocessor/image.png)

- 마이크로 프로세서는 마이크로 칩에 CPU의 기능을 대부분 통합

![](Atmega128/1.Microprocessor/image-1.png)


### **CPU 구조**

1. ALU : 연산 논리 구조
2. 레지스터
3. Control unit


### **Clock Speed이란?**

- clock 생성기가 펄스를 생성할때 주파수
- 3.4GHz => 2.94*1010 second = 294 ps (picosecond)



## Microcontroller

![](Atmega128/1.Microprocessor/image-2.png)

1. processor core, memory, and programmable input/output peripherals을 포함하는 단일 집적 회로의 소형 컴퓨터
2. µC or MCU(micro-controller unit)
3. 8051(Intel), AVR(Atmel), PIC(Microchip Tech.) , … 존재



## Microprocessor 와 Microcontroller 차이
![alt text](Atmega128/1.Microprocessor/image-3.png)



## Microprocessor 시스템 

![alt text](Atmega128/1.Microprocessor/image-4.png)

1. CPU
   1. 마이크로 프로세서 하드웨어 핵심부분
   2. 산술 연산, 논리연산 등의 명령어 처리
   3. 8비트 마이크로 프로세서는 데이터 버스가 8비트
2. 메모리
   1. RAM,ROM
   2. 저장용 메모리(ssd,hdd)
3. 입출력 장치
   1. 데이터를 입출력하는 부분
4. 인터 페이스 회로
   1. CPU와 입출력 장치를 연결



## 어드레스 버스, 데이터 버스, 제어 버스
1. 버스(bus) : CPU, 메모리 및 입출력 장치 사이에 어드레스, 데이터 및 제어 신호 등이 이동하는 통로
2. Address bus : 주소가 이동하는 통로
3. 데이터 버스 : 데이터가 이동하는 통로
4. 제어 버스 : 제어 신호가 이동하는 통로


## 마이크로 프로세서의 메모리 구조와 명령어
1. 메모리 버스 구조에 따른 분류
   1. 폰 - 노이만 구조
   2. 하버드 구조
   

2. 명령어 구조에 따른 분류
   1. CISC(Complex Instruction Set Computer)
   2. RISC(Reduced Instruction Set Computer)





## 폰노이만 구조와 하버드 구조

![](Atmega128/1.Microprocessor/image-5.png)

- **폰-노이만 구조**: 프로그램과 데이터가 같은 메모리 사용, (b)임
- **하버드 구조** : 프로그램 메모리와 데이터 메모리가 분리, (a)
  - 명령어와 데이터를 동시에 리드할 수 있어 병목 현상이 줄어듬




## CISC와 RISC
  
- **CISC 프로세서**

  -  단일 명령어 처리, 외부 메모리, 작은 개수의 레지스터, 수백개이상의 명령어로 특징됨
  - 수 많은 명령어 처리로 복잡해지며 느려지고 전력소모가 많아짐

- **RISC 프로세서**
  
  - CISC 프로세서에 비해 명령어 개수가 작으며, 처리 속도가 빠르며, 전력소모가 작음
  - 파이프 라인 방식으로 명령어를 처리
  - 임베디드 프로세서에 많이 활용

※ 최근에는 CISC와 RISC 구분이 없어지는 추세




## 디지털 기초

### hexadecimal (16진수)


![alt text](Atmega128/1.Microprocessor/image-6.png)

- 4비트 단위로 16진수 숫자로 표시
- 16진수 표시로 숫자 뒤에 “H”, “h”을 붙이거나 숫자 앞에 “0x”,
“$”를 붙임


  ![alt text](Atmega128/1.Microprocessor/image-7.png)




- **enable, disable**
  - enable : 허가, 활성화 또는 동작을 의미함
  - disable : 금지 또는 비활성화를 의미함



-  **active low, active high**
   -  active low 신호(핀) : “Low”일 때 정상 입출력 동작
   - active high 신호(핀) : “High”일 때 정상 입출력 동작\



- /
  - “또는”의 의미
  - 예) R/W : read (active high) 또는 write(active low)