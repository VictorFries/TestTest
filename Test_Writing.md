#include <nRF24L01.h>
#include <printf.h>
#include <RF24.h>
#include <RF24_config.h>

void setup() {
  RF24 transmit(6,7);
  byte address[][6]={"Node1"};
  transmit.openWritingPipe(address[0]);
  transmit.begin();
}

void loop() {
  
  transmit.write();

}
