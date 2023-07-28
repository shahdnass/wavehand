# wavehand

This is an Arduino project that uses an ultrasonic sensor to measure distance and controls a servo motor based on that distance.

## Setup and Requirements

- Arduino board
- HC-SR04 Ultrasonic Sensor
- Servo Motor
- Arduino IDE with the Servo library

## How to Use

1. Connect the HC-SR04 sensor to the Arduino board:
   - VCC pin to 5V
   - GND pin to GND
   - TRIG pin to Arduino pin 9
   - ECHO pin to Arduino pin 8

2. Connect the servo motor to the Arduino board:
   - Signal pin to Arduino pin 7
   - VCC and GND as per servo motor requirements

3. Open the Arduino IDE and upload the sketch to the Arduino board.

4. Once uploaded, the Arduino will read the distance using the ultrasonic sensor and control the servo motor based on the distance. When an object is detected within 40 cm, the servo will rotate to 90 degrees and then back to 0 degrees repeatedly.

## circuit diagram

<img src="https://github.com/shahdnass/wavehand/assets/123496373/42aa6c2a-ca62-4cf1-9295-6ba21f42f2f2">
  
 

## simulation link

 https://www.tinkercad.com/things/cc7nughBHGg-terrific-hillar/editel?sharecode=K0EqffsbfgJ26dPXrsztGsyApbKNvJt1H6D1BV8-zt8


 ## code
 ```
 #include <Servo.h>
int TRIG = 9;
int ECHO = 8;
int servosignal = 7;
Servo servo;
int pos = 0;
float time;
float distance;
float Distance;

void setup()
{
  Serial.begin(9600);
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  servo.attach(servosignal);
}

void loop()
{
  Distance = calculateDis(TRIG, ECHO);
  Serial.print("Distance = ");
  Serial.println(Distance);
  
  wave();
}

float calculateDis(int trig, int echo)
{
	digitalWrite(trig, LOW);
    delayMicroseconds(5);
  	digitalWrite(trig, HIGH);
	delayMicroseconds(10);
  	digitalWrite(trig, LOW);
  
  time = pulseIn(echo, HIGH);
    // read the echo, returns the sound wave travel time in microseconds

  distance = (time/2) * 0.034;
  	//calculate distance
  return distance;
}

void wave()
{
  if(Distance < 40){
    servo.write(180); // rotate the servo motor to 90 degree
    delay(1500); 
    servo.write(0); // rotate the servo motor back to 0 degree
    delay(1500); 
  }else
    servo.write(0);
}
```

 
 
