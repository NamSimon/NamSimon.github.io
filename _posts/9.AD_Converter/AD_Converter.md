
# 조도센서

![[Pasted image 20240614205618.png]]


![[Pasted image 20240614205634.png]]


# Analog-to-digital converter (ADC)

- 아날로그 신호를 디지털 신호로 변환하는 장치
- 아날로그 신호 =온도, 유량, 초음파 등등 각종 센서들의 신호
- microcontroller 에서는 아날로그 -> 디지털 신호 전환

![[Pasted image 20240614205812.png]]

## ATmega128의 A/D 변환기 특징

- 10-bit  분해능(resolution)
- 12~260 $\mu s$ 변환 시간(conversion time) 
- 8개의 단극성 입력 채널 (Single Ended Input Channels)
- 7개의 차등 입력 채널(Differential Input Channels)
- 22개의 차동 입력 모드
- 10배와 200배 증폭을 갖는 2개의 차동 입력 채널
- 선택 가능한 2.56V 내부 기준 전압

## ATmega128의 A/D 변환기 핀

- A/D 변환기는 8채널 아날로그 입력(ADC0~ADC7) : 포트 F

![[Pasted image 20240614212031.png]]

## A/D 변환기 블록도

![[Pasted image 20240614212105.png]]

## A/D 변환기 관련 레지스터

|   레지스터    |                               기능                               |
| :-------: | :------------------------------------------------------------: |
|   ADMUX   | A/D 변환기 멀티 플렉서 선택 레지스터<br>(ADC Multiplexer Selection Register) |
|  ADCSRA   |  A/D변환기 제어 및 상태 레지스터 A<br>(ADC Control and Status Register A)  |
| ADCH,ADCL |            A/D 변환기 데이터 레지스터<br>(ADC Data Register)             |


## ADMUX(ADC Multiplexer Selection Register)

![[Pasted image 20240614213101.png]]

- REFS1, REFS0(Reference Selection Bits) : A/D 변환기 기준 전압 선택

![[Pasted image 20240614213823.png]]


 
## ADLAR(ADC Left Adjust Result)

- A/D 변환 결과 값 저장 형식 지정(ADCH & ADCL)
![[Pasted image 20240614213915.png]]

## MUX4~MUX0(Analog Channel and Gain Selection Bits)

![[Pasted image 20240614214013.png]]
![[Pasted image 20240614214022.png]]


## ADCSRA(ADC Control and Status Register A)

![[Pasted image 20240614214038.png]]

### ADEN(ADC Enable)

- ADEN =1 -> A/D 변환기 동작 가능
- ADEN =0 -> A/D  변환기 동작 정지, 소비 전력이 감소

### ADSC(ADC Start Conversion)

- 단일 변환(single conversion)에서 ADSC =1 -> A/D 변환 시작
- 프리러닝 변환(free running conversion)에서 ADSC =1 -> 첫번째 A/D변환 후 자동적으로 A/D 변환 계속됨

### ADFR(ADC Free Running Select)

- ADFR=1 -> A/D 변환기 프리 러닝 변환
- ADFR=0 -> A/D 변환기는 단일 변환

## ADIF(ADC Interrupt Flag)

- ADIF=1 : A/D 변환 완료
- A/D 변환 완료 인터럽트 발생
- ADIF를 강제적으로 클리어시키려면 ADIF=1로 라이트시켜야 함

## ADIE (ADC Interrupt Enable)

## ADPS2 ~ ADPS0(ADC Prescaler Select Bits)

![[Pasted image 20240614214534.png]]


## ADCH, ADCL(ADC Data Register)

- 10비트의 A/D 변환 결과 값을 저장
	- ADC = 0x00(0)~0x3FF(1023)
- 위 단극성 입력, 아래 차동입력 

![[Pasted image 20240614214636.png]]

### 단극성 입력의 A/D 변환 결과

- VREF : 기준 전압(5V) 
- VIN : 단극성 입력 채널의 전압
$$ ADC=0   =>  V_{IN} = 0V$$

$$ADC=0x3FF(1023) => V_{IN}=V_{REF}
(=5V)$$
$$ ADC=
\frac{V_{IN} \times 1023 }{V_{REF}} \;\;\;\;\;\; V_{REF}=
\frac{V_{IN} \times 1023 }{ADC}  $$
$$ 100 \; lux \; : V_{IN} = 4.76 \sim 4.9\;[V] \;\Rightarrow \; ADC=973\sim 1002$$

$$ 10\;\;lux : V_{IN}=4\sim4.55[V] \;\Rightarrow \; ADC=818\sim930$$
$$Dark \;\; : V_{IN}=0.45[V]\;\;\Rightarrow\;\; ADC=92$$

### 차동 입력의 A/D 변환 결과 (2's complement)

-  $V_{POS}$  :  차동 입력의 (+) 입력 전압
- $V_{NEG}$ : 차동입력의 (-) 입력 전압
- $V_{DIFF} = V_{POS} -  V_{NEG}$

![[Pasted image 20240614224010.png]]



# 예제 
----
[예제1](./예제1)
[예제2](./예제2)
[예제3](./예제3)