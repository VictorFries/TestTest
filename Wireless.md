


#include <Servo.h>
#include<SoftwareSerial.h>
SoftwareSerial phone(10,11);
Servo index;
Servo middle;
Servo ring;
Servo pinkie;

const int flexIndexpin=A0;
const int flexMiddlepin=A1;
const int flexRingpin=A2;
const int flexPinkiepin=A3;
int currentState=0;
int lastState=0;
void setup() {
  
  phone.begin(9600);
  Serial.begin(9600);
  phone.println("First");
  index.attach(9);
  middle.attach(6);
  ring.attach(5);
  pinkie.attach(3);
  pinMode(flexIndexpin,INPUT);
  pinMode(flexMiddlepin,INPUT); 
  pinMode(flexRingpin,INPUT);
  pinMode(flexPinkiepin,INPUT);
  pinMode(8,INPUT);
  pinMode(9,OUTPUT);
  pinMode(6,OUTPUT);
  pinMode(5,OUTPUT);
  pinMode(3,OUTPUT);
  
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
  Serial.println("Bluetooth");
if(phone.available())
  {
   in=phone.read();
   //Serial.println(in);
   if(in=='1')
   {
    index.write(90);
    
   }
   else if(in=='2')
   {
    index.write(180);
   }
   else if(in=='3')
   {
    middle.write(90);
   }
   else if(in=='4')
   {
    middle.write(180);
   }
   else if(in=='5')
   {
    ring.write(90);
   }
   else if(in=='6')
   {
    ring.write(180);
   }
   else if(in=='7')
   {
    phone.println(90);
   }
   else if(in=='8')
   {
    pinkie.write(180);
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
  
  index.write(pullIndex);//turn the servos
  middle.write(pullMiddle);
  ring.write(pullRing);
  pinkie.write(pullPinkie);
  }
  }

  










