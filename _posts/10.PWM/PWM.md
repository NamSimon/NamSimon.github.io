
## DC Motor

![[Pasted image 20240614225832.png]]

- **Law of Motor : 플레밍의 왼손법칙**
![[Pasted image 20240614225851.png]]

- **Law of Generator : 플레밍의 오른손 법칙**
![[Pasted image 20240614225907.png]]

## 실습 키트

![[Pasted image 20240614225933.png]]


- DC motor 예제
```C
#include<avr/io.h>
int main(void){
	unsigned char tmp;
	init();
	while(1) {
		tmp = PINE & 0x30;
		switch(tmp) {
			case 0x00 : PORTB = 0x00; break;
			case 0x10 : PORTB = 0x40; break;
			case 0x20 : PORTB = 0x80; break;
			case 0x30 : PORTB = 0xC0; break;
			default : break;
		}
	}
	return 0;
}




void init()
{

	// I/O Port 초기화
	DDRA = 0xFF;
	DDRB = 0xD0;
	DDRC = 0xFF;
	DDRG = 0x0F;
	DDRE = 0x02;
	DDRF = 0x00;

	// 외부 인터럽트 (Switch1/2) Enable
	EICRB = 0x0A;
	EIMSK = 0x30;

	// Timer/Counter0 초기화
	TCCR0 = 0x06;
	TCNT0 = 0x83;
	
	// Timer/Counter1 초기화
	TCCR1A = 0x00;
	TCCR1B = 0x0A;
	TCCR1C = 0x00;
	OCR1A = 0x3BA;

	// Timer/Counter2 초기화
	TCCR2 = 0x6B;


	// Timer/Counter3 초기화
	TCCR3A = 0x00;
	TCCR3B = 0x0B;
	TCCR3C = 0x00;
	OCR3A = 0x1869;

	// Timer Interrupt Enable
	TIMSK = 0x01|0x10;
	ETIMSK =0x10;

	// UART 초기화
	UCSR0A = 0x00;
	UCSR0B = 0x98;
	UCSR0C = 0x06;
	UBRR0H = 0;
	UBRR0L = 0x67;

	// AD 변환기 초기화
	ADMUX = 0x00;
	ADCSRA = 0x87;

	sei();
}

ISR(TIMER0_OVF_vect)
{
	static int count = 0;
	TCNT0 = 0x83;
	PORTC = Fnd[count];
	PORTG = 8 >> count;
	count++;
	count %= 4;
}

void txd(char ch)
{
	while(!(UCSR0A & 0x20));
	UDR0 = ch;
}
void txd_string(char *str)
{
	int i=0;
	while(1) {
		if (str[i] == '\0') break;
		txd(str[i++]);
	}
}
ISR(USART0_RX_vect) // keyboard input 시 interrupt 발생
{
	Cmd_U0 = UDR0; /* Cmd_U0 : global 변수 */
}


```

## DC 모터의 가감속 제어

- DC 모터의 속도 제어
- DC 모터의 전달함수
  
![[Pasted image 20240614232038.png]]

- 정상 상태 속도는 입력 전압에 비례
![[Pasted image 20240614232058.png]]


## Pulse Width Modulation (PWM, 펄스폭 변조)

- 전기 장치 전원 공급, 전압 조정, 통신 등에 대한 전원을 제어하기 위해 일반적으로 사용되는 기술
- 왜 PWM인가?
	- 적절한 전력으로 전압을 증폭하기가 어려움
	- 많은 장치에 조정 가능한 전력을 적용하기 위한 소형의 저비용 수단
- 신호 크기에 비례하는 pulse width or duty cycle 

![[Pasted image 20240614232302.png]]


## Timer/Count Mode( 8bit )

![[Pasted image 20240614232340.png]]

## Fast PWM Mode (8bit)

![[Pasted image 20240614232356.png]]

- PWM Frequency
$$ f_{pwm} = \frac{f_{I/O}}{N \cdot 256} $$
- duty resolution : 256
	- duty 25% -> OCRn = 0x3F, duty 50% -> OCRn = 0x7F
	- 0 : ORCn = 0x00 Vmax : OCRn = 0xFF

## Phase Correct PWM Mode (8bit)
	![[Pasted image 20240614232744.png]]
- PWM Frequency
$$f_{pwm} = \frac{f_{I/O}}{N \cdot 510}
$$

- duty resolution : 256
	- duty 25% -> OCRn = 0x3F, duty 50% -> OCRn = 0x7F (or 0x80)
	- 0 : ORCn = 0x00   Vmax : OCRn = 0xFF

## PWM in ATmega128

### Fast PWM mode/Phase Correct PWM Mode

- TCNT0
	- OC0 (PB4)
- TCNT1
	- OC1A(PB5), OC1B(PB6), OC1C(PB7)
- TCNT2
	- OC2(PB7)
- TCNT3 : 16 bit Counter
	- OC3A(PE3), OC3B (PE4), OC3C(PE5)

### TCNT2 => PWM으로 사용

- Fast PWM / PB7
- PB6 = ‘0’ or ‘1’

## TCCRn Register : Control Register

- Bit 6, 3 – WGMn1:0: Waveform Generation Mode'
![[Pasted image 20240614233227.png]]

- Bit 5, 4 – COM01:0: Compare Match Output Mode

![[Pasted image 20240614233245.png]]

- Bit 2:0 – CSn2:0 Clock Select : prescale

![[Pasted image 20240614233304.png]]

## 예제
---
[예제1](./예제1)