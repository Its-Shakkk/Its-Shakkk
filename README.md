- 👋 Hi, I’m @Its-Shakkk
#include<LiquidCrystal_I2C.h>
#define triggerPIN 3
#define echoPIN 4

LiquidCrystal_I2C lcd(0x27,20,4);
long duration;
int distance, meter, cmeter;

void setup() {
  pinMode(triggerPIN, OUTPUT);
  pinMode(echoPIN, INPUT);
  lcd.init();
  lcd.backlight();
   Serial.begin(9600); // // Serial Communication is starting with 9600 of baudrate speed
  Serial.println("Ultrasonic Sensor HC-SR04 Test"); // print some text in Serial Monitor
  Serial.println("with Arduino Nano");
}

void loop() {
  digitalWrite(triggerPIN, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPIN, LOW);
  duration = pulseIn(echoPIN, HIGH);
  distance = duration * 0.034 / 2;
  meter = distance / 100;
  cmeter = distance - (meter * 100);
   Serial.print("Distance: ");
  Serial.print(distance);
  Serial.println(" cm");
  lcd.clear();
  lcd.setCursor(11, 0);
  lcd.print(meter);
  lcd.setCursor(0, 0);
  lcd.print("Distance:");
   lcd.setCursor(15, 0);
  lcd.print("M");
  lcd.setCursor(11, 1);
  lcd.print(cmeter);
  lcd.setCursor(0, 1);
  lcd.print("Distance:");
  lcd.setCursor(14, 1);
  lcd.print("CM");
}
