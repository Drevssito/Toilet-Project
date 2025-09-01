# Toilet-Project

#include <Servo.h>

Servo myservo;

long duration;
int distance;

const int trigPin = 13;
const int echoPin = 12;

int ServoPosition = 90;

void setup() {
  // put your setup code here, to run once:
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.begin(115200);

  // Servo
  myservo.attach(9);

}

void loop() {
  // put your main code here, to run repeatedly:
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);

  distance = float(duration * 0.0343) / 2;

  // Funcionalidad del Servo
  if (distance > 5) {
    myservo.write(ServoPosition);
    Serial.println("Polea en reposo");

  }
  else {
    for (ServoPosition = 90; ServoPosition >= 0; ServoPosition -= 1) {
      myservo.write(ServoPosition);
      Serial.println("Polea subiendo");
      delay(15);
    }
    for (ServoPosition = 0; ServoPosition <= 90; ServoPosition += 1) {
      myservo.write(ServoPosition);
      Serial.println("Polea bajando");
      delay(15);
    }

  }

}
