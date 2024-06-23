# 4. AVR CPU Core & 8 bit AVR Instruction Set 


## Block Diagram of the AVR ArchitectureBlock Diagram of the AVR Architecture

![alt text](Atmega128/4.Instruction/image.png)



## AVR Architecture

![alt text](Atmega128/4.Instruction/image-1.png)

- **Flash program memory (16bit)**
  - 16 bit x 216 = 2 byte x 64 k = 128 kbyte =1024 bit
  - Program code가 저장되는 곳


-  **Data Memory (8 bit)**
   -  범용 register : 32 byte
   -  I/O register : 64 byte
   -  Ext I/O register : 160 byte
   -  SRAM : 4096byte
   -  변수가 저장되는 곳

-  **PC : Program Counter**
   -  address of the instruction being executed
  


## Program / Compile / Execution

   - **Program 작성 -> Ccode 생성**
   - **Compile -> hex code 생성**
     - hex code : download 가 가능한 code
     - machine code (assembly code) : 실행 가능한 code
   - **Execution**
     - 프로그램 코드 실행 주소 => PC
     - Fetch : PC -> flash program memory
       - machine code -> IR, PC +=1 OR +=2
       - Decode : instruction decode



   -  **실행**
       -  Operand Fetch 등록
       - ALU 연산 실행
       - 결과 다시 쓰기



  - **Fetch로 이동**
  
    ![alt text](Atmega128/4.Instruction/image-2.png)


## Instruction Execution

   - Instruction
     - 실행 프로그램의 요소
     - 프로세서의 단일 작동
     - opcode / machine code/ assembly code

- clk: system clock
	- Atmega 128 : 16MHz 가능, XTAL1 pin으로 공급 
- Execution Time
	- 1/clk
	- clk = 16MHz
	- clk = 7.3728MHz


## AVR Instruction Set : 133 Instructions

- Operation Code + Operand
- **Operation Code** : ALU가 실행할 내용
- **Operand :** ALU가 실행할 대상

## Register

**32개의 8비트 범용 레지스터(R0~R31)**


![[Pasted image 20240416135741.png]]


## Operation Code의 유형

-  **Arithmetic and Logic** : 범용 레지스터간의 사칙연산과 로직연산
	- ex) ADC, AND, SUB, AND ,OR, ...
	
- **Branch** : 다른 opcode 위치로 이동
	- ex) JMP.BRBC ..
	
- **Data Transfer**
	- Load : SRAM등의 Data를 범용 Register로 이동(LD,LDI, ...)
	- Store : 범용 Register의 값을 SRAM등으로 이동(ST, STD, ...)

- **Bit and Bit-Test**
	- Register의 특정 bit을 set(=‘1’)하거나 clear(=‘0’)으로 변경
	- SBI,CLI,...

- **MCU Control**
- **Immediate**
- **Direct(absolute)**
	- operand의 주소
	- Register Direct, I/O Direct, Data Direct

- I**ndirect**
	- operand을 명시하는 주소
	- 간접데이터, 변위가 있는 간접데이터 , 사전감소가 있는 간접데이터, 추후 증가가 있는 간접 데이터

## Data Indirect
-----

![[Pasted image 20240416140824.png]]



## Status Register
---------

- 상태 레지스터에는 가장 최근에 실행된 결과에 대한 정보가 포함
- SREG

![[Pasted image 20240416141658.png]]

- 모든 연산이 실행된 후에 SREG이 변경
- ex) ADD
![[Pasted image 20240416141739.png]]




## Debug

--------

- JTAG(Joint Test Action Grouop)
	- JTAG 경계 스캔 기능을 사용하여 PCB 테스트
	- Fuses 과 Lock bits, 논 휘발 메모리을 프로그래밍함.
	- On-chip 디버깅


## I/O register
----

![[Pasted image 20240416142120.png]]![[Pasted image 20240416142129.png]]