#include <Key.h>
#include <Keypad.h>
#include <SoftwareSerial.h>

#include <LiquidCrystal.h>
const char predefinedPassword[4] = "*911";
const int passwordLength = 4;
int inputLength = 5;

char val[5];

char inputPassword[passwordLength + 1];
int inputCount = 0 ; //Counter for input from keypad

const byte ROWS = 4 ; //Number of rows on keypad
const byte COLS = 3 ; //Number of columns on keypad 

char keys[ROWS][COLS] = {
  {'1','2','3'},
  {'4','5','6'},
  {'7','8','9'},
  {'*','0','#'}
};

byte rowPins[ROWS] = {2,3,4,5}; // ROWS PINS ON ARDUINO
byte colPins [COLS] = {6,7,8}; // COLUMN PINS ON ARDUINO

Keypad keypad = Keypad(makeKeymap(keys), rowPins , colPins , ROWS , COLS );
LiquidCrystal lcd(A5,13,A3,A1,A4,A2); // RS,E,D4,D5,D6,D7
SoftwareSerial bt(12,11); //12 for RX and 11 for TX

void setup(){
  char key = keypad.getKey();

  if(bt.available()>0)
  {
    bt.readBytesUntil('\0', inputPassword , 4);
    val[4]='\0';
    checkPass();
/*
  if (strcmp(val.predefinedPassword)==0)
  {
    lcd.clear();
    lcd.print("Access Granted");
    Serial.println(val);
  }
  else
  {
    Serial.print("Hi");
    lcd.clear();
    Serial.print(val);
    lcd.print("Acess Denied");
    Serial.println(inputPassword);
    delay(2000);
    lcd.clear();
    lcd.print("Enter Password : ");
  }*/
  }
  if (key){
    lcd.setCursor(inputCount,1);
    lcd.print("*");
    //stor the key press in the inputPassword array
    if (inputCount < passwordLength){
      inputPassword[inputCount] = key;
      inputCount++ ;
      //lcd.print(key);
    }
    if (inputCount == passwordLength){
      inputPassword[inputLength] = '\0';
      checkPass();
      inputCount = 0;
    }
  }
}

void checkPass()
{
  if(strcmp(inputPassword , predefinedPassword)==0){
    lcd.clear();
    lcd.print("Acess Granted");
    digitalWrite(10,0);
    Serial.println(inputPassword);
  }
  else{
    lcd.clear();
    lcd.print("Access Denied");
    Serial.println(inputPassword);
  }

  delay(4000);
  lcd.clear();
  lcd.print("Enter Password : ");
  digitalWrite(10,1);
}
