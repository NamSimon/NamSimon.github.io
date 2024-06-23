




```c
#include <avr/io.h>
#include <util/delay.h>


int main(){
	unsigned char seg[16] = {0x3f, 0x06, 0x5b, 0x4f, 0x66,0x6d,0x7d,0x07,
	0x7f, 0x67, 0x77, 0x7c, 0x58,0x5e,0x79, 0x71}; // 0~F까지 나타내는 코드
	int i=0;
	DDRC = 0xFF;//모든 등 출력모드
	DDRG = 0x0F; // 모든위치 가능하게함
	while(1){
		for(i=0;i<4;i++){//1~4 가능하게하는코드
			PORTC = seg[i+1];
			PORTG = (0x8 >> i);//자리이동 1000 -> 0100 -> 0010 -> 0001
			_delay_ms(5);//5ms 간격
		}
	}
	return 0;
}
```