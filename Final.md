#include <Servo.h>
Servo index;
Servo middle;
Servo ring;
Servo pinkie;

const int flexIndexpin=A0;
const int flexMiddlepin=A1;
const int flexRingpin=A2;
const int flexPinkiepin=A3;


void setup() {
  //Serial.begin(9600); 
  index.attach(9);
  middle.attach(6);
  ring.attach(5);
  pinkie.attach(3);
  pinMode(flexIndexpin,INPUT);
  pinMode(flexMiddlepin,INPUT); 
  pinMode(flexRingpin,INPUT);
  pinMode(flexPinkiepin,INPUT);

  pinMode(9,OUTPUT);
  pinMode(6,OUTPUT);
  pinMode(5,OUTPUT);
  pinMode(3,OUTPUT);
  
}

void loop() {
  
  int flexIndex;//reads the postion of the flex sensors
  int flexMiddle;
  int flexRing;
  int flexPinkie;
  int pullIndex; //tells the servos to move
  int pullMiddle;
  int pullRing;
  int pullPinkie;
  
  flexIndex=analogRead(flexIndexpin);
  flexMiddle=analogRead(flexMiddlepin);
  flexRing=analogRead(flexRingpin);
  flexPinkie=analogRead(flexPinkiepin);
  
  pullIndex=map(flexIndex,200,300,0,180);
  pullIndex=constrain(pullIndex,0,180);
  
  pullMiddle=map(flexMiddle,200,300,0,180);
  pullMiddle=constrain(pullMiddle,0,180);
  
  pullRing=map(flexRing,200,300,0,180);
  pullRing=constrain(pullRing,0,180);

  pullPinkie=map(flexPinkie,200,300,0,180);
  pullPinkie=constrain(pullPinkie,0,180);
  
  index.write(pullIndex);//turn the servos
  middle.write(pullMiddle);
  ring.write(pullRing);
  pinkie.write(pullPinkie);

 
}
  
