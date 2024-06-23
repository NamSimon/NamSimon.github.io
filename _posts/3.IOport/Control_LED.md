





```c
#include <avr/io.h>
#include <util/delay.h>

int main(void)

{
    /*
        보드에 적용된 LED를 500ms 간격으로 깜박이는 코드

        DDRA : A핀에 연결된 LED를 출력으로 설정

        PORTA : A핀에 연결된 LED를 1로 설정하면 LED가 켜지고 0으로 설정하면 LED가 꺼진다.

        _delay_ms : 500ms 대기

     */
    DDRA = 0xFF; // A핀에 연결된 LED를 출력으로 설정
    while (1) {

        PORTA = 0xFF; // A핀에 연결된 핀 모두 1로 설정

        _delay_ms(500);// 500ms 대기

        PORTA = 0x00; // A핀에 연결된 핀 모두 0으로 설정

        _delay_ms(500);// 500ms 대기

    }

}
```