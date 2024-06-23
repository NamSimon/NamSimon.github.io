# I / O 포트

## ATmega128 I/O 포트
- 8 비트 단위의 Read-Modify-Write 기능을 갖는 7개의 범용 입/출력(I/O) 포트를 가지고 있음

  ![alt text](Atmega128/3.IOport/image.png)

- I/O 포트
  - 마이크로 컨트롤러가 외부와 인터페이스할때 사용하는 입 /출력 핀들의 묶음
  
  ![alt text](Atmega128/3.IOport/image-1.png)

**※ 풀업 저항 사용 여부는 SFIOR 레지스터의 PUD 비트로 설정**

- I/O 포트 동작을 위해 각 I/O 포트마다 3개의 레지스터를 사용(8bit 이용한다는 뜻)

![](Atmega128/3.IOport/image-2.png)


![alt text](Atmega128/3.IOport/image-3.png)




## DDRx 레지스터

- I/O 포트의 입/출력 방향을 설정하는 레지스터
  
  - DDRA, DDRB, DDRC, DDRD, DDRE, DDRF, DDRG 
  - DDxn = 0 → Pxn 핀은 입력으로 설정
  - DDxn = 1 → Pxn 핀은 출력으로 설정
  

  ![alt text](Atmega128/3.IOport/image-4.png)




## PORTx 레지스터


- I/O 포트에 데이터를 출력하기 위해 사용하는 레지스터



  - PORTA, PORTB, PORTC, PORTD, PORTE, PORTF, PORTG
  - PORT 레지스터에 출력할 데이터를 라이트하기 전에 DDR 레지스터로 I/O 포트를 출력으로 설정해야 함



![alt text](Atmega128/3.IOport/image-5.png)



## PIN 레지스터

- I/O 포트에 데이터를 입력받기 위해 사용하는 레지스터
  - PINA, PINB, PINC, PIND, PINE, PINF, PING
  - I/O 포트로 입력된 데이터를 PIN 레지스터에서 리드하기 전에 DDR 레지스터로 I/O 포트를 입력으로 설정해야 함



![alt text](Atmega128/3.IOport/image-6.png)



## LED 점등 제어


![alt text](Atmega128/3.IOport/image-7.png)



## Switch 제어
![alt text](Atmega128/3.IOport/image-8.png)




## FND(Flexible Numeric Display) 제어

![](Atmega128/3.IOport/image-9.png)




![alt text](Atmega128/3.IOport/image-10.png)



## FND 포트 맵

![alt text](Atmega128/3.IOport/image-11.png)




# 실습 예제
--------------------------------------

[LED 예제](Control_LED.md)
[스위치,LED 예제](Control_Switch_LED.md)
[FND 점등](FND_onoff.md)
[FND 여러개 점등](Muti_Display_FND.md)

## 과제
---------------
[LED과제](Practice_LED)
[FND과제](Practice_FND)