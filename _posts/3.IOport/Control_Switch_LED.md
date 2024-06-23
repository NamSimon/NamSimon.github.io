```c
#include<avr/io.h>
int main(){
	char tmp;
	DDRA = 0xFF; //LED 출력 설정
	DDRE = 0x00; // 입력 설정 
	while(1){
		tmp = 0x30 & PINE; // 스위치 1,2가 눌렸는지 보는 코드 눌리면 0 안눌리면 1
		if( tmp == 0x00 ) //두개다 눌렸을때
		{
			PORTA = 0x01;//0000 0001
		}
		if( tmp == 0x20 ) // 첫번째 스위치가 눌렸을때 
		{
			PORTA = 0x0c; //0000 1100
		}
		
		if( tmp == 0x10 ) //2번째 스위치가 눌렸을때
		{
			PORTA = 0x10; //0001 0000
		}
		
		if( tmp == 0x30 ) //하나도 눌리지 않았을때 
		{
			PORTA = 0xc0; //1100 0000
		}
	}
}
```