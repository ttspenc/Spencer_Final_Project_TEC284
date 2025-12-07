# Spencer_Final_Project_TEC284

#include <Wire.h>
#include <U8g2lib.h>

// constructor for Grove Beginner Kit OLED (SSD1312)
U8G2_SSD1316_128X32_F_HW_I2C u8g2(U8G2_R0, U8X8_PIN_NONE);

// use d2
const int buttonPin = 2;
// 8 ball replay pool
const char* answers[] = 
{
  "Yep Yep Yep", "Noooo", "Ask again sorry", "For Sureeee",
  "uh not sure", "Probably idk", "Never bro", "It depends *shrug*"
};

int numAnswers = sizeof(answers) / sizeof(answers[0]);

// setup
void setup() 
{
  pinMode(buttonPin, INPUT);
  randomSeed(analogRead(0));
  u8g2.begin();

  u8g2.setFlipMode(0);

  u8g2.clearBuffer();
  u8g2.setFont(u8g2_font_ncenB08_tr);
  u8g2.drawStr(0, 15, "Magic 8 Ball, ask at your own risk...");
  u8g2.sendBuffer();
}
// loop
void loop() {
  // if button is pressed, thinking screen comes up
  if (digitalRead(buttonPin) == HIGH) 
  {
    u8g2.clearBuffer();
    // sets font 
    u8g2.setFont(u8g2_font_ncenB08_tr);
    u8g2.drawStr(0, 15, "Thinking...");
    u8g2.sendBuffer();
    // add delay
    delay(1000);
// looks at the random number index
    int index = random(numAnswers);
// displays answer 
    u8g2.clearBuffer();
    u8g2.setFont(u8g2_font_ncenB08_tr);
    u8g2.drawStr(0, 15, "Answer:");
    u8g2.drawStr(0, 35, answers[index]);
    u8g2.sendBuffer();
// delay
    delay(500);
  }
}
