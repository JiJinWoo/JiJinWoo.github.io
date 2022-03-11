---
layout: single
title: "[Arduino]알람시계"
categories: ["arduino"]
tag: [arduino]
author_profile: true
sidebar_main: true
---



> **설명**

아두이노로 간단한 알람시계를 만들어보았다. LCD 화면에 오늘의 날짜, 시간, 알람이 울릴 시간이 출력된다. 알람이 울릴 시간이 되면 부저가 울리게 되고 스위치를 누르면 알람을 끄고 초기화 시킨다.

---

> __사용한 부품__

|부품명|수량|설명|
|:---:|:---:|:---:|
|아두이노 우노|1|  |
|piezo 부저|1|  |
|SW|1|  |
|220Ω 저항|1|  |
|LCD|1|LCM1602|
|가변저항|1|1~2KΩ으로 교체가능|

---

> **[회로도]하드웨어 설계**

![image](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/ALARM.jpg?raw=true)

![circuit](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/alarmclock.PNG?raw=true)


|LCD(LCM1602A)|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|핀 명|VSS|VDD|V0|RS|R/W|E|DB0|DB1|DB2|DB3|DB4|DB5|DB6|DB7|A|K|
|아두이노 핀|GND|VCC| |2|3|4|  |  |  |  |5|6|7|8|VCC|GND|

---

> **[소스코드]소프트웨어 설계**

LCD를 쉽게 사용하기 위해 라이브러리에서 ```LiquidCrystal.h```를 설치해준다.
시간과 날짜를 LCD 화면 상에 출력하기 위해 라이브러리에서 ```swRTC.h```를 설치해준다.
* swRTC Reference : [**https://github.com/leomil72/swRTC**](https://github.com/leomil72/swRTC)
* LiquidCrystal Reference : [**https://www.arduino.cc/reference/en/libraries/liquidcrystal/**](https://www.arduino.cc/reference/en/libraries/liquidcrystal/)


![LCD](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/LCDIMAGE.PNG?raw=true)

![swRTC](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/swRTC%20%EB%9D%BC%EC%9D%B4%EB%B8%8C%EB%9F%AC%EB%A6%AC%20%EC%B6%94%EA%B0%80.PNG?raw=true)

```cpp
#include <LiquidCrystal.h>
#include <core_build_options.h>
#include <swRTC.h>

LiquidCrystal lcd(2, 3, 4, 5, 6, 7, 8);

swRTC rtc;

int piezo = 9;    //알람 사운드
int sw = 11;      //알람 종료 스위치

int alarmHour = 2;    //알람이 울리는 시
int alarmMinute = 8;  //알람이 울리는 분

void setup(){
  rtc.stopRTC();  //정지
  rtc.setTime(6, 30, 35); //시간, 분, 초 초기화
  rtc.setDate(6, 3, 2022); //일, 월, 년 초기화 
  rtc.startRTC(); //시작

  lcd.begin(16, 2);
  lcd.clear();

  pinMode(piezo, OUTPUT);
  pinMode(sw, INPUT_PULLUP);
}

void loop(){
  //오늘 날짜와 현재 시간 LCD 화면 상에 출력
  lcd.setCursor(0,0);
  lcd.print("[");
  numberPrint(rtc.getMonth());
  lcd.print("/");
  numberPrint(rtc.getDay());
  lcd.print("]");
  setAMPM(rtc.getHours());
  numberPrint(rtc.getHours());
  lcd.print(":");
  numberPrint(rtc.getMinutes());

  //설정된 알람 시간을 LCD 화면 상에 출력
  lcd.setCursor(0,1);
  lcd.print("Alarm");
  lcd.setCursor(7,1);
  setAMPM(alarmHour);
  numberPrint(alarmHour);
  lcd.print(":");
  numberPrint(alarmMinute);

  //지정된 시간에 알람이 울리고 스위치를 누르면 지정된 알람 시간 초기화
  alarmClock(alarmHour, alarmMinute);
  if(digitalRead(sw) == 0){
    analogWrite(piezo, 0);
    alarmHour = 0;
    alarmMinute = 0;
  }
}


void alarmClock(int checkHour, int checkMinute){      //알람이 울리는 시간이라면 알람 울리게 한다
  if(checkHour == rtc.getHours() && checkMinute == rtc.getMinutes()){
  analogWrite(piezo, 128);
  }
}

void setAMPM(int hour){         //AM, PM을 설정해주는 함수
  if(hour >= 12) lcd.print("PM");
  else lcd.print("AM");
}

void numberPrint(int number){   //10보다 작은 수가 출력 될 때 앞에 0을 출력하고 아니면 원래의 숫자 출력
  if(number < 10){
    lcd.print("0");
    lcd.print(number);
  }
  else lcd.print(number);
}
```

```void alrmClock()```는 알람이 울리는 시간을 확인하고 만약 알람이 울리는 시간이라면 피에조 부저에 소리가 나게 한다.
```cpp
void alarmClock(int checkHour, int checkMinute){      //알람이 울리는 시간이라면 알람 울리게 한다
  if(checkHour == rtc.getHours() && checkMinute == rtc.getMinutes()){
  analogWrite(piezo, 128);
  }
}
```
```void setAMPM()``` 는  ```getHours()```에서 받은 시간이 12이상이면 PM을 LCD 화면에 출력하고 12이하라면 AM을 출력하게 하는 함수이다.
```cpp
void setAMPM(int hour){         //AM, PM을 설정해주는 함수
  if(hour >= 12) lcd.print("PM");
  else lcd.print("AM");
}
```
```void numberPrint()```는 10이하의 시간이 입력될 경우 앞의 0을 출력하고 아니면 원래의 숫자를 출력하는 함수이다. 예를 들어 AM7:1 이 AM07:01 로 출력되는 형식이다.
```cpp
void numberPrint(int number){   //10보다 작은 수가 출력 될 때 앞에 0을 출력하고 아니면 원래의 숫자 출력
  if(number < 10){
    lcd.print("0");
    lcd.print(number);
  }
  else lcd.print(number);
}
```

---

> **참고사항**

* 참조 : [**https://www.kocoafab.cc/make/view/144**](https://www.kocoafab.cc/make/view/144)

* 스위치를 누르고 알람을 초기화 시키면 소스코드 상에서 직접 알람시간을 다시 조정해줘야 한다.