#include <SPI.h>
#include <RF24.h>
#include <Servo.h>
#include <SoftwareSerial.h>

Servo index;
Servo middle;
Servo ring;
Servo pinkie;
int i=A0;
int out=A1;
SoftwareSerial phone(i,out);
RF24 receive(3,4);
int currentState=0;
int lastState=0;
byte address[]=("Node1");

void setup() {
Serial.begin(9600);
phone.begin(9600);
receive.begin();
receive.openReadingPipe(0,address);
receive.startListening();
Serial.println("Listening");
pinMode(8,INPUT);
pinMode(i,INPUT);
pinMode(out,OUTPUT);
index.attach(10);  
middle.attach(7);
ring.attach(6);
pinkie.attach(5);



}
int arr[4]={};
char in;
int x=0;
void loop() {
  lastState=0;
  currentState=digitalRead(8);
  if(lastState!=currentState)
  {
  x=x+1;
  }
  Serial.println(x);
  delay(100);
  if(x%2==0)
  {
    if(receive.available())
    {
    Serial.println("Data Recieved");
    
    receive.read(&arr,sizeof(arr));
    int a=arr[0];
    int b=arr[1];
    int c=arr[2];
    int d=arr[3];
    /*Serial.println(a);
    Serial.println(b);
    Serial.println(c);
    Serial.println(d);*/
    index.write(b);
  middle.write(c);
  ring.write(a);
  pinkie.write(d);
  }
  else if(!receive.available())
  {
    Serial.println("Failed");
  }
  
  }
  if(x%2==1)
  {
    Serial.println("Bluetooth");
    if(phone.available())
  {
   in=phone.read();
   Serial.println(in);
   if(in=='1')
   {
    index.write(45);
    phone.println("Works");
   }
   else if(in=='2')
   {
    index.write(90);
   }
   else if(in=='3')
   {
    middle.write(45);
   }
   else if(in=='4')
   {
    middle.write(90);
   }
   else if(in=='5')
   {
    ring.write(45);
   }
   else if(in=='6')
   {
    ring.write(90);
   }
   else if(in=='7')
   {
    phone.println(45);
   }
   else if(in=='8')
   {
    pinkie.write(90);
   }
   }
  }

}



