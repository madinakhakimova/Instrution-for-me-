# Arduino

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
    // Подключаем библиотеку
    #include <QuadDisplay.h>
     
    // Указываем номер цифрового выхода (9-й пин)
    #define DISPLAY_PIN 9
     
    void setup()
    {
    }
     
    void loop()
    {
      // выведем целое число
      displayInt(DISPLAY_PIN, 123);
      delay(1000);
     
      // теперь отрицательное
      displayInt(DISPLAY_PIN, -123);
      delay(1000);
     
      // можно показывать ведущие нули (0012)
      displayInt(DISPLAY_PIN, 12, true);
      delay(1000);
     
      // можно показывать вещественные числа
      // с заданной точностью, например 2 знака после запятой
      displayFloat(DISPLAY_PIN, -1.23, 2);
      delay(1000);
     
      // можно показывать температуру в °C
      displayTemperatureC(DISPLAY_PIN, -5);
      delay(1000);
     
      // можно показывать нехитрый текст (on/off, например) или
      // произвольную графику
      displayDigits(DISPLAY_PIN, QD_O, QD_f, QD_f, QD_NONE); // off
      delay(1000);
      displayDigits(DISPLAY_PIN, QD_O, QD_n, QD_NONE, QD_NONE); // on
      delay(1000);
     
      // в конце нужно очистить индикатор
      displayClear(DISPLAY_PIN);
      delay(1000);
    }

```
