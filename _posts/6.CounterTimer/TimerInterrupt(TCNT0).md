
```c
#include <avr/io.h>
#include <avr/interrupt.h>

void init();

int main(){
	init();
	while(1);
	return 0;
}

void init() // init 함수 정의
{
	DDRA = 0xFF;
	//DDRC = 0xFF;
	//DDRG = 0x0F;
	//DDRE = 0x00; // 스위치
	//EICRB = 0x0A; //외부 인터럽트
	//EIMSK = 0x30;
	TCCR0 = 0x06; // normal mode, prescale = 256  0000 0110
	TCNT0 = 0x83; // After 2mSec, Overflow
	TIMSK = 0x01; // Overflow Interrupt Unmask
	sei();
}

ISR(TIMER0_OVF_vect) //tcnt0 overflow interrupt
{
	static int cnt = 0; // static 은 이전 값을 유지 함
	TCNT0 = 0x83; // After 2mSec, Overflow
	if( cnt < 100 ) PORTA = 0xFF; // 0.2초간 LED on
	else PORTA = 0x00; // 0.2초간 LED off
	cnt++;
	cnt %= 200;
	
	//if( cnt < 250 ) PORTA = 0xFF; // 0.5초간 LED on
	//else PORTA = 0x00; // 0.5초간 LED off
	//cnt++;
	//cnt %= 500;
}
```
