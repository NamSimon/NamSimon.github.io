



```c
/*
	다음 기능을 수행하는 코드 
		- 스위치를 누르지 않을 경우 : LED off
		- 1번 스위치를 누를 경우 : LED 불빛이 우측에서 좌측으로 이동(200ms 간격)
		- 2번 스위치를 누를 경우 : LED 불빛이 좌측에서 우측으로 이동(500ms 간격)
		- 스위치를 모두 누를 경우 : LED on
*/

#include <avr/io.h>
#include <util/delay.h>

int main(){
	
	DDRA = 0xFF;//A핀 모두 출력핀 설정 
	DDRE = 0x00; // E핀 모두 입력 핀 설정
	
	while(1)
	{
		char i;

		if(!(0x30 & PINE))// 모든 스위치 눌려 있을경우(E입력이 모두 0일경우)
		{
			PORTA = 0xff;//모든 LED켜짐
		}else if((0x10 & PINE) != 0x10) // 1번째 스위치를 눌렀을경우
		{
			PORTA = i;
			i >>= 1; //우측에서 좌측으로 이동(점점 커짐) ex) 0000 00001 -> 0000 0010 
			if( i == 0) {
				i = 0x80; // 끝이면 우측 마지막 led 켜짐
			}
			_delay_ms(200);	
			
		}else if((0x20 & PINE) != 0x20)// 2번째 스위치를 눌렀을꼉우 
		{
			PORTA = i;
			i <<= 1;//  좌측에서 우측으로 이동 ex) 1000 0000 -> 0100 0000
			if( i == 0 )
			{
				i = 1; // 끝이면 좌측 마지막 led 켜짐
			}
			_delay_ms(500);
			
			
		}else if((0x30 & PINE)) //모든 스위치 안눌려있는경우
		{
			PORTA=0x00;//불 다꺼짐.
		}
		
	}
	
}
```