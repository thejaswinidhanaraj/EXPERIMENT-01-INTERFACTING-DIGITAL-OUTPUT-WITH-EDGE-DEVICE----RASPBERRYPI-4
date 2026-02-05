# EXPERIMENT-01-INTERFACTING-DIGITAL-OUTPUT-WITH-EDGE-DEVICE---(RASPBERRYPI-PI4)
### NAME : THEJASWINI D  
### DEPARTMENT : B.E.CSE(IOT)
### REGISTER NO : 212223110059
### DATE OF EXPERIMENT :04.02.2026

### AIM
To interface a digital output device (LED) with the Raspberry Pi 4 and control it using Python.

## APPARATUS REQUIRED
Raspberry Pi 4
LED (Light Emitting Diode)
330Ω Resistor
IR Sensor
Breadboard
Jumper Wires
USB Cable
 ## THEORY

![Raspberry Pi Pin](https://github.com/user-attachments/assets/19e5a1e7-cb46-4909-ba59-e4f4560cae03)





 
 
 
 ### FIGURE-01 RASPI PI 4 PINOUT DIAGRAM 


The Raspberry Pi 4 Model B is built around a Broadcom BCM2711 system-on-chip that integrates a quad-core ARM Cortex-A72 (64-bit) CPU, VideoCore VI GPU, memory controller, and peripheral interfaces, forming a compact yet complete computer architecture where the SoC connects internally to RAM, USB 3.0 controller, Gigabit Ethernet, HDMI display, and wireless modules. Its 40-pin GPIO header provides a flexible pin configuration consisting of power pins (5 V and 3.3 V), multiple ground pins, and general-purpose input/output pins that operate at 3.3 V logic and can be programmed for digital I/O or alternate functions. Key alternate functions include I²C (SDA, SCL) for sensor communication, SPI (MOSI, MISO, SCLK, CS) for high-speed peripheral interfacing, UART (TX, RX) for serial communication, and PWM for control applications.  For communication, I2C (SDA, SCL), SPI (MOSI, MISO, SCK), and UART (TX, RX) interfaces are mapped across different GPIO pins, allowing seamless connectivity with sensors and peripherals. All GPIO pins support PWM (Pulse Width Modulation), making it useful for motor control, LED brightness adjustment, and sound applications. The BOOTSEL button enables USB mass storage mode for firmware flashing, while the DEBUG pins (SWD interface) provide debugging capabilities. With its low power consumption, flexible GPIO options, and rich interface support, the Raspberry Pi Pico is widely used for IoT, embedded systems, robotics, and automation projects.This architecture and pin multiplexing allow the Raspberry Pi 4 to act as both a general-purpose computing platform and an embedded controller, supporting rapid prototyping, hardware interfacing, and IoT applications.


## Working Principle:
Experiment 1A
The LED is connected to one of the GPIO pins of the Raspberry Pi 4.
The Python script sets the GPIO pin HIGH to turn the LED ON and LOW to turn it OFF.
CIRCUIT DIAGRAM
Connect the anode (longer leg) of the LED to GP15 via a 330Ω resistor.
Connect the cathode (shorter leg) of the LED to GND (ground).

Experiment 1B
The LED is connected to one of the GPIO pins of the Raspberry Pi 4.
The IR sensor is connected one of the GPIO pins in Raspberry Pi 4.
The Python script sets the GPIO pin HIGH to turn the LED ON and LOW to turn it OFF based on the IR sensor.
CIRCUIT DIAGRAM
Connect the anode (longer leg) of the LED to any one GPIO via a 330Ω resistor.
Connect the cathode (shorter leg) of the LED to GND (ground).
Connect the IR sensor Vcc to any +5V.
Connect the IR sensor GND to any GND.
Connect the IR sensor OUT to any one GPIO. 

## PROGRAM (Python)
## EXPERIMENT 1A
```
import RPi.GPIO as GPIO
import time
import urllib.request
#ThingSpeak details
WRITE_API_KEY="UMETZ0NGLC8SYTG4"
CHANNEL_ID = 3249653
THINGSPEAK_URL = "https://api.thingspeak.com/update"
#Set GPIO numbering mode
GPIO.setmode (GPIO.BCM)

# Define LED pin
LED_PIN 18

#Set GPI018 as output
GPIO.setup(LED_PIN, GPIO.OUT)

def send_to_thingspeak(value):
    url=f"https://api.thingspeak.com/update?api_key-UMETZ0NGLC8SYTG4&field=(value)"
    urllib.request.urlopen(url)
    print("Sent to ThingSpeak:", value)

try:
    while True:
        #LED_ON
        GPIO.output(LED_PIN, GPIO.HIGH)
        print("LED_ON")
        send_to_thingspeak(1)
        time.sleep(15)
        #LED_OFF
        GPIO.output (LED_PIN, GPIO.LOW)
        print("LED_OFF")
        send_to_thingspeak(0)
        time.sleep(15)

except KeyboardInterrupt:
    print("Program stopped")
finally:
    GPIO.cleanup() 
```

## EXPERIMENT 1B
```
import RPi.GPIO as GPIO
import time
import urllib.request

# ThingSpeak details
WRITE_API_KEY = "52UXZLCFHXHH3KRA"
CHANNEL_ID = 3249843
THINGSPEAK_URL = "https://api.thingspeak.com/update"



# Pin setup
SENSOR_PIN = 23   # Input from sensor
LED_PIN = 18      # Output to LED

# GPIO mode
GPIO.setmode(GPIO.BCM)

# Setup pins
GPIO.setup(SENSOR_PIN, GPIO.IN)
GPIO.setup(LED_PIN, GPIO.OUT)

def send_to_thingspeak(value):
    url = f"https://api.thingspeak.com/update?api_key=52UXZLCFHXHH3KRA&field2={value}"
    urllib.request.urlopen(url)
    print("Sent to ThingSpeak:", value)


print("Sensor + LED system running...")

try:
    while True:
        sensor_value = GPIO.input(SENSOR_PIN)

        if sensor_value == 0:   # Many IR sensors give LOW when object detected
            print("Object Detected! LED ON")
            GPIO.output(LED_PIN, GPIO.HIGH)
            send_to_thingspeak(1)

            time.sleep(15)
        else:
            print("No Object. LED OFF")
            GPIO.output(LED_PIN, GPIO.LOW)
            send_to_thingspeak(0)

            time.sleep(15)

        time.sleep(0.1)

except KeyboardInterrupt:
    print("Stopped by user")

finally:
    GPIO.cleanup()
```
### OUPUT  
## Experiment 1A
# LED ON

![edge1](https://github.com/user-attachments/assets/1fb37af6-5424-4bfc-8259-30308a306975)

![edge4](https://github.com/user-attachments/assets/1f29fcfb-d502-4d17-884d-07dd9bdfbf62)

<img width="1886" height="908" alt="Screenshot 2026-02-04 112425" src="https://github.com/user-attachments/assets/a4d3e155-5ddd-4a85-917b-1c4010e36600" />


# LED OFF

![edge2](https://github.com/user-attachments/assets/bdd68a5b-0ab7-4db0-b798-abfb6393b1a7

![edge3](https://github.com/user-attachments/assets/7b179504-6d28-483d-88db-665755431279)

<img width="1878" height="898" alt="Screenshot 2026-02-04 112440" src="https://github.com/user-attachments/assets/aa5b1a39-4b6b-43aa-8e44-d58374bb8f75" />

## Experiment 1B
## Obstacle not detected
![edge6](https://github.com/user-attachments/assets/a7dadbf4-3e89-4b05-85f3-267222bc54ee)

![console](https://github.com/user-attachments/assets/6f977acc-bd30-4849-9264-9cb9c402bb25)

<img width="1502" height="837" alt="image" src="https://github.com/user-attachments/assets/5fa5a073-2103-47ce-800f-2650a84b8f29" />

## Obstacle detected 
![edge5](https://github.com/user-attachments/assets/81dad74d-ea3f-45d1-ae96-8bac7411905e)

![console1](https://github.com/user-attachments/assets/cc710286-c79e-41e1-8fab-5aaaf99c7fd8)

<img width="1893" height="883" alt="image" src="https://github.com/user-attachments/assets/0c19a3fb-7506-4586-97b3-35abf41c6f72" />

## RESULTS
The LED connected to the Raspberry Pi 4 successfully turns ON and OFF at  user defined time  confirming the proper interfacing of a digital output.
