#include <Servo.h>

int dist = 0;

long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
 
  return pulseIn(echoPin, HIGH);
}

Servo servo_8;

void setup()
{
  servo_8.attach(8, 500, 2500);
  pinMode(2, INPUT);
  pinMode(12, OUTPUT);
  pinMode(A0, INPUT);
  pinMode(9, OUTPUT);
}

void loop()
{
  dist = 0.01723 * readUltrasonicDistance(7, 7);
  if (dist <= 100) {
    servo_8.write(90);
    delay(1000); 
  } else {
    servo_8.write(0);
    delay(1000); 
  }
  if (digitalRead(2) == 1) {
    digitalWrite(12, HIGH);
    delay(1000); 
  } else {
    digitalWrite(12, LOW);
    delay(1000); 
  }
  if (analogRead(A0) > 200) {
    digitalWrite(9, HIGH);
    delay(1000);
  } else {
    digitalWrite(9, LOW);
    delay(1000); 
  }
}