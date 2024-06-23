
```c
/*
	인터럽트를 이용하여 숫자를 증감하는 코드
	- 첫번째 스위치를 누르면 숫자 증가
	- 2번째 스위치를 누르면 숫자 차감
*/

#include <avr/io.h>
#include <avr/interrupt.h>
#include <util/delay.h>


void init();
volatile char Int_status = 0;// 스위치 상태 전역변수

int main() {
	unsigned char seg[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f}; //0 ~ 10 FND
	unsigned char fnd[4];// 자리 
	int i, count=0, cnt_min=0, cnt_sec = 0;
	init();// 핀 초기 세팅
	while(1) {
		
		fnd[0] = cnt_min; // 분
		fnd[1] = cnt_sec/10; //10's
		fnd[2] = cnt_sec%10;//1's
		fnd[3] = (count/10)%10;// msec
		
		for(i=0;i<4;i++){
			PORTG=0x08>>i;//1000 0000 -> 0100 0000 -> 0010 0000 -> 0001 0000
			if( i%2==0 ) { // 짝수 마다
				PORTC = seg[fnd[i]] | 0x80; // . 추가 
				_delay_ms(3);
			} 
			else { // 홀수 마다
				PORTC = seg[fnd[i]];
				_delay_ms(2);
			}
		}
		
		if(Int_status == 0x01){ //1번째 스위치 일경우 
			count++;
			if(count == 100){//100마다 증가
				count = 0;
				cnt_sec++;
			}
			if(cnt_sec == 60){// 60이면 분 증가
				cnt_sec = 0;
				cnt_min++;
				cnt_min %= 10;
			}
		}else if(Int_status == 0x02&& cnt_sec>=0){ //2번쨰 스위치면
			count--;
			if(count == -1){
				count =99;
				cnt_sec--;
			}
		}
	} // while 문의 end
	return 0;
}

void init() // init 함수 정의
{
	DDRA = 0x03; // 전류 제한
	DDRC = 0xFF; // 각 핀마다 출력
	DDRG = 0x0F;//위치 관련 출력
	DDRE = 0x00; //입력 
	EICRB = 0x0A;// 0000 1010 -> falling edge
	EIMSK = 0x30;// INT 4,5 설정
	sei();
} 

ISR(INT4_vect) // 스위치1
{
	Int_status = 0x01;
	PORTA = 0x01;
}

ISR(INT5_vect) //스위치2
{
	Int_status = 0x02;
	PORTA = 0x02;
}
```


