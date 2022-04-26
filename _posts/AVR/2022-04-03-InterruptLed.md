---
layout: single
title: "[ATmega128]Falling edge Interrupt LED 제어"
categories: ["basic"]
tag: [ATmega128]

toc: true
toc_label: "Table of Contents"
toc_icon: "align-justify" # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

># Falling edge Interrupt LED 제어

이론 파트에서 정리한 인터럽트를 활용해서 LED를 제어하려 한다.    


C++을 어느정도 익힌 사람이라면 **함수 호출**의 개념을 알고 있을 것이다. 인터럽트도 마찬가지로 **함수 호출**의 개념이라고 생각하면 편하다.

## 하드웨어 설계

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/interruptLEDBasic.PNG?raw=true)|
|:---:|
|*[Interrupt Led (Reference : Proteus 8)]*|

## 소스코드

```cpp
#define F_CPU 16000000UL
#include <avr/io.h>
#include <avr/interrupt.h>

unsigned char led = 0x00;	//LED 초기값
unsigned char sw = 0x10;	//SW 초기값

int main(void){
	
	DDRB = 0xff;	//B포트 출력 설정
	DDRE = 0x00;	//E포트 입력 설정
	
	PORTB = led;	//LED 초기값 설정(LED OFF 상태)
	PORTE = sw;		//풀업 저항 구현
		
	EIMSK = 0x10;	//INT 4번핀 활성화
	EICRB = 0x02;	//INT 4번핀 falling edge 동작
	sei();			//전역 인터럽트 허용
		
	while(1);	//무한 반복
}

ISR(INT4_vect){		//INT 4번핀 인터럽트
	led = led<<1;	//LED shift 연산
	led |= 0x01;	//LED 증가 연산
	if(led == 0xff) led = 0x00;	//LED가 다 켜지면 초기화
	PORTB = led;	
	}
```


### 소스코드 구성
---

```cpp
#include <avr/interrupt.h>
```
* 인터럽트를 사용하기 위해서 헤더파일을 선언했다.

```cpp 
	DDRB = 0xff;	//B포트 출력 설정
	DDRE = 0x00;	//E포트 입력 설정
	
	PORTB = led;	//LED 초기값 설정(LED OFF 상태)
	PORTE = sw;		//풀업 저항 구현
```
* 입출력 설정
	* LED를 제어할 **B포트**는 **출력(0xff)** 으로 설정하고 스위치를 제어할 **E포트**는 **입력(0x00)** 으로 설정했다.
	* 풀업 저항으로 구현하기 위해 E포트 방향을 입력으로 설정하고 스위치와 연결된 E포트 4번핀의 값을 1로 설정했다.

```cpp 
	EIMSK = 0x10;	//INT 4번핀 활성화
	EICRB = 0x02;	//INT 4번핀 falling edge 동작
	sei();			//전역 인터럽트 허용
```
* 인터럽트 설정
	* **EIMSK = 0x10;(0b0001_0000)** 을 선언해 INT 4번핀을 활성화시켰다.
	* **EICRB = 0x02;(0b0000_0010)** 은 EICRB Table을 살펴보면 하강에지로 설정 값이 정해져있다.

 |![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EICRB%20table%20page%2091.PNG?raw=true)|
|:--:|
|*[EICRB Table (Reference : ATmega128 datasheet page 91)]*|

* 하강에지(Falling edge)
	* **falling edge**는 상태 1에서 0으로 변화하는 순간을 뜻한다.
	* INT 4번핀을 **falling edge**로 설정한 이유는 스위치를 풀업으로 구성했기 때문이다. 풀업 저항으로 스위치를 구성하면 스위치가 열린 상태에서 HIGH값이 읽히고 닫힌 상태에선 LOW값이 읽히게 된다. 즉, **상태 1에서 0으로 변화하는 순간** 인터럽트가 발생해야 하므로 하강에지를 사용한 것이다.

```cpp
ISR(INT4_vect){		//INT 4번핀 인터럽트
	led = led<<1;	//LED shift 연산
	led |= 0x01;	//LED 증가 연산
	if(led == 0xff) led = 0x00;	//LED가 다 켜지면 초기화
	PORTB = led;	
	}
```
* ISR(Interrupt Service Routine) 구성
	* LED는 초기값을 0x00으로 설정해서 LED의 불이 꺼져있는 상태이다. **shift 연산**을 통해 스위치가 누른 순간마다 **(인터럽트 호출이 될 때마다)** LED에 불이 하나씩 켜지게 되는 구성이다.