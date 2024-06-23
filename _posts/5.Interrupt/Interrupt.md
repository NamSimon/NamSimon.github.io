
### 주의가 필요함을 나타내는 비동기 신호

- 프로세서의 내/ 외부 장치가 프로세서에게 특정 이벤트(event)가 발생함을 알려서 이벤트를 처리함.
- 이벤트는 프로세서의 내부 장치나 외부 I/O장치에서 비 정기적으로 발생하기 때문에 인터럽트 처리를 통해 주변 장치의 서비스 요청을 효율적으로 다룸.

![[Pasted image 20240416142658.png]]


## 인터럽트 처리 과정

![[Pasted image 20240416142801.png]]

1. 실행 프로그램의 중단점 주소를 스택에 저장
2. 인터럽트 벡터(Interrupt vector)에 위치한 인터럽트 처리 루틴(ISP : Interrupt Service Routine)를 실행
3. 스택에서 중단점의 주소를 로드하여 원래 프로그램의 중단점으로 복귀


![[Pasted image 20240416142959.png]]



## 인터럽트는 비동기식 이벤트

![[Pasted image 20240416144033.png]]

## 인터럽트의 용어

| 용어                              | 설명                                               |
| ------------------------------- | ------------------------------------------------ |
| Interrupt Source                | - 인터럽트 발생되는 원인 <br>- ATmega128은 35개의 인터럽트 소스가 있음 |
| Interrupt Trigger               | 인터럽트 소스의 신호 유형(level, edge)                      |
| Interrupt Enable                | 인터럽트 허가                                          |
| Interrupt Disable               | 인터럽트 금지                                          |
| Interrupt Response Sequence     | 인터럽트 발생시 처리 절차                                   |
| Interrupt Service Routine (ISR) | 발생한 인터럽트의 처리를 위해 미리 정의된 프로그램                     |
| Interrupt Vector                | 인터럽트 서비스 루틴이 실행되는 시작주소                           |


## Interrupt Source

![[Pasted image 20240416144558.png]]
![[Pasted image 20240416144612.png]]
![[Pasted image 20240416144622.png]]



## 외부 인터럽트 (INT 0 ~7)

- INT0~INT3 : PD0~PD3 (Port D) 
- INT4~INT7 : PE4~PE7 (Port E)

![[Pasted image 20240416144918.png]]![[Pasted image 20240416145006.png]]

## Global Interrupt Enable

-  SREG(Status Register) : address (0x5F)

	![[Pasted image 20240416150754.png]]
	- I (7 bit) : Global Interrupt Enable
	- ‘1’ : interrupt enable
	- ‘0’ : interrupt disable

	ex)
- **Interrupt Enable**
```c
	SREG |= 0x80; //SREG 직접 제어 
	sei(); // avr library
```


- **Interrupt Disable**
```c
	SREG &= ~(0x80); //SREG 직접 제어 (또는, SREG &= 0x7F;)
	cli(); // avr library
```




## EIMSK register : Interrupt Mask

- **External Interrupt MaSK register**  : address( 0x59 )
- External Interrupt (INT0~INT7)의 허용 여부를 제어


![[Pasted image 20240416151405.png]]

- ‘1’ : enable 
- ‘0’: disable

## External Interrupt Control Register (EICRA, EICRB) : Interrupt Trigger 

- Interrupt Trigger
	- Level trigger
		- low level : ‘0’ 상태이면 interrupt trigger
		- high level : ‘1’ 상태이면 interrupt trigger
	- Edge trigger
		- rising edge : ‘0’ -> ‘1’ 이면 interrupt trigger
		- falling edge : ‘1’ -> ‘0’ 이면 interrupt trigger
		![[Pasted image 20240416151654.png]]
	![[Pasted image 20240416151937.png]]
	※ 2비트씩 생각해야함.



## Interrupt Service Routine

- ISR (vector, attributes)
	- Format of WinAVR
	- vector : interrupt source
		- ex) INT0_vect : external interrupt 0(PD0)
	- attrubutes : interrupt 속성, 생략 가능
	ex)
```c
		ISR(INT0_vect) { 
		… 
		} /* external interrupt 0 (PD0)가 발생할 때 ISR */
```

※ ISR은 선언, 호출은 필요 없음

![[Pasted image 20240416152756.png]]
![[Pasted image 20240416152809.png]]
![[Pasted image 20240416152823.png]]




## 실습
----
[스위치 인터럽트(pin4)](Interrupt/switch_interrupt.md)
[스위치 인터럽트 활용](5.Interrupt/Useful_of_interrupt.md)
[Timer 인터럽트](5.Interrupt/Timer_inturrpt)
