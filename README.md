# Obstacle-Avoiding-Robot
Obstacle Avoiding Robot is an Arduino-based autonomous robot that uses an ultrasonic sensor (HC-SR04) to detect obstacles in its path and automatically avoid collisions. The car continuously measures distance in front of it and decides whether to move forward or turn to avoid hitting objects.
Introduction:Obstacle Avoiding Robot is an Arduino-based autonomous robot that uses an ultrasonic sensor (HC-SR04) to detect obstacles in its path and automatically avoid collisions.
The robot continuously measures distance in front of it and decides whether to move forward or turn to avoid hitting objects.

Features:
-Detects obstacles using an ultrasonic sensor
-Moves forward when the path is clear
-Stops and turns automatically when an obstacle is detected
-Simple logic with Arduino UNO + DC motors

The problem I faced was:False or unstable distance readingS(A common problem faced while useing ultrasonic sensor)
How I fixed it : Add a short delay (10–20 ms) between distance checks.
 Cicuit diagram:<img width="882" height="637" alt="Screenshot 2025-08-19 173323" src="https://github.com/user-attachments/assets/d5a26397-928e-4054-83e6-a9abfc219189" />

 Code:
int trig = 12;
int echo = 8;
int m1 = 13;
int m2 = 3;

long duration;
float distance;

void setup()
{
  pinMode(m1, OUTPUT);
  pinMode(m2, OUTPUT);
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);
  Serial.begin(9600);
 
}

void loop()
{
  
  digitalWrite(trig ,LOW);
  delayMicroseconds(2);
  digitalWrite(trig ,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig ,LOW);
  
  duration = pulseIn(echo,HIGH);
  distance = duration * 0.034 / 2;

  Serial.println(distance);
  
  if(distance > 15){
   moveforward();
  }else{
    stop();
    turnright();
  }
}

void stop()
  {
   digitalWrite(m1,LOW);
    digitalWrite(m2,LOW);
  }

 void moveforward()
  {
    digitalWrite(m1,HIGH);
    digitalWrite(m2,HIGH);
  }

void turnright()
  {
    digitalWrite(m1,HIGH);
    digitalWrite(m2,LOW);
  }
