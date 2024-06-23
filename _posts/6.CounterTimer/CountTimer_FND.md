
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
	DDRA = 0x03; DDRC = 0xFF; DDRG = 0x0F;
	//DDRE = 0x00;
	//EICRB = 0x0A;
	//EIMSK = 0x30;
	//TCCR0 = 0x06; // normal mode, prescale = 256
	//TCNT0 = 0x83; // After 2mSec, Overflow
	//TIMSK = 0x01; // Overflow Interrupt Unmask
	TCCR2 = 0x0D; // CTC mode, prescale = 1024
	OCR2 = 0x32; // after 3.2mSec, CTC match
	TIMSK = 0x80; // Output Compare Interrupt Unmask
	sei();
}

ISR(TIMER2_COMP_vect) //tcnt2 output compare interrupt
{
	static int cnt = 0; // static 은 이전 값을 유지 함
	switch(cnt){
		case 0 : 
				 PORTC = 0x3f; // 0출력
				 PORTG = 0x08;// 첫번째 FND 
				 break;
				 
		case 1 : 
				 PORTC = 0x06; //1 출력
				 PORTG = 0x04; //2번쨰 FND
				 break;
				 
		case 2 : 
				 PORTC = 0x5b; //2 출력
				 PORTG = 0x02; //3번째 FND
				 break;
				 
		case 3 : 
				 PORTC = 0x4f; //3 출력
				 PORTG = 0x01; //4번쨰 출력
				 break;
				 
		default : 
				 break;
	}
	cnt++;
	cnt %= 4;
	// TCNT2 초기화 없음, CTC mode
}
```