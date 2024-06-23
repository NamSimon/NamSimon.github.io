

```c


#include <avr/io.h>
#include <avr/interrupt.h>

int main(void)
{
    DDRA=0xFF;//A핀 모두 출력으로 설정
	DDRE=0x00; //E핀 모두 입력으로 설정
	EICRA=0x0A; //  0000 10 10 2비트씩 나눠서 설정 -> falling edge 
	EIMSK=0x30;//  INT4,5 unmask
	sei();
    while (1) 
    {
    }
}

ISR(INT4_vect)
{
	
	PORTA=0xFF;
}

ISR(INT5_vect)
{
	
	PORTA=0x00;
}


```