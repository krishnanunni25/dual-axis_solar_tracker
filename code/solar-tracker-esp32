#include <ESP32Servo.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(25, 26, 27, 17, 16, 4);

const int servoPin1 = 19;
const int servoPin2 = 18;
const int ldr1 = 32;
const int ldr2 = 33;
const int ldr3 = 34;
const int ldr4 = 35;
const int voltageSensor = 13;
const int led1 = 2;
const int button = 23;

int ldrValue1;
int ldrValue2;
int ldrValue3;
int ldrValue4;
float voltageValue;
float currentValue;
int power;
int diff1;
int diff2;
bool ledState = false;

int angle1 = 90;
int angle2 = 90;
int cutoff1 = 100;
int cutoff2 = 150;
bool prev_button = false;
unsigned long previousMillis = 0;
int axis_1 = 0;

Servo servo1;
Servo servo2;

void setup() {
  pinMode(ldr1, INPUT);
  pinMode(ldr2, INPUT);
  pinMode(ldr3, INPUT);
  pinMode(ldr4, INPUT);
  pinMode(voltageSensor, INPUT);
  pinMode(led1, OUTPUT);
  pinMode(button, INPUT_PULLUP);

  Serial.begin(115200);
  servo1.attach(servoPin1,500,2400);
  servo2.attach(servoPin2,500,2400);
  
  servo1.write(angle1);
  servo2.write(angle2);

  lcd.begin(16, 2);
  lcd.print("Solar ready");

  delay(1000);
  Serial.println("Initialization Successfull");
  lcd.clear();
}

void loop() {
  unsigned long currentMillis = millis();

  ldrValue1 = analogRead(ldr1);
  ldrValue2 = analogRead(ldr2);
  ldrValue3 = analogRead(ldr3);
  ldrValue4 = analogRead(ldr4);

  bool buttonVal = !digitalRead(button);
  delay(100);
  if (buttonVal && !prev_button) {  
    if(axis_1<2){
      axis_1 = axis_1 + 1;
    }
    else{
      axis_1 = 0;
    }
  }
  prev_button = buttonVal;

  diff1 = ldrValue2-ldrValue1;
  diff2 = ldrValue4-ldrValue3;
  if(angle1>90){
    diff2=-diff2;
  }

  if (axis_1 == 2){
    if (diff1>cutoff1){
      if (angle1<150){
        angle1 = angle1 + 5;
      }
    }
    else if (diff1<(-1*cutoff1)){
      if (angle1>30){
          angle1 = angle1 - 5;
      }
    }

    if (diff2>cutoff2){
      if (angle2<150){
        angle2 = angle2 + 5;
      }
    }
    else if (diff2<(-1*cutoff2)){
      if (angle2>30){
        angle2 = angle2 - 5;
      }
    }

    servo1.write(angle1);
    servo2.write(angle2);
    ledState = HIGH;
    digitalWrite(led1, ledState);
  }
  else{
    digitalWrite(led1, LOW);
  }


  if (axis_1 == 1){
    if (diff1>cutoff1){
      if (angle1<150){
        angle1 = angle1 + 5;
      }
    }
    else if (diff1<(-1*cutoff1)){
      if (angle1>30){
          angle1 = angle1 - 5;
      }
    }

    servo1.write(angle1);
    if (currentMillis - previousMillis >= 500) {
    previousMillis = currentMillis;
    ledState = !ledState;
    digitalWrite(led1, ledState);
    }
  }
  else{
    digitalWrite(led1, LOW);
  }


  voltageValue = analogRead(voltageSensor);
  voltageValue = voltageValue/540;

  Serial.print("Voltage: ");
  Serial.println(voltageValue);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Voltage: ");
  lcd.print(voltageValue);
  lcd.setCursor(0, 1);
  lcd.print("Mode: ");
  lcd.print(axis_1);
  lcd.print(" axis");
  Serial.print("Differences: ");
  Serial.print(diff1);
  Serial.print(", ");
  Serial.println(diff2);

  delay(200);
}
