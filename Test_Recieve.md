#include <SPI.h>
#include <RF24.h>
#include <Servo.h>
#include <SoftwareSerial.h>

Servo index;
Servo middle;
Servo ring;
Servo pinkie;
SoftwareSerial phone(10,11);
RF24 receive(A0,A1);
int currentState=0;
int lastState=0;

void setup() {
index.attach(9);  
middle.attach(6);
ring.attach(5);
pinkie.attach(3);
pinMode(8,INPUT);
 byte address[][6]={"Node1"};
 receive.openReadingPipe(1,address[0]);
 receive.startListening();
}
int arr[]={};
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
  if(x%2==0)
  {
  if(receive.available())
  {
    while(receive.available())
    {
      receive.read(&arr,sizeof(arr));
    }
  }
  index.write(arr[0]);
  middle.write(arr[1]);
  ring.write(arr[2]);
  pinkie.write(arr[3]);
  }
  if(x%2==1)
  {
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



















  
}
