#Arduino Code 

```cpp
#include <AccelStepper.h>

// Constructor for the stepper motor
AccelStepper stepper(AccelStepper::DRIVER, 9, 8);

// Constants and Variables

//Arduino Inputs
const int ledBlue = 2;
const int ledGreen = 3;
const int ledRed = 4;
const int backwardsPin = 5;
const int buttonPin = 6;
const int forwardsPin = 7;
const int limitSwitch = 10;

//Other
const int stepsPerRevolution = 200;
const float syringeDiameter10 = 14.3; //mm
const float syringeDiameter20 = 19.6; //mm
bool syringePumping = false;
bool yellow_light = false;
int buttonState = 0;
int forwardsState = 0;
int backwardsState = 0; 
int lastButtonState = HIGH; // Assume the button starts unpressed
int lastLimitState = HIGH;

float pi = 3.14159;
unsigned long lastDebounceTime = 0;
unsigned long debounceDelay = 50; // Debounce delay in milliseconds

//Variables to change 
float flowRate = 0.4; // mL/min
float syringeDiameter = syringeDiameter10; // mm

//Equations to calculate flow rate from motor step rate 
float linear_velocity = (flowRate * 1000)/ (60 * pi * sq(syringeDiameter/2));//changes to mm/s
float Revolution_per_second = (linear_velocity / 2); //RPS given a linear_velocity in rev/sec
float steps_per_second = (Revolution_per_second * stepsPerRevolution);

void setup() {
  pinMode(buttonPin, INPUT);
  pinMode(limitSwitch,INPUT_PULLUP);
  pinMode(backwardsPin, INPUT_PULLUP);
  pinMode(forwardsPin, INPUT_PULLUP);
  pinMode(ledRed, OUTPUT);
  pinMode(ledGreen, OUTPUT);
  pinMode(ledBlue, OUTPUT);

  stepper.setMaxSpeed(2500);
  stepper.setAcceleration(400);
  stepper.setSpeed(steps_per_second);
  Serial.begin(9600);

}

void loop() {
  int buttonReading = digitalRead(buttonPin);
  int limitSwitchState = digitalRead(limitSwitch);
  int forwardReading = digitalRead(forwardsPin);
  int backwardReading = digitalRead(backwardsPin);
  // Check for a change in the button state

  if (buttonReading != lastButtonState) {
    lastDebounceTime = millis();
  }

  if ((millis() - lastDebounceTime) > debounceDelay) {
    if (buttonReading != buttonState) {
      buttonState = buttonReading;


      if (buttonState == LOW) {
        // Toggle the syringePumping state
        syringePumping = true;
        forwardReading = HIGH;
        backwardReading = HIGH;
        stepper.setSpeed(400);
        stepper.runSpeed();
        digitalWrite(ledRed, LOW);
        digitalWrite(ledGreen, HIGH);
        digitalWrite(ledBlue, LOW);
        Serial.println("Forward");
        Serial.println(steps_per_second);
      } else {
        syringePumping = false;
         stepper.setSpeed(0);
          analogWrite(ledRed, 255); // Assuming these are digital pins
          analogWrite(ledGreen, 100);
          analogWrite(ledBlue, 0);
          Serial.println("Syringe Pumping: OFF");
      }
    }
  }

  lastButtonState = buttonReading;

  if (limitSwitchState == LOW) {
    syringePumping = false;
    buttonReading = HIGH;
    forwardReading = HIGH;
    yellow_light = false;
    stepper.setSpeed(0);
    digitalWrite(ledRed, HIGH);
    digitalWrite(ledGreen, LOW);
    digitalWrite(ledBlue, LOW);

  }

    if (backwardReading == LOW && syringePumping == false) {
    stepper.setSpeed(-abs(600));
    // Set negative speed for backward direction
    stepper.runSpeed();
    digitalWrite(ledRed, LOW);
    digitalWrite(ledGreen, HIGH);
    digitalWrite(ledBlue, LOW);
  }

  if (forwardReading == LOW && syringePumping == false) {
    syringePumping = true;
    stepper.setSpeed(steps_per_second);
   // Set positive speed for forward direction
    stepper.runSpeed();
    digitalWrite(ledRed, LOW);
    digitalWrite(ledGreen, HIGH);
    digitalWrite(ledBlue, LOW);
  }

  if (forwardReading == HIGH && backwardReading == HIGH && syringePumping == false && limitSwitchState == HIGH) {
    stepper.setSpeed(0);
    yellow_light = true;
    if (yellow_light = true) {} 
      analogWrite(ledRed, 255); // Assuming these are digital pins
      analogWrite(ledGreen, 100);
      analogWrite(ledBlue, 0);
    }
  

  // Continuously run the stepper motor if pumping
  if (syringePumping) {
    stepper.runSpeed();
    Serial.println(steps_per_second);
  }
  }
  ```




