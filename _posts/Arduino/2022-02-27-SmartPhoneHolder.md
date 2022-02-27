---
layout: single
title: "[아두이노]스마트폰 거치대"
categories: ["arduino"]
tag: [arduino]
author_profile: true
sidebar_main: true
---




> **개요**

IoT를 구현하고 싶었기에 아이디어를 생각하다가 아두이노로 제어할 수 있는 스마트폰 거치대를 만들어 보기로 했다. 혹시나 하는 마음에 정보를 찾아봤는데 누군가 이미 구현을 해놓았다. 그래서 만들어진 소스코드를 참조해서 조이스틱으로 제어하는 스마트폰 거치대를 구현했다.

---

> __사용한 부품__

|부품명|수량|설명|
|:---:|:---:|:---:|
|아두이노 우노|1|  |
|서보 모터|2| SG90 |
|조이스틱|1|  |

---

> **[회로도]하드웨어 설계**

조이스틱(대체)은 5핀이라 가정한다.

![circuit](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/%ED%9A%8C%EB%A1%9C%EB%8F%84.PNG?raw=true)

![image](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/Merged_document.jpg?raw=true)
서브모터는 팬틸트 거치대(SG90 프레임 거치대)로 고정시켰다.

---

> **조이스틱 설정**

위 회로도와 같이 연결하고 조이스틱 설정을 한다. 조이스틱은 아날로그 포트로 입력을 받아 ADC(Analog to Digital Converter)로 인해 0V ~ 5V 전압이 0 ~ 1023 값으로 변환된다. 


그렇기에 밑의 소스코드를 통해 움직이지 않았을 때 조이스틱의 초기 값이 얼마인지 파악해야 한다.

```cpp
void setup(){
  Serial.begin(9600);
}

void loop(){
  Serial.print("X축");
  Serial.println(analogRead(A0)); // X축 값 표기
  Serial.print("Y축");
  Serial.println(analogRead(A1)); // y축 값 표기 
  delay(1000);                                 
}
```

![circuit](https://github.com/JiJinWoo/JiJinWoo.github.io/blob/master/assets/images/blog/x,y.PNG?raw=true)

---

> **[소스코드]소프트웨어 설계**

서보 모터를 제어하기 위해 ```Servo.h``` 헤더 파일을 추가해준다.


```Servo.h``` 의 함수는  아두이노 [**Reference**](https://www.arduino.cc/reference/en/libraries/servo/)에서 자세한 사항을 확인할 수 있다.

```cpp
#include<Servo.h>   //서브모터 헤더파일
Servo LeftRightMotor;  //서브모터 좌우 클래스 선언
Servo UpDownMotor;     //서브모터 상하 클래스 선언

int LeftRightWidth = 90;      //좌우 서브모터 각도 초기값
int UpDownWidth = 140;         //상하 서브모터 각도 초기값 설정

int xDegree;   //조이스틱 x축(좌우) 값 저장하는 변수
int yDegree;   //조이스틱 y축(상하) 값 저장하는 변수

void setup(){
    LeftRightMotor.attach(9);
    UpDownMotor.attach(10);   
    LeftRightMotor.write(90); //좌우 서브모터 최초각도 설정
    UpDownMotor.write(140);    //상하 서브모터 최초각도 설정
}

void loop(){
  int xSum = 0;  //조이스틱 x축(좌우) 각도 조정 변수
  int ySum = 0;  //조이스틱 y축(상하) 각도 조정 변수

  for(int i = 0; i < 20; i++){    //민감하게 반응하는 조이스틱의 아날로그 값을 추출하여 오차범위 조절
    xDegree = analogRead(A0);
    yDegree = analogRead(A1);
    xSum += xDegree;
    ySum += yDegree;
  }
   xDegree = xSum / 20;
   yDegree = ySum / 20;

  if(xDegree >= 0 && xDegree < 350){	//민감하게 반응하는 조의스틱의 값을 0~350 범위로 조정
    if(LeftRightWidth >= 0){LeftRightWidth--;}
    else if(LeftRightWidth == 0){}
  }
  else if(xDegree > 650 && xDegree < 1023){
    if(LeftRightWidth <= 180){LeftRightWidth++;}
    else if(LeftRightWidth == 180){}
  }
  LeftRightMotor.write(LeftRightWidth);   //계산된 각도 입력
  
  if(yDegree >= 0 && yDegree < 350){
    if(UpDownWidth <= 180){UpDownWidth++;}
    else if(UpDownWidth == 180){}
  }
  else if(yDegree > 650 && yDegree < 1023){
    if(UpDownWidth >= 130){UpDownWidth--;}
    else if(UpDownWidth == 130){}
  }
  UpDownMotor.write(UpDownWidth);
}

```

---

> **참고사항**

* Reference : 
[**https://www.arduino.cc/reference/en/libraries/servo/**](https://www.arduino.cc/reference/en/libraries/servo/) 
[**https://www.kocoafab.cc/make/view/520**](https://www.kocoafab.cc/make/view/520) 

* 펜틸트 거치대만으로는 스마트폰의 무게를 감당하기 힘들다. 그렇기에 지탱이 잘되는 거치대를 이용한다면 더 실용적인 스마트폰 거치대를 만들 수 있다.

*  서보모터의 최초 각도를 거치대에 맞게 설정해야 소스코드 상에서 각도를 계산하기 쉽다.