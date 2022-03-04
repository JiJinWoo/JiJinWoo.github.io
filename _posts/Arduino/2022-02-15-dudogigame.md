---
layout: single
title: "[아두이노]두더지잡기 게임"
categories: ["arduino"]
tag: [arduino]
author_profile: true
sidebar_main: true
---


> **설명**

LED와 SW, LCD를 이용해서 간단한 두더지 잡기 게임을 구현한다.


하드웨어 설계에서 LED는 두더지, SW(스위치)는 두더지를 잡는 망치를 나타내고, LCD화면 상에 게임 진행 상태를 출력할 수 있도록 설정한다.

---

> __사용한 부품__

|부품명|수량|설명|
|:---:|:---:|:---:|
|아두이노 우노|1|  |
|LED|3|  |
|SW|3|  |
|220Ω 저항|4|  |
|LCD|1|LCM1602|
|가변저항|1|1~2KΩ으로 교체가능|

---

> **[회로도]하드웨어 설계**

LCD마다 Data sheet가 다르기 때문에 해당하는 Data sheet에 맞게 연결해야 한다.
SW는 소스코드에서 PULLUP 회로로 구성한다.

![circuit](https://raw.githubusercontent.com/JiJinWoo/JiJinWoo.github.io/master/assets/images/dudogigame.PNG)


|LCD(LCM1602A)|1|2|3|4|5|6|7|8|9|10|11|12|13|14|15|16|
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|핀 명|VSS|VDD|V0|RS|R/W|E|DB0|DB1|DB2|DB3|DB4|DB5|DB6|DB7|A|K|
|아두이노 핀|GND|VCC| |2|3|4|  |  |  |  |5|6|7|8|VCC|GND|

---

> **[소스코드]소프트웨어 설계**

LCD를 쉽게 사용하기 위해 ```LiquidCrystal.h``` 헤더파일을 설치해준다.


아두이노 IDE -> 스케치 ->  라이브러리 포함하기 -> 라이브러리 관리 -> LCD검색 
이후 라이브러리에서 ```LiquidCrystal``` 불러온다.


```LiquidCrystal.h``` 의 함수는  아두이노 [**Reference**](https://www.arduino.cc/en/Reference/LiquidCrystal)에서 자세한 사항을 확인할 수 있다.
![LCD](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/LCDIMAGE.PNG?raw=true)



LED, SW, LCD의 핀 번호들과 게임에서 사용할 변수를 전역변수로 설정한다.
```cpp
#include <LiquidCrystal.h>	//LCD를 사용하기 위한 헤더파일

LiquidCrystal lcd(2, 3, 4, 5, 6, 7, 8);	//2~8번 핀을 사용하기 위한 LCD객체생성

int led[] = {A0, A1, A2};	//두더지를 A0~A2 핀으로 설정
int sw[] = {9, 10, 11};		//망치를 9~11번 핀으로 설정

int rand_num; //무작위로 켜지는 Led와 Sw 번호
int count = 0;  //두더지 잡은 수
int total_game = 10; //총 게임진행 횟수
int ending = 0;	//게임 종료 변수
```


SW를 사용할 땐 PULL-UP/PULL-DOWN회로를 직접 구성해서 할 수도 있지만 아두이노에선 ```pinMode()``` 코드로 구현된 ```INPUT_PULLUP```을 사용할 수 있다.
```cpp
void setup(){
  for(int i = 0; i < 3; i++){
    pinMode(led[i], OUTPUT);	//LED에 연결된 핀들을 OUPUT으로 설정
    pinMode(sw[i], INPUT_PULLUP);	//SW에 연결된 핀들을 INPUT_PULLUP으로 설정 
  }
  lcd.begin(16,2);	//LCD화면에 16개의 셀을 2줄로 출력하도록 설정
  lcd.clear();	//LCD 초기화
}
```
```cpp
void loop(){
  if(ending == 0){	//게임종료를 위한 변수
    if(digitalRead(sw[0]) == LOW){	//Sw[0]을 게임시작 스위치로 설정 
      ending = 1;
      gameStart();	//함수호출
      startLcd();	//함수호출
    }
  }
  else if(total_game == 0){	//게임종료
    endLcd();	//함수호출
    ending = 0;
  }
  else{
    rand_num = random(0, 3);	//0~2번 중 무작위 두더지 선정
    switch(rand_num){
      case 0:
      dudogi();
      total_game--;	//게임 진행횟수 감소
      break;

      case 1:
      dudogi();
      total_game--;
      break;

      case 2:
      dudogi();
      total_game--;
      break;
    }
  }
  delay(1000);	//다음 두더지 선정 대기시간
}
```


반복되는 게임 진행을 위해```void dudogi()``` 함수를 만들어 사용한다.
```cpp
void dudogi(){
  for(int i = 0; i < 20; i++){
    if(total_game == 0){	
      break;	//모든 게임이 진행됐다면 종료
    }
    else if(digitalRead(sw[rand_num]) == LOW){
      analogWrite(led[rand_num], 0);
      count++;	//두더지 잡은 수 증가
      lcd.setCursor(10, 1);	//LCD 화면 10번째 셀, 2번째 줄로 이동
      lcd.print(count);	//count 출력
      break;
    }
    else{
      analogWrite(led[rand_num], 255);
      delay(100);	//0.1초마다 스위치가 눌러졌는지 확인
      analogWrite(led[rand_num], 0);
    }
  }
}
```
```cpp
void gameStart(){	//게임이 시작될 때 LCD에 표시될 내용
  lcd.setCursor(0,0);
  lcd.print("3");
  delay(1000);
  lcd.print("2");
  delay(1000);
  lcd.print("1");
  delay(1000);
  lcd.setCursor(0,0);
  lcd.print("GameStart");
  delay(1000);
}

void showScore(){	//게임이 진행되는 상황을 LCD에 표시해주는 함수
  lcd.setCursor(0,0);
  lcd.print("Total : ");
  lcd.print(total_game);
  lcd.setCursor(0,1);
  lcd.print("Success : ");
}

void showResult(){	//게임이 끝나고 결과를 LCD에 표시해주는 함수
  lcd.setCursor(0,0);
  lcd.print("----THE END----");
  lcd.setCursor(0,1);
  lcd.print("Result : ");
  lcd.print(count);
  lcd.print("!!!");
}
```
---

> **참고사항**

* 참조 : [**https://kocoafab.cc/make/view/443**](https://kocoafab.cc/make/view/443) 

* LED를 디지털 핀에 연결해서 사용해도 무관하다. 여기서 아날로그 핀으로 연결한 이유는 LCD와 SW를 사용하게 되면서 디지털 핀의 개수가 부족하다고 판단했다.

* 부품이 부족해서 초기화 버튼과 더 많은 LED와 SW를 사용하지 못한 점이 있다. 부품의 여유가 있다면 더 많은 부품들을 사용해서 더 난이도 있는 두더지잡기 게임을 만들 수 있다.

* LCD 3번 핀(V0)에 굳이 가변저항을 사용하지 않고 1~2KΩ 저항을 사용해도 무관하다. LCD 마다 차이가 있지만 여기서 가변저항을 사용한 이유는 저항 값을 직접 조정하면서 화면의 선명도를 높이기 위해 사용했다.

* ```delay()``` 함수의 시간을 더 짧게 만들어서 더 난이도 있는 게임을 만들 수 있다.

* 피에조를 사용해서 소리를 낼 수 있게 구현할 수 있다.