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

```
**Новый свет светодиода**
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
**Светодиод горит если температура ниже или ровно на 20 С**
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

**Показывает на экране "YOO" или "OFF"**
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
**Позазывает на экране "YOO" если температура ниже или ровно на 25 С или иначе**
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
**Управление с джойстиком**
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
```
**Draw square**
```c++
#include <IRremote.hpp>

#define IR_RECEIVE_PIN 0
#define IR_BUTTON_PLUS 21
#define IR_BUTTON_MINUS 7
#define IR_BUTTON_CH_PLUS 71
#define IR_BUTTON_CH_MINUS 69
#define IR_BUTTON_PLAY_PAUSE 67

#define SPEED_1      5 
#define DIR_1        4
 
#define SPEED_2      6
#define DIR_2        7

void setup(){
  Serial.begin(9600);
  IrReceiver.begin(IR_RECEIVE_PIN);

  for (int i = 4; i < 8; i++) {     
    pinMode(i, OUTPUT);
  }
}

void loop(){
   if (IrReceiver.decode()) {
      IrReceiver.resume(); // Enable receiving of the next value
      int command = IrReceiver.decodedIRData.command;
      
      switch (command) {
        case IR_BUTTON_PLUS: {

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_MINUS: {
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_CH_PLUS: { // stop mototrs
          digitalWrite(DIR_1, HIGH); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          break;
        }
        case IR_BUTTON_CH_MINUS: { 

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed
                                                         
          delay (600);
          
          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay (800);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay (600);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay (800);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay (600);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, LOW); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay (800);

          digitalWrite(DIR_1, LOW); // set direction
          analogWrite(SPEED_1, 255); // set speed

          digitalWrite(DIR_2, HIGH); // set direction
          analogWrite(SPEED_2, 255); // set speed

          delay (600);



          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);

          break;
        }
          case IR_BUTTON_PLAY_PAUSE: {
            
          analogWrite(SPEED_1, 0); 
          analogWrite(SPEED_2, 0);

          break;
        }
      }
  }
}
```
