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
