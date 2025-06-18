//p. s.: yes i know how to use void, and using them was ai's advice, but i still know how to use them
//optimisation and some functions ideas copyright chatgpt.com
#include <Servo.h>

// pins for the ultrasonic sensor
int trigPin = 7;
int echoPin = 6;

// RGB LED pins
int redPin = 11;
int greenPin = 10;
int bluePin = 12;

// pins for the buzzer and the servo motor
int buzzerPin = 8;
int servoPin = 13;

//variables
long time;
float distance;
static float prevDistance = 0; // remembers the last distance

float range = 0;  // gonna be changed later

Servo myServo; 

// stuff for moving the servo smoothly
int servoPos = 0;
int servoDirection = 1; 
int servoMin = 10;
int servoMax = 170;

unsigned long lastServoMove = 0;
unsigned long servoInterval = 20; // how often the servo should move

// alert system stuff
bool alertMode = false;
unsigned long alertStart = 0;
unsigned long alertDuration = 10000; // 10 seconds of alert

// panic timer stuff
bool panicPending = false;
unsigned long panicTimerStart = 0;
const unsigned long panicWaitTime = 5000; // 5 seconds to confirm danger

// setup stuff
bool rangeSet = false;
unsigned long setupStartTime;

void setup() {
  // setup the sensor and output pins
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);

  pinMode(redPin, OUTPUT);
  pinMode(greenPin, OUTPUT);
  pinMode(bluePin, OUTPUT);

  pinMode(buzzerPin, OUTPUT);

  myServo.attach(servoPin); // connect the servo
  myServo.write(servoMin);  // move it to start position

  Serial.begin(9600); // start the serial monitor
  setupStartTime = millis(); // save the start time
}

void loop() {
  // wait 3 seconds to set the normal range
  if (!rangeSet && millis() - setupStartTime >= 3000) { 
    range = measureDistance(); // get starting distance
    rangeSet = true;
    Serial.print("Fixed range set to: ");
    Serial.println(range);
  }

  distance = measureDistance(); // measure distance every loop

  Serial.print("Distance: ");
  Serial.println(distance);

  if (rangeSet) {
    // if the object moved far or suddenly changed position
    if (abs(distance - prevDistance) > 4 || distance > range + 15) {
      if (!panicPending && !alertMode) {
        panicPending = true;
        panicTimerStart = millis();
        Serial.println("Warning detected...");
      }
    } else {
      if (panicPending) {
        Serial.println("Warning cancelled - object back in range.");
        panicPending = false;
      }
    }

    // if danger lasted too long, trigger alert
    if (panicPending) {
      if (millis() - panicTimerStart >= panicWaitTime) {
        if (!alertMode) {
          alertMode = true;
          alertStart = millis();
          Serial.println("ALERT! Panic triggered!");
          tone(buzzerPin, 1000); // start buzzer
        }
      }
    }

    if (alertMode) {
      alertRGB(255, 0, 0); // make the LED red
      myServo.write(90);   // move servo to middle
      if (millis() - alertStart > alertDuration) {
        alertMode = false;
        panicPending = false;
        noTone(buzzerPin); // stop buzzer
        Serial.println("Alert ended.");
      }
    } else {
      alertRGB(0, 255, 0); // green LED if all good
      moveServoSmooth();  // keep moving servo left and right
    }
  }

  prevDistance = distance; // update last distance
  delay(50); // wait a little bit
}

float measureDistance() {
  // basic ultrasonic distance measurement
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);

  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  time = pulseIn(echoPin, HIGH);
  return time * 0.0343 / 2; // convert time to cm
}

void moveServoSmooth() {
  unsigned long currentMillis = millis();
  if (currentMillis - lastServoMove >= servoInterval) {
    servoPos += servoDirection;
    if (servoPos >= servoMax) {
      servoPos = servoMax;
      servoDirection = -1;
    } else if (servoPos <= servoMin) {
      servoPos = servoMin;
      servoDirection = 1;
    }
    myServo.write(servoPos); // move servo to new position
    lastServoMove = currentMillis;
  }
}

void alertRGB(int r, int g, int b) {
  // set LED color
  analogWrite(redPin, r);
  analogWrite(greenPin, g);
  analogWrite(bluePin, b);
}
