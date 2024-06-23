
```c

#include <avr/io.h>
#include <avr/interrupt.h>
void init();

unsigned char Seg[16] = {0x3f, 0x06, 0x5b, 0x4f, 0x66,0x6d,0x7d,0x07,0x7f, 0x67, 0x77, 0x7c, 0x58,0x5e,0x79, 0x71};//0~F 
volatile char Int_status = 0;
int Count = 0;

int main(){
	init();
	
	while(1);
	
	return 0;
}

void init() // init 함수 정의
{
	DDRA = 0x03; //A핀 출력 0000 0011
	DDRC = 0xFF; //C핀 전체 출력 모드
	DDRG = 0x0F; //FND자리 숫자 출력
	DDRE = 0x00; // 입력모드 
	EICRB = 0x0A; //0000 1010 인터럽트  failing edge 
	EIMSK = 0x30; // IN4 INT5 인터럽트 설정
	TCCR0 = 0x06; // normal mode, prescale = 256
	TCNT0 = 0x83; // After 2mSec, Overflow
	TCCR2 = 0x0D; // CTC mode, prescale = 1024
	
	OCR2 = 0x64; // after 6.4mSec, CTC match
	TIMSK = 0x81; // Output Compare Interrupt Unmask
	sei();
}

ISR(TIMER0_OVF_vect) //tcnt0 overflow interrupt
{
	static int cnt = 0; // static 은 이전 값을 유지 함
	TCNT0 = 0x83; // After 2mSec, Overflow
	
	cnt++;
	cnt %= 50;// 100mSec필요하면 5->50
	if(cnt==0){
		if(Int_status == 0x01) { //증가  
			Count++;
			Count %= 10000;
		}
		if(Int_status ==0x02)//감소
		{
			Count--;
			if(Count<0)
			{
				Count=9999;
			}
		}
	}
}

ISR(TIMER2_COMP_vect) //tcnt2 output compare interrupt
{
	static int cnt = 0; // static 은 이전 값을 유지 함
	switch(cnt){
		case 0 : 
			PORTC = Seg[Count/1000]; // 100자리수 마지막에 표출
			PORTG = 0x08; 
			break;
			
		case 1 : 
			PORTC = Seg[(Count/100)%10];// |0x80; // 0x80 는 FND에 점찍는것 // 십의 자리수 2번째 표출
			PORTG = 0x04; 
			break;
			
		case 2 : 
			PORTC = Seg[(Count/10)%10]|0x80; // 일의 자리수 3번째 표출
			PORTG = 0x02; 
			break;
			
		case 3 : 
			PORTC = Seg[Count%10]; // 소수점전 자리
			PORTG = 0x01; 
			break;
			
		default : 
			break;
	}
	cnt++;
	cnt %= 4;
}


ISR(INT4_vect)//1번째 버튼 눌렸을때
{
	Int_status = 0x01;
	PORTA = 0x01;
}
ISR(INT5_vect)//2번째 버튼 눌렸을때
{
	Int_status = 0x02;
	PORTA = 0x02;
}
```