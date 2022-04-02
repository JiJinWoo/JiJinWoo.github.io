---
layout: single
title: "[ATmega128]타이머/카운터(Timer/Counter)"
categories: ["theory"]
tag: [ATmega128]

toc: true
toc_label: "Table of Contents"
toc_icon: "align-justify" # corresponding Font Awesome icon name (without fa prefix)
toc_sticky: true
---

># 타이머/카운터(Timer/Counter)

**타이머/카운터(Timer/Counter)** 는 말 그대로 시간을 측정하는데 쓰인다. 또한 **PWM(Pulse Width Modulation)** 신호를 만드는데도 사용한다.

> 타이머(Timer)

* MCU 내부 시스템 **클럭(clk)** 을 세는 장치이며 시스템 클럭의 변화를 감지한다.
	* **클럭**이란 일정한 시간 간격으로 **0** 과 **1**이 반복하는 하여 시간을 측정할 때 사용한다.
* 일정시간 간격의 펄스를 만들어 내거나 일정한 시간이 지나면 인터럽트를 발생시킨다.
* 동기 모드이다.

> 카운터(Counter)

* **카운터**는 클럭의 **한 주기**를 뜻하며 클럭을 세는 장치이기도 하다.
* 외부 핀에서 들어오는 펄스를 세는 장치이며 외부 입력의 변화를 감지한다.
* 외부핀을 통해 들어오는 펄스의 수를 확인해 이벤트 카운터로 동작한다.
* 비동기 모드이다.



## 타이머/카운터 특징

ATmega128에는 총 4개의 타이머가 존재한다. 

> Timer/Counter0, 2(TCNT0, TCNT2)

* **8bit 타이머**이다. 즉, **TCNT0**와 **TCNT2**는 **0~255(8bit)** 까지의 값을 가질 수 있다.
* 오버플로우나 PWM과 같은 기능을 보유하고 있다.
* **TCNT0**는 **RTC(Real Time Clock)** 기능을 보유하고 있으며 다른 타이머와는 다르게 외부, 내부 클럭을 사용할 때 **프리스케일러(Prescaler)** 의 분주 기능이 사용 가능하다.
	* **Prescaler**는 타이머에 공급하는 입력 클럭 속도를 조절하는 분주기이다. 최대 1024배까지 조절이 가능하다.

> Timer/Counter1, 3(TCNT1, TCNT3)

* **16bit 타이머**이다. 즉, **TCNT1**과 **TCNT3**는 **0~65535(16bit)** 까지의 값을 가질 수 있다.
* 인터럽트 기능을 수행하고 PWM 출력 기능도 가지고 있다.


## 타이머/카운터 레지스터(8bit)

> TCCRn(Timer/Counter Control Register n = 0, 2)

* 타이머/카운터를 제어하기 위한 레지스터이다.
* **동작모드(WGM0n : Waveform Generation Mode n = 0, 1)**, **프리스케일러(CS0n, n = 0~2)**, **비교출력모드(COM0n : Compare Output Mode n = 0, 1)**, **핀제어(FOC0 : Force Ouput Compare)** 등 전반적인 동작 형태를 결정한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/TCCR0%20page%20104.PNG?raw=true)|
|:--:|
|*[TCCR0 (Reference : ATmega128 datasheet page 104)]*|

* 동작 모드(WGM0n : Waveform Generation Mode n = 0, 1)

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/Waveform%20Generation%20Mode%20page%20105.PNG?raw=true)|
|:--:|
|*[Waveform Generation Mode Table (Reference : ATmega128 datasheet page 105)]*|

* 프리스케일러(CS0n : Clock Select n = 0~2)

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/Prescaler%20page%20106.PNG?raw=true)|
|:--:|
|*[Clock Select Table (Reference : ATmega128 datasheet page 106)]*|

> TCNTn(Timer/Counter Register n = 0, 2)

* **TCNT0**는 8bit로  0~0xff까지 카운트를 세며 0xff가 되면 **오버플로우 인터럽트**가 발생한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/TCTN0%20page%20106.PNG?raw=true)|
|:--:|
|*[TCNT0 (Reference : ATmega128 datasheet page 106)]*|

> OCRn(Output Compare Register n = 0, 2)

* **OCRn**는 TCNTn과 값이 같아지면 **비교일치 인터럽트**가 발생하고 **OCn** 핀에 출력을 제어한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/OCR0%20page%20106.PNG?raw=true)|
|:--:|
|*[OCR0 (Reference : ATmega128 datasheet page 106)]*|

> ASSR(Asynchronous Status Register)

* TCNT0가 비동기 모드로 동작하는 경우 제어를 담당하는 레지스터이다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/ASSR%20page%20107.PNG?raw=true)|
|:--:|
|*[ASSR (Reference : ATmega128 datasheet page 107)]*|

> TIMSK(Timer/Counter Interrupt Mask Register)

* **TIMSK**는 인터럽트를 활성화시킬 수 있는 레지스터이다.
* **bit 0 - TOIE0** 를 **set(1)** 하면 **오버플로우 인터럽트**를 활성할 수 있다.
* **bit 1 - OCIE0** 를 **set(1)** 하면 **비교일치 인터럽트**를 활성화 할 수 있다. 

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/TIMSK%20page%20109.PNG?raw=true)|
|:--:|
|*[TIMSK (Reference : ATmega128 datasheet page 109)]*|

> TIFR(Timer/Counter Interrupt Flag Register)

* **TIFR**은 발생한 인터럽트의 플래그 값을 저장하는 레지스터이다.
* TCNTn에서 **오버플로우가 발생**하면 **bit 0 - TOV0**가 **set(1)** 되어 **오버플로우 인터럽트**가 발생한다.
*  TCNTn과 OCRn 값이 **비교일치**되면 **bit 1 - OCF0**가 **set(1)** 되어 **비교일치 인터럽트**가 발생한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/TIFR%20page%20109.PNG?raw=true)|
|:--:|
|*[TIFR (Reference : ATmega128 datasheet page 109)]*|

> SFIOR(Special Fucntion IO Register)

* 타이머/카운터를 **동기화**하는데 사용하는 레지스터이다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/SFIOR%20page%20110.PNG?raw=true)|
|:--:|
|*[SFIOR (Reference : ATmega128 datasheet page 110)]*|

## 타이머/카운터 동작

타이머/카운터의 주된 용도는 **시간 측정**이다. **시간 측정**은 클럭의 개수를 카운트하는 것이다.
* EX) 클럭이 100Hz의 주기로 펄스를 발생시킨다면 총 100번의 카운팅 진행되면 1초가 지난 것이다.

> Normal Mode

* 타이머/카운터의 가장 기본적인 모드이다.
* 클럭 인가시 TCNTn이 1씩 증가 또는 감소하는 동작 모드이다.
* **최대 카운트(0xff)** 가 되면 **오버플로우 인터럽트(OVF: OverFlow)** 가 발생하고 그 후 다시 0부터 카운트의 기능을 수행한다.


> CTC Mode(Clear Timer on Compare Match)

* TCNTn이 OCRn 값까지만 증가하고 TCNTn과 OCRn의 값이 같아지면 **비교일치 인터럽트(COMP : Compare Match Interrupt)** 가 발생한다. 그 후 다시 TCNTn은 0부터 카운트의 기능을 수행한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/CTC%20mode%20page%2098.PNG?raw=true)|
|:--:|
|*[CTC Mode (Reference : ATmega128 datasheet page 98)]*|

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/non%20PWM%20mode%20page%20105.PNG?raw=true)|
|:--:|
|*[non-PWM Mode Table (Reference : ATmega128 datasheet page 105)]*|


> Fast PWM Mode

* PWM의 한 주기는 TCNTn이 0xff까지 증가하는데 걸리는 시간이 된다.
* **COMn 1:0 = 2**일 때 OCn이 HIGH(5V)로 시작하며 TCNTn이 증가하다가 OCRn과 값이 같아지면(비교일치) OCn이 LOW(0V)로 출력된다. 이후 TCNTn이 오버플로우가 발생하여 값이 0이되면 다시 OCn에서 HIGH(5V)가 출력된다.
* **COMn 1:0 = 3**일 때는 OCn이 **토글**된 상태이다. 즉, OCn이 LOW(0V)로 시작한다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/Fast%20PWM%20mode%20page%20100.PNG?raw=true)|
|:--:|
|*[Fast PWM Mode (Reference : ATmega128 datasheet page 100)]*|

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/Fast%20PWM%20mode%20page%20105.PNG?raw=true)|
|:--:|
|*[Fast PWM Mode Table (Reference : ATmega128 datasheet page 105)]*|


> Phase Correct PWM

* **COMn 1:0 = 2**일 때 TCNTn이 0부터 0xff까지 증가되면 다시 0xff부터 0까지 감소를 반복한다.
* **상향 카운터**일 때 OCRn과 비교일치되면 OCn은 LOW(0V)가 출력되고 **하향 카운터**일 때 OCRn과 비교일치되면 OCn은 HIGH(5V)가 출력된다.

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/Phase%20Correct%20PWM%20page%20101.PNG?raw=true)|
|:--:|
|*[Phase Correct PWM (Reference : ATmega128 datasheet page 87)]*|

|![blog](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/avrblog/Phase%20Correct%20PWM%20page%20106.PNG?raw=true)|
|:--:|
|*[Phase Correct PWM Table (Reference : ATmega128 datasheet page 106)]*|

> Reference

[1] [ATmega128 datasheet](https://www.alldatasheet.com/view.jsp?Searchword=Atmega128%20datasheet&gclid=CjwKCAjwxZqSBhAHEiwASr9n9BnM2BYUT8UYk14wDrEEu2xSXP17kQdJLfsgKoZNEAQW1gyPJWnHxBoCnYgQAvD_BwE)    
[2] [https://m.blog.naver.com/gjs1029/221098320900](https://m.blog.naver.com/gjs1029/221098320900)