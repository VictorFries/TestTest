#include <SPI.h>
#include <RF24.h>
const int flexIndexpin=A0;
const int flexMiddlepin=A1;
const int flexRingpin=A2;
const int flexPinkiepin=A3;

RF24 transmit(8,10);

void setup() {
  Serial.begin(9600);
  pinMode(flexIndexpin,INPUT);
  pinMode(flexMiddlepin,INPUT); 
  pinMode(flexRingpin,INPUT);
  pinMode(flexPinkiepin,INPUT);
  Serial.println("setup");
   transmit.begin();
  byte address[]={"Node1"};
  transmit.openWritingPipe(address);
 
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
  lh
  flexIndex=analogRead(flexIndexpin);
  flexMiddle=analogRead(flexMiddlepin);
  flexRing=analogRead(flexRingpin);
  flexPinkie=analogRead(flexPinkiepin);
  
  pullIndex=map(flexIndex,200,300,0,90);
  pullIndex=constrain(pullIndex,0,90);
  
  pullMiddle=map(flexMiddle,200,300,0,90);
  pullMiddle=constrain(pullMiddle,0,90);
  
  pullRing=map(flexRing,200,300,0,90);
  pullRing=constrain(pullRing,0,90);

  pullPinkie=map(flexPinkie,200,300,0,90);
  pullPinkie=constrain(pullPinkie,0,90);
  
  int r[]={pullIndex,pullMiddle,pullRing,pullPinkie};
  
  //Serial.println(c);
  transmit.write(&r,sizeof(r));
  
  }

