---
layout: single
title: "[ATmega128]인터럽트(Interrupt)"
categories: ["theory"]
tag: [ATmega128]

toc: true
toc_label: "Table of Contents"
toc_icon: "align-justify" # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

># 인터럽트(Interrupt)

* **인터럽트(Interrupt)** 란 프로그램이 수행되는 도중 어떤 조건에 의해 인터럽트 요청이 발생하면 프로그램이 일시적으로 중지하는 조건을 말한다.
* 인터럽트가 요청이 발생하면 프로그램을 일시적으로 중지하고 인터럽트를 처리하는 프로그램인 **ISR(Interrupt Service Routine, 인터럽트 서비스 루틴)** 함수를 수행하게 되게 된다. 그리고 **ISR** 이 종료되면 수행 중이었던 프로그램으로 다시 돌아오게 된다. 이는 **함수 호출(Function Call)** 의 개념과 일치한다.
* **ISR** 은 동시에 여러 가지가 실행될 수 없다. 즉, 어떤 **ISR** 이 수행되는 도중에 다른 인터럽트가 요청되면 그 인터럽트는 무시된다. 하지만 몇몇 예외도 존재한다. 
* 따라서 **ISR** 함수 내부는 간단한 코드만 작성하는 것이 바람직 하며, 절대 **ISR** 함수 내부에서는 딜레이 함수나 반복문을 사용하지 않아야 한다.

## 인터럽트(Interrupt) 종류

ATmega128에는 총 35개의 인터럽트가 있다. 상세한 인터럽트의 내용은 사용하는 분야가 올 때 더 자세히 살펴볼 예정이다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/interrupt1.PNG?raw=true)|
|:--:|
|*[Interrupt (Reference : ATmega128 datasheet page 60)]*|

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/interrupt2.PNG?raw=true)|
|:--:|
|*[Interrupt (Reference : ATmega128 datasheet page 60)]*|

## 외부 인터럽트(External Interrupt)

* **외부 인터럽트(External Interrupt)** 는 외부의 조건에 의해 요청되는 인터럽트를 말한다. 외부 조건을 감지할 때 입력 펄스의 상승엣지, 하강 엣지, 레벨로 입력할 수 있다.
* **외부 인터럽트**는 핀을 출력으로 사용할 때 발생하고 소프트웨어 인터럽트를 발생하는 방법으로 사용된다.
* 총 8개의 **외부 인터럽트**가 존재하며 INT 3 ~ 0핀, INT 7 ~ 4 핀 4개씩 그룹으로 묶여있다. 
	* INT3:0 핀은 PD0 ~ PD3에 매칭되고 I/O클럭이 있어야 사용 가능하다.
	* INT7:4 핀은 PE4 ~ PE7에 매칭되고 비동기식 검출이 가능하다.

> EICRA - 외부 인터럽트 제어 레지스터 A

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EICRA%20page%2090.PNG?raw=true)|
|:--:|
|*[EICRA (Reference : ATmega128 datasheet page 90)]*|

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EICRA%20table%20page%2091.PNG?raw=true)|
|:--:|
|*[EICRA Table (Reference : ATmega128 datasheet page 91)]*|

> EICRB - 외부 인터럽트 제어 레지스터 B

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EICRB%20page%2091.PNG?raw=true)|
|:--:|
|*[EICRB (Reference : ATmega128 datasheet page 91)]*|

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EICRB%20table%20page%2091.PNG?raw=true)|
|:--:|
|*[EICRB Table (Reference : ATmega128 datasheet page 91)]*|

> EIMSK - 외부 인터럽트 마스크 레지스터


* **SREG** 의 bit 7이 1로 설정되었을 때 비트를 1로 설정하면 해당 비트의 설정한 핀을 활성화 시킬 수 있다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EIFR%20page%2092.PNG?raw=true)|
|:--:|
|*[EIFR (Reference : ATmega128 datasheet page 91)]*|

> EIFR - 외부 인터럽트 플래그 레지스터


* 외부 또는 내부에서 해당 핀에 인터럽트가 요청되면 해당 비트는 1로 설정된다. 다시 인터럽트가 실행 될 때 0으로 설정된다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/EIMSK%20page%2092.PNG?raw=true)|
|:--:|
|*[EIMSK (Reference : ATmega128 datasheet page 91)]*|

> SREG - 상태 레지스터


* 외부 인터럽트를 제어할 때 사용하는 레지스터로 허가 및 금지를 할 수 있다.
* ATmega128의 상태 결과를 보여주며 ALU 연산 수행 후 갱신하는 역할을 한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/SREG%20page%2011.PNG?raw=true)|
|:--:|
|*[SREG (Reference : ATmega128 datasheet page 11)]*|

> Reference

[1] [ATmega128 datasheet](https://www.alldatasheet.com/view.jsp?Searchword=Atmega128%20datasheet&gclid=CjwKCAjwxZqSBhAHEiwASr9n9BnM2BYUT8UYk14wDrEEu2xSXP17kQdJLfsgKoZNEAQW1gyPJWnHxBoCnYgQAvD_BwE)    
[2] [https://m.blog.naver.com/gjs1029/221098320900](https://m.blog.naver.com/gjs1029/221098320900)
