#include <nRF24L01.h>

#include <RF24.h>

#include<SoftwareSerial.h>

SoftwareSerial phone(10,11);

const int flexIndexpin=A0;
const int flexMiddlepin=A1;
const int flexRingpin=A2;
const int flexPinkiepin=A3;
int currentState=0;
int lastState=0;
RF24 transmit(4,5);

void setup() {
  phone.begin(9600);
  pinMode(flexIndexpin,INPUT);
  pinMode(flexMiddlepin,INPUT); 
  pinMode(flexRingpin,INPUT);
  pinMode(flexPinkiepin,INPUT);
  
  byte address[][6]={"Node1"};
  transmit.openWritingPipe(address[0]);
  transmit.begin();
}

char in;
int x=1;
void loop() {
lastState=0;
currentState=digitalRead(8);
if(lastState!=currentState)
{
  x=x+1;
}
delay(100);
Serial.println(lastState);
Serial.println(currentState);
Serial.println(x);
if(x%2==0)
{ 
  int z=0;
  Serial.println("Bluetooth");
if(phone.available())
  {
    
   in=phone.read();
   //Serial.println(in);
   if(in=='1')
   {
    z=1;
    transmit.write(z,sizeof(z));
    
   }
   else if(in=='2')
   {
    z=2;
    transmit.write(z,sizeof(z));
   }
   else if(in=='3')
   {
    z=3;
    transmit.write(z,sizeof(z));
   }
   else if(in=='4')
   {
    z=4;
    transmit.write(z,sizeof(z));
   }
   else if(in=='5')
   {
    z=5;
    transmit.write(z,sizeof(z));
   }
   else if(in=='6')
   {
    z=6;
    transmit.write(z,sizeof(z));
   }
   else if(in=='7')
   {
    z=7;
    transmit.write(z,sizeof(z));
   }
   else if(in=='8')
   {
    z=8;
    transmit.write(z,sizeof(z));
   }
  }
}
   if(x%2==1)
  {
  Serial.println("Glove");
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
  transmit.write(r,sizeof(r));
  }
  }
