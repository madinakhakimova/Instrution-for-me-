# Arduino

**Подключения 3 светодиода**
```c++
const int led1 = 2;
const int led2 = 4;
const int led3 = 7;

bool btnState = false ;
void setup()
{
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
}

void loop()
{
  if(btnState)
  digitalWrite(led1, 1);
  
  digitalWrite(led1, 0);
  
  digitalWrite(led2, 1);
  digitalWrite(led2, 0);
  
  digitalWrite(led3, 1);
  digitalWrite(led3, 0);
}
![IMG](photo_2023-11-18_10-50-13.jpg) 

```
**Новый цвет светодиода**
```C++
#include <RGBLed.h>

#define RED_PIN 9
#define GREEN_PIN 10
#define BLUE_PIN 11

RGBLed led(RED_PIN, GREEN_PIN, BLUE_PIN, RGBLed::COMMON_ANODE);


void setup() {
  pinMode(RED_PIN, OUTPUT);
  pinMode(GREEN_PIN, OUTPUT);
  pinMode(BLUE_PIN, OUTPUT);

}

void loop() {
  led.setColor(255, 216, );
}
```
**Работа термоме
```C++
#include <TroykaThermometer.h>
const int led = 3;
 
TroykaThermometer thermometer(A0);
  
void setup()
{
  pinMode(led, OUTPUT);
  Serial.begin(9600);
}
 
void loop()
{
 
  thermometer.read();
  int temperature = thermometer.getTemperatureC();
 
  Serial.print("Temperature is ");
  Serial.print(temperature);
  Serial.println(" C");
   if(temperature >= 20) {
    digitalWrite(led, HIGH);
   }
   else {
    digitalWrite(led, LOW);
   }
}
```

```C++
           #include <QuadDisplay2.h>
#include <TroykaThermometer.h>


TroykaThermometer thermometer(A0);

// создаём объект класса QuadDisplay и передаём номер пина CS
QuadDisplay qd(9);
  
void setup()
{
  qd.begin();
}
  
void loop()
{  // можно выводить целые числа
  thermometer.read();
  int temperature = thermometer.getTemperatureC();

  
  // можно показывать температуру в °C
  qd.displayTemperatureC(temperature);
  delay(1000);
  
  // qd.displayDigits(QD_O, QD_f, QD_f, QD_NONE); // off
  // delay(1000);
  // qd.displayDigits(QD_O, QD_n, QD_NONE, QD_NONE); // on
  // delay(1000);
  
}


```
```C++
#include <QuadDisplay2.h>     
#include <TroykaThermometer.h>


TroykaThermometer thermometer(A5);

QuadDisplay qd(9);
constexpr auto pinSensor = A0;

void setup() {
  Serial.begin(9600);
  qd.begin();
  
}
  
void loop() {
  thermometer.read();
  int temperature = thermometer.getTemperatureC();

  int valueSensor = analogRead(pinSensor);
  Serial.println(temperature);

  qd.displayTemperatureC(temperature);
  if (temperature >= 25 && valueSensor >=250) {
    qd.displayDigits(QD_Y, QD_O, QD_O, QD_NONE);
  }
  else{
    qd.displayDigits(QD_O, QD_f, QD_f, QD_NONE);
  }
}
  
```

```C++
#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7
 
void setup() {
  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
} 
 
void loop() {
 
  digitalWrite(DIR_1, LOW);
  analogWrite(SPEED_1, 255);

}
```
**С джой**
```C++
#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

#define uy A0


void setup(){
  Serial.begin(9600);
  pinMode (uy, INPUT);
  
  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
  Serial.println(analogRead(uy));
  delay(200);
  int command = analogRead(uy);

  if (command < 200) {
       
    digitalWrite(DIR_1, LOW); // set direction
   analogWrite(SPEED_1, 255); // set speed
  }
  else if (command > 200 && command < 600){
  digitalWrite(DIR_1, HIGH); // set direction
   analogWrite(SPEED_1, 255);

  }
    else if (command > 600){
  digitalWrite(DIR_1, HIGH); // set direction
   analogWrite(SPEED_1, 0);

  }      

}


 

          

