
## Counter 이란

![[Pasted image 20240416173611.png]]

- 프로세스가 발생 하거나 특정한 상황일 경우의 수를 저장하는 기기
	- 동기식/ 비 동기식 pulse
	- UP카운터/ Down 카운터

## Timing Diagram

![[Pasted image 20240416173802.png]]


## Timer

- 타이머는 특수한 카운터 형태
- 고정 주파수 클럭와 함께 동기식 카운터zz


![[Pasted image 20240416174019.png]]

## Counter/Timer in Atmega128

- 8-bit Timer/Counter
	- TCNT0, TCNT2
	- Counting 범위 : 0x00 ~ 0xFF( 0~255 )
	![[Pasted image 20240416174247.png]]
- 16-bit Timer/Counter 
	- TCNT1H & TCNT1L, TCNT3H & TCNT3L
	- Counting 범위 : 0x0000~0xFFFF ( 0~216 – 1 = 65535)
	![[Pasted image 20240416174335.png]]

## 8-bit Timer/Counter Block Diagram

- TCNT0

![[Pasted image 20240416182429.png]]

- TCNT2
![[Pasted image 20240416182446.png]]



## Pin Configuration

![[Pasted image 20240416192340.png]]

## 8bit Timer/Counter Register 관련 Register

- TCNT0 관련 : TCCR0, OCR0 
- TCNT2 관련 : TCCR2, OCR2 
- 공통 : TIMSK, TIFR, ASSR, SFIOR

![[Pasted image 20240416192440.png]]


## TCNTn : Timer/Counter Register

- TCNTn : Timer/Counter Register : address(0x52, 0x44)
 ![[Pasted image 20240416192629.png]]
 - 타이머 / 카운터 0,2가 카운트 하고 있는 입력 펄스 개수를 기록하는 8비트 레지스터 
 - Prescale !=0 , 상시 동작 및 read/ write 가능 ``

## TCCRn Register : Control Register

- Timer / Counter Control Register : address(0x53, 0x45)
- 8bit counter의 동작 모드, 프리 스케일등을 결정

![[Pasted image 20240416193924.png]]

- Bit 7 - FOC0(Force Output Compare) :  OCn pin 출력여부
- Bit 6, 3 - WGM01:0 ( Waveform Generation Mode )
		![[Pasted image 20240416194842.png]]![[Pasted image 20240416194933.png]]
		
- Bit 5:4 - COM01:0 ( Compare Match Output Mode )
- Bit 2:0 - CS02:0 ( Clock Select : prescale )
		![[Pasted image 20240416195452.png]]



## 8 bit Timer/Counter 관련 Register
- OCR0, 2(Output Compare Register0, 2)
	- TCNT0, 2의 값과 비교하는 8비트 출력 비교 레지스터
	- OCRn과 TCNTn 값이 같을 때 Ocn 핀으로 파형 출력
	![[Pasted image 20240416195421.png]]


## Prescaler

![[Pasted image 20240416195618.png]]

- 예) TCNT0 사용, Normal, OC0 없음, prescale = 256
	![[Pasted image 20240416195649.png]]
		- TCCR0 = 0x06;

- 예) TCNT2 사용, CTC mode, OC0 없음, prescale = 256

	![[Pasted image 20240416195727.png]]
		- TCCR2 = 0x0C;


- **TIMSK : Timer/Counter Interrupt Mask Register**
	![[Pasted image 20240416195841.png]]
	- TOIEn bit : Overflow Interrupt Unmask
	- OCIEn bit : Output Compare Interrupt Unmask
	
- **ETIMSK : Extended Timer/Counter Interrupt Mask Register**
	![[Pasted image 20240416195934.png]]


## Type of Timer Interrupt


### **normal model : overflow interrupt**

![[Pasted image 20240416200039.png]]

- 예) Overflow Interrupt에 활용 (Normal Mode)
	- TCNT0 =0x27
	- 구간 = 0x100 - 0x27 = 0xD9=217
	- 217 ** T 이후 인터럽트 발생

### **clear time on compare match (CTC) mode**

- output comopare interrupt

![[Pasted image 20240416200358.png]]

- 예) OCR0 = 0xA2
	- 구간 = 0xA2=162
	- (162+1) * T 마다 인터럽트 발생 


# 실습
----
[실습1](./TimerInterrupt(TCNT0))
[실습2](./CountTimer_FND)
[실습3](./CounterTimer_FND_interrupt)




