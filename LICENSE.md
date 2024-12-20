material required:- 
male female connectors
ptc heater 
spdt relay
Arduino uno




code:-
#include <Wire.h>

// Pin definitions
const int heatPin = 9; // Pin for heating element
const int vibrationPin = 10; // Pin for vibration motor
const int buttonHeat = 2; // Button to toggle heat settings
const int buttonVibration = 3; // Button to toggle vibration modes

// Variables
int heatLevel = 0; // Heat level: 0 = off, 1 = low, 2 = medium, 3 = high
int vibrationMode = 0; // Vibration mode: 0 = off, 1 = low, 2 = medium, 3 = high

void setup() {
  pinMode(heatPin, OUTPUT);
  pinMode(vibrationPin, OUTPUT);
  pinMode(buttonHeat, INPUT_PULLUP);
  pinMode(buttonVibration, INPUT_PULLUP);
}

void loop() {
  // Heat control
  if (digitalRead(buttonHeat) == LOW) {
    delay(200); // Debounce
    heatLevel = (heatLevel + 1) % 4; // Cycle through 0-3
  }

  // Adjust heating element based on heatLevel
  switch (heatLevel) {
    case 0:
      analogWrite(heatPin, 0); // Off
      break;
    case 1:
      analogWrite(heatPin, 85); // Low heat
      break;
    case 2:
      analogWrite(heatPin, 170); // Medium heat
      break;
    case 3:
      analogWrite(heatPin, 255); // High heat
      break;
  }

  // Vibration control
  if (digitalRead(buttonVibration) == LOW) {
    delay(200); // Debounce
    vibrationMode = (vibrationMode + 1) % 4; // Cycle through 0-3
  }

  // Adjust vibration motor based on vibrationMode
  switch (vibrationMode) {
    case 0:
      analogWrite(vibrationPin, 0); // Off
      break;
    case 1:
      analogWrite(vibrationPin, 85); // Low vibration
      break;
    case 2:
      analogWrite(vibrationPin, 170); // Medium vibration
      break;
    case 3:
      analogWrite(vibrationPin, 255); // High vibration
      break;
  }

  delay(100);
}
