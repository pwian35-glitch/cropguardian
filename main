#include <Wire.h>
#include <Adafruit_GFX.h>
#include <Adafruit_SSD1306.h>

// OLED Display Size
#define SCREEN_WIDTH 128
#define SCREEN_HEIGHT 64

// OLED Object
Adafruit_SSD1306 display(SCREEN_WIDTH, SCREEN_HEIGHT, &Wire, -1);

// Sensor Pins
int soilPin = A0;
int rainPin = A1;
int irPin = 7;

// Output Pins
int greenLED = 5;
int redLED = 6;
int buzzer = 8;
int pump = 9;

void setup() {

  // Serial Monitor Start
  Serial.begin(9600);

  // Output Pins
  pinMode(greenLED, OUTPUT);
  pinMode(redLED, OUTPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(pump, OUTPUT);

  // Input Pin
  pinMode(irPin, INPUT);

  // OLED Start
  if(!display.begin(SSD1306_SWITCHCAPVCC, 0x3C)) {
    Serial.println("OLED not found");
    while(1);
  }

  // OLED Settings
  display.clearDisplay();
  display.setTextSize(1);
  display.setTextColor(WHITE);

  // Welcome Screen
  display.setCursor(15,20);
  display.println("SMART PLANT");

  display.setCursor(18,35);
  display.println("MONITORING");

  display.display();

  delay(2000);
}

void loop() {

  // Read Sensor Values
  int soilValue = analogRead(soilPin);
  int rainValue = analogRead(rainPin);
  int irValue = digitalRead(irPin);

  // Show in Serial Monitor
  Serial.print("Soil: ");
  Serial.println(soilValue);

  Serial.print("Rain: ");
  Serial.println(rainValue);

  Serial.print("IR: ");
  Serial.println(irValue);

  // Soil Dry Condition
  if (soilValue > 600) {

    // Red LED ON
    digitalWrite(redLED, HIGH);

    // Green LED OFF
    digitalWrite(greenLED, LOW);

    // Pump ON
    digitalWrite(pump, HIGH);

    // Buzzer ON
    digitalWrite(buzzer, HIGH);

  }
  else {

    // Red LED OFF
    digitalWrite(redLED, LOW);

    // Green LED ON
    digitalWrite(greenLED, HIGH);

    // Pump OFF
    digitalWrite(pump, LOW);

    // Buzzer OFF
    digitalWrite(buzzer, LOW);
  }

  // OLED Display
  display.clearDisplay();

  display.setCursor(0,0);
  display.println("SMART PLANT");

  // Soil Value
  display.setCursor(0,15);
  display.print("Soil: ");
  display.println(soilValue);

  // Rain Value
  display.setCursor(0,28);
  display.print("Rain: ");
  display.println(rainValue);

  // IR Sensor
  display.setCursor(0,41);
  display.print("IR: ");

  if(irValue == 0) {
    display.println("OBJECT");
  }
  else {
    display.println("CLEAR");
  }

  // Pump Status
  display.setCursor(0,54);

  if(soilValue > 600) {
    display.println("PUMP ON");
  }
  else {
    display.println("PUMP OFF");
  }

  // Update OLED
  display.display();

  delay(1000);
}
