// Computational-craft

#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
  #include <avr/power.h>
#endif

#define PIN            5
#define NUMPIXELS      8

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

int delayval = 500;
int points = 8;
int inPinOne = 6;
int inPinTwo = 7;
int inPinThree = 8;
int inPinFour = 9;

int old_one = 0;
int new_one = 0;
int old_two = 0;
int new_two = 0;
int old_three = 0;
int new_three = 0;
int old_four = 0;
int new_four = 0;

void setup() {
pinMode(inPinOne, OUTPUT); 

#if defined (__AVR_ATtiny85__)
  if (F_CPU == 16000000) clock_prescale_set(clock_div_1);
#endif
  pixels.begin(); 
  Serial.begin(9600);
}

void loop() {
  new_one = digitalRead(inPinOne);
  new_two = digitalRead(inPinTwo);
  new_three = digitalRead(inPinThree);
  new_four = digitalRead(inPinFour);
  
  if(new_one == 1 && old_one == 0){
    old_one = 1;
    points--;
    Serial.println("pin6");
  }
  
  if(old_one == 1 && new_one == 0){
    old_one = 0;
  }

  if(new_two == 1 && old_two == 0){
    old_two = 1;
    points--;
    Serial.println("pin7");
  }
  
  if(old_two == 1 && new_two == 0){
    old_two = 0;
  }

  if(new_three == 1 && old_three == 0){
    old_three = 1;
    points--;
    Serial.println("pin8");
  }
  
  if(old_three == 1 && new_three == 0){
    old_three = 0;
  }

  if(new_four == 1 && old_four == 0){
    old_four = 1;
    points--;
    Serial.println("pin9");
  }
  
  if(old_four == 1 && new_four == 0){
    old_four = 0;
  }

  Serial.println(points);
  
  for(int i=0;i<points;i++){
    //Serial.println(points);
    pixels.setPixelColor(i, pixels.Color(0,0,250)); 
    pixels.show(); 
  }
  for(int i=points;i<8;i++){
    pixels.setPixelColor(i, pixels.Color(250,0,0)); 
    pixels.show();
  }
  
}
