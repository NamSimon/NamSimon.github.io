

```c
/*
	0.1초 timer 만드는 코드
		- x.xx.x 로 표시 (예 : 3.24.7 -> 3분 24.7초)
		- 초는 60초까지 표기 (예 : 4.59.9 다음은 5.00.0)
		- switch 를 누르지 않은 경우 정지
		- switch 1을 누르면 0.1초 씩 증가
		- switch 2를 누르면 0.00.0으로 초기화
*/
#include <avr/io.h>
#include <util/delay.h>


int main()
{
	unsigned char seg[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f}; // 0 to 9
	unsigned char fnd[4] = {0};
	int i, seconds=0, tenths_of_seconds = 0, minutes = 0;

	DDRC = 0xff; // FND segments
	DDRG = 0x0f; // FND selection
	DDRE = 0x00; // 스위치 input

	while(1) {
		if((0x30 & PINE) == 0x20){ // 첫번째 스위치 눌렀을떄
			tenths_of_seconds++;
			if(tenths_of_seconds == 100){
				seconds++;
				tenths_of_seconds = 0;
			}
			if(seconds >= 60){ // 초가 60이상일경우
				minutes++;
				seconds = 0;
			}
			if(minutes == 10){ // 분이 10을 넘었을떄
				minutes = 0;
			}
		}
		else if((0x30 & PINE) == 0x10){ // 2번째 스위치를 눌렀을때 초기화
			tenths_of_seconds = 0;
			seconds = 0;
			minutes = 0;
		}

		
		fnd[0] = minutes; //분
		fnd[1] = seconds / 10; // 10's
		fnd[2] = seconds % 10; // 1's
		fnd[3] = tenths_of_seconds /10; // ms

		for(i = 0; i < 4; i++){ // 멀티 디스플레이 해주는 코드 
			PORTC = seg[fnd[i]];
			if(i == 2||i==0) PORTC |= 0x80;
			PORTG = (0x08 >> i);
			if (i%2==0)
			{
				_delay_ms(2);
				}else{
				_delay_ms(3);
			}
		}
	}
	return 0;
}

```