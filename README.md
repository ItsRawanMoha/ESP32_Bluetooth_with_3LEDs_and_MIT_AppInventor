# ESP32 Bluetooth Control of 3 LEDs with MIT App Inventor

This task demonstrates how to control 3 LEDs using an ESP32 microcontroller and a mobile app created with MIT App Inventor. The ESP32 is programmed to receive commands over Bluetooth from the mobile app and toggle the states of the LEDs accordingly.

## Introduction

The ESP32 Bluetooth Control task provides a practical example of using Bluetooth communication to control hardware devices from a mobile app. By creating a simple interface with MIT App Inventor, users can send commands to the ESP32 to control the states of 3 LEDs wirelessly.

## How it Works

The ESP32 is configured to act as a Bluetooth server and listen for incoming commands from the mobile app. The mobile app, built with MIT App Inventor, sends commands to the ESP32 whenever a user interacts with the interface. Upon receiving a command, the ESP32 toggles the states of the connected LEDs accordingly.

## Getting Started

To get started with this task, you will need the following components:

- ESP32 development board
- 3 LEDs
- Jumper wires
- Mobile device with the MIT App Inventor Companion app installed

## Steps

Follow these steps to set up the task:

1. Connect the anodes (+) of the LEDs to three GPIO pins on the ESP32 (e.g., pins 2, 4, and 0).
2. Connect the cathodes (-) of the LEDs to the GND pin on the ESP32.
3. Upload the provided Arduino sketch to the ESP32.
4. Create a mobile app using MIT App Inventor that sends Bluetooth commands to control the LEDs.
5. Install the MIT App Inventor Companion app on your mobile device.
6. Pair your mobile device with the ESP32 via Bluetooth.
7. Open the MIT App Inventor Companion app and connect to the ESP32.
8. Use the mobile app interface to send commands to control the LEDs.

## Connection

The following table summarizes the wiring connections between the ESP32 and the LEDs:

| ESP32 Pin  | LED          |
| ---------- | ------------ |
| GPIO ( 2)  | Anode (+)    |
| GPIO ( 4)  | Anode (+)    |
| GPIO ( 0)  | Anode (+)    |
| GND        | Cathode (-)  |

## Output

Once the task is set up and the ESP32 is connected to the mobile app, you can use the app interface to control the states of the LEDs wirelessly via Bluetooth.

## Code

```
#include "BluetoothSerial.h" 

// init Class:
BluetoothSerial ESP_BT; 

// init PINs: assign any pin on ESP32
int led_pin_1 = 4;
int led_pin_2 = 0;
int led_pin_3 = 2;     // On some ESP32 pin 2 is an internal LED, mine did not have one

// Parameters for Bluetooth interface
int incoming;

void setup() {
  Serial.begin(19200);
  ESP_BT.begin("ESP32_Control"); //Name of your Bluetooth interface -> will show up on your phone

  pinMode (led_pin_1, OUTPUT);
  pinMode (led_pin_2, OUTPUT);
  pinMode (led_pin_3, OUTPUT);
}

void loop() {
  
  // -------------------- Receive Bluetooth signal ----------------------
  if (ESP_BT.available()) 
  {
    incoming = ESP_BT.read(); //Read what we receive 

    // separate button ID from button value -> button ID is 10, 20, 30, etc, value is 1 or 0
    int button = floor(incoming / 10);
    int value = incoming % 10;
    
    switch (button) {
      case 1:  
        Serial.print("Button 1:"); Serial.println(value);
        digitalWrite(led_pin_1, value);
        break;
      case 2:  
        Serial.print("Button 2:"); Serial.println(value);
        digitalWrite(led_pin_2, value);
        break;
      case 3:  
        Serial.print("Button 3:"); Serial.println(value);
        digitalWrite(led_pin_3, value);
        break;
    }
  }
}
```
![screen-gif](https://github.com/ItsRawanMoha/ESP32_Bluetooth_with_3LEDs_and_MIT_AppInventor/blob/main/image%20(23).png) 

## Pictures

<img src="https://github.com/ItsRawanMoha/ESP32_Bluetooth_with_3LEDs_and_MIT_AppInventor/blob/main/1.gif" alt="Alt text" width="500" height="400"> <img src="https://github.com/ItsRawanMoha/ESP32_Bluetooth_with_3LEDs_and_MIT_AppInventor/blob/main/1.jpeg" alt="Alt text" width="300" height="400">  


The ESP32, coupled with a button and an LED, can be configured to receive binary data (1 or 0) via Bluetooth. Utilizing the Serial Bluetooth Terminal app, users can send signals wirelessly to the ESP32, triggering the LED based on the received data. This simple setup enables remote control or automation applications where a button press on the app corresponds to turning the LED on or off. As shown below: 

<img src="https://github.com/ItsRawanMoha/ESP32_Bluetooth_with_3LEDs_and_MIT_AppInventor/blob/main/2.gif" alt="Alt text" width="400" height="600"> <img src="https://github.com/ItsRawanMoha/ESP32_Bluetooth_with_3LEDs_and_MIT_AppInventor/blob/main/2.jpeg" alt="Alt text" width="400" height="600">  

## Conclusion

The ESP32 Bluetooth Control task provides a practical demonstration of using Bluetooth communication to control hardware devices from a mobile app. By combining the capabilities of the ESP32 microcontroller and MIT App Inventor, users can create custom interfaces to interact with their tasks wirelessly.
