
```c
#include <avr/io.h>
#include <util/delay.h>

int main(){
	unsigned char seg[16] = {0x3f, 0x06, 0x5b, 0x4f, 0x66,0x6d,0x7d,0x07,
	0x7f, 0x67, 0x77, 0x7c, 0x58,0x5e,0x79, 0x71}; // 0~F까지 나타내는 코드
	int n=0;
	DDRC = 0xFF;// 그 위치에서 불을 얼마나 킬지 설정
	DDRG = 0x0F;//위치 관련된 설정 코드 ex)0 0 0 1
	while(1){
		PORTG = 0x01; // 맨 첫번째 위치로 설정
		PORTC = seg[n++]; // 배열 안에 있는 수 불러오기 n인덱스 업데이트
		n %= 10;//10이면 초기화
		_delay_ms(500);// 500ms 딜레이
	}
	return 0;
}

```