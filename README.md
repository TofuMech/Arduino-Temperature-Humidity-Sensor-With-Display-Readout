This is serving as the code I use for a temperature sensor project with Arduino



#include "DHT.h"
#include <LiquidCrystal.h>

// This is the pin connection from pin five of the Uno to the third pin on the DHT module
#define DHTPIN 5

// Data pins on the ardunio connected to the LCD display
LiquidCrystal lcd(7, 8, 9, 10, 11, 12);

// Type of DHT sensor.
#define DHTTYPE DHT11

// Initialize DHT sensor.
DHT dht(DHTPIN, DHTTYPE);

void setup() {

  
  Serial.begin(9600);
  // Uncomment this code to view in the monitor window Serial.println("Humidity and Temperature");

  // Start the sensor.
  dht.begin();


  //setup for lcd 
  lcd.begin(16, 2);

  
}

void loop() {

  // Counted in miliseconds, this will return the value given by the DHT module every two seconds
  delay(2000);

  // Reads humidity.
  float h = dht.readHumidity();

  // Temperature readings, defaulting in celsius
  float t = dht.readTemperature();
  
  // Celsius to Farhenheit conversion formula
  float f = ((t * 9) / 5 +32);

  Serial.print("Humidity: ");
  Serial.print(h);
  Serial.print("%  Temperature: ");

  //To change to celcius, change the variable instead of f, to t
  Serial.print(f);



  //In order to the make the display provide both lines at the same time, set the cursor to 0, 0 for the first line
  // and 0, 1 for the second.

  lcd.setCursor(0, 0);

  //Same as aboive. To change to celcius, change the variable instead of f, to t

  lcd.print(String("Temp: ") + String(f));

  lcd.setCursor(0, 1);

  lcd.print(String("Humidity: ") + String(h));

  lcd.noCursor();
  Serial.println(" F");



}
