#include <Wire.h>
#include "RTClib.h"
#include <Servo.h>
#include <LiquidCrystal.h>

RTC_DS1307 rtc;

LiquidCrystal lcd(8, 10, 7, 6, 5, 4);

Servo myservo;
int pos = 60;
int volumen;
int tiempo;
int pot = A0;
int pot2 = A1;

DateTime now;
byte hour, minute;
String h, m;

int feedHour = 7;
int feedMin = 0;
boolean foodTime = true;

void setup() {
now = rtc.now();
printTime(now);

if ((feedHour == now.hour()) && (feedMin == now.minute()) && foodTime){
feed();
}

if (feedMin != mow.minute()) {
foodTime = true;
}
}

void feed() {
lcd.clear();
lcd.setCursor(0, 0);
lcd.print("Sirviendo Comida");


myservo.attach(9);
volumen = analogRead(pot/5);
tiempo = analogRead(pot/8);

for (pos = 60; pos <= volumen; pos += 1) {
myservo.write(pos);
delay(tiempo);
}
delay(1000);

for (pos = volumen; pos >= 60; pos -= 1) {
myservo.write(pos);
delay(tiempo);
}
delay(3000);
myservo.detach();
foodTime = false;
}

void printTime(DetaTime t) {
lcd.setCursor(0, 0);
lcd.print("H. actual: ");
hour = t.hour();
if(hour < 10) {
h ="0" + String(hour);
} else {

h = String(hour);
}
lcd.print(h);
lcd.print(':');
minute = t.minute();
if (minute < 10) {
m = "0" + String(minute);
} else {
m = String(minute);
}
lcd.print(m);

lcd.setCursor(0, 1);
lcd.print("H. comida: ");
if (feedHour < 10) {
h = "0" + String(feedHour);
} else {
h = String(feedHour);
}
lcd.print(h);
lcd,print(':');
if (feedMin < 10) {
m = "0" + String(feedMin);
} else {
 m = String(feedMin);
}

lcd.print(m);

return;

}
