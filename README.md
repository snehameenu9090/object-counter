# object-counter
i have made the object counter hardware project with arduino code i have made that project with the hardware components like  arduino uno,lcd display,module,male cable and then i do soldering in that projects which helps to give the exact answer.
then by uploading the code to the arduino then if we pass any object near it then it senses and counts the objects that passes near it

 #include <Wire.h> 
#include <LiquidCrystal_I2C.h>

// LCD ka address check karein (0x27 zyadatar sahi hota hai)
LiquidCrystal_I2C lcd(0x27, 16, 2); 

const int IR_PIN = 2; // IR Sensor Pin
int count = 0;
int lastState = HIGH;

void setup() {
  pinMode(IR_PIN, INPUT);
  
  lcd.init();          // LCD initialize karein
  lcd.backlight();     // LCD ki light on karein
  
  lcd.setCursor(0, 0);
  lcd.print("Counter Ready!");
  delay(2000);
  lcd.clear();
  
  // Starting display
  lcd.setCursor(0, 0);
  lcd.print("Count: 0");
}

void loop() {
  int currentState = digitalRead(IR_PIN);

  // Jab sensor ke aage kuch aaye (LOW trigger)
  if (currentState == LOW && lastState == HIGH) {
    count++;
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("Object Detected");
    lcd.setCursor(0, 1);
    lcd.print("Total Count: ");
    lcd.print(count);
    
    delay(500); // Taki ek baar mein 10 baar na gin le (Debounce)
  }
  
  lastState = currentState;
}
