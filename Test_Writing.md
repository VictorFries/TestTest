#include <SPI.h>
#include <RF24.h>
const int flexIndexpin=A0;
const int flexMiddlepin=A1;
const int flexRingpin=A2;
const int flexPinkiepin=A3;
RF24 transmit(4,5);

void setup() {
  
  pinMode(flexIndexpin,INPUT);
  pinMode(flexMiddlepin,INPUT); 
  pinMode(flexRingpin,INPUT);
  pinMode(flexPinkiepin,INPUT);
  
  byte address[][6]={"Node1"};
  transmit.openWritingPipe(address[0]);
  transmit.begin();
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
  
  int r[]={pullIndex,pullMiddle,pullRing,pullPinkie};
  transmit.write(&r,sizeof(r));
  
  }

