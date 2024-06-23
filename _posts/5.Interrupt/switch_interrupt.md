

```c

#include <avr/io.h>
#include <avr/interrupt.h> //인터럽트 라이브러리 불러오기

int main(void)
{
	DDRA= 0xFF; //LED핀 출력으로 설정
	DDRE= 0x00;// 스위치핀 입력으로 설정 
	EICRA = 0x02; // A던B던 상관노 Failing edge
	EIMSK=0x10; //  INT 4번핀 설정
	sei();// Global Interrupt Enable
    while (1) 
    {
    }
}


ISR(INT4_vect)
{
	PORTA=0xFF;// INT4 발생시 led on
}


```