**Nane:** Nicolas Marandi

**Company:** CODETECH IT SOLUTION PVT LTD

**ID:**  CT08DS5176

**Domain:** INTERNET OF THINGS

**Duration:** JULY 15TH TO AUGUST 15TH 2024

**Mentor:** Muzammil Ahmed


# Overview of the Project

### Project:IoT-Based Smart Home System

 ## Project Goal
 
 The primary goal of this project is to create an IoT-based smart home system that allows users to control home appliances such as lights, fans, and thermostats remotely via a mobile app or web interface. The project will utilize popular IoT development platforms like Arduino and Raspberry Pi to build the hardware components and integrate them with software solutions for user interaction and control.

 ## Key Components
 
 **Hardware Components:**
 
 **Microcontroller/Single-Board Computer:** Arduino or Raspberry Pi for controlling appliances.
 
**Relays/Switches:** To switch appliances on and off.

**Sensors:** For monitoring environmental conditions (e.g., temperature, humidity).

**WiFi Module:** ESP8266 for Arduino or built-in WiFi on Raspberry Pi.

**Power Supply:** Adequate power supply for the microcontroller and connected components

## Software Components:

**Firmware for Microcontroller:** Code running on Arduino/Raspberry Pi to manage appliance control
.
**Backend Server:** To handle requests from the mobile app or web interface and communicate with the microcontroller.

**Mobile App/Web Interface:** For users to remotely control appliances.

## System Architecture

## Microcontroller Setup:

**Arduino:** Programmed with C++ using the Arduino IDE, equipped with ESP8266 for WiFi connectivity
.
**Raspberry Pi:** Programmed using Python, running a web server using Flask to handle HTTP requests.

## Appliance Control:

Relays are connected to the microcontroller to switch appliances on and off based on received commands.
Sensors are connected to gather environmental data which can be used to automate appliance control.

## Communication Protocol:

**MQTT:** Lightweight messaging protocol for small sensors and mobile devices (Arduino setup).

**HTTP/REST API:** For sending commands from the backend server to the Raspberry Pi.

## User Interface:

**Mobile App:** Built using frameworks like React Native, allowing cross-platform functionality.

**Web Interface:** Built using modern web development frameworks like React or Vue.js.

## Development Steps

## Hardware Configuration:

Assemble the Arduino or Raspberry Pi with relays, sensors, and WiFi module.
Connect the relays to the appliances you want to control.
## Firmware Development:

Write and upload code to the Arduino to handle MQTT communication and control relays.
Write Python scripts for Raspberry Pi to handle GPIO pins and HTTP requests.
## Backend Server Setup:

Develop a server (using Node.js, Python Flask, or Django) to handle incoming commands from the mobile app/web interface.
Implement endpoints to communicate with the microcontroller.
## Mobile App/Web Interface Development:

Develop the user interface allowing users to send control commands to the backend server.
Implement features for user authentication, appliance control, and status monitoring.

## Integration and Testing:

Test the communication between the mobile app/web interface, backend server, and microcontroller.
Verify the control of appliances through the user interface.
Debug and troubleshoot any issues that arise during testing.

## Example Code Snippets

## Arduino with ESP8266 for MQTT Communication:

#include <ESP8266WiFi.h>
#include <PubSubClient.h>

const char* ssid = "your-SSID";
const char* password = "your-PASSWORD";
const char* mqtt_server = "your-MQTT-SERVER";

WiFiClient espClient;
PubSubClient client(espClient);

void setup() {
  pinMode(D1, OUTPUT);
  Serial.begin(115200);
  setup_wifi();
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void setup_wifi() {
  delay(10);
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
}

void callback(char* topic, byte* payload, unsigned int length) {
  String message;
  for (int i = 0; i < length; i++) {
    message += (char)payload[i];
  }
  if (String(topic) == "home/appliance") {
    if (message == "ON") {
      digitalWrite(D1, HIGH);
    } else if (message == "OFF") {
      digitalWrite(D1, LOW);
    }
  }
}

void reconnect() {
  while (!client.connected()) {
    if (client.connect("ESP8266Client")) {
      client.subscribe("home/appliance");
    } else {
      delay(5000);
    }
  }
}

void loop() {
  if (!client.connected()) {
    reconnect();
  }
  client.loop();
}



### Raspberry Pi with Flask for HTTP Communication:

## python


from flask import Flask, request, jsonify
import RPi.GPIO as GPIO

app = Flask(__name__)

GPIO.setmode(GPIO.BCM)
GPIO.setup(18, GPIO.OUT)

@app.route('/control', methods=['POST'])
def control():
    data = request.json
    appliance = data['appliance']
    state = data['state']
    if appliance == 'light' and state == 'on':
        GPIO.output(18, GPIO.HIGH)
    elif appliance == 'light' and state == 'off':
        GPIO.output(18, GPIO.LOW)
    return jsonify({'status': 'success'})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)


## React Web Interface:

## javascript

import React, { useState } from 'react';
import axios from 'axios';

function App() {
  const [state, setState] = useState('off');

  const handleToggle = async () => {
    const newState = state === 'off' ? 'on' : 'off';
    setState(newState);
    await axios.post('http://your-backend-server/control', {
      appliance: 'light',
      state: newState
    });
  };

  return (
    <div>
      <h1>Smart Home Control</h1>
      <button onClick={handleToggle}>
        Turn Light {state === 'off' ? 'On' : 'Off'}
      </button>
    </div>
  );
}

export default App;

## Web interface output


![Alt text](JPG File (.JPG))



## Conclusion

As the conclusion, a prototype of smart home automation system can be developed with
Arduino Mega 2560 as microcontroller. Besides, ultrasonic sensor and LM35 temperature
sensor acts as a medium of communication. Other than that, automated light system is running
when people enter the house by using ultrasonic sensor to detect people’s motion. Next,
the surrounding temperature can be detected and switched on the fan when surrounding
temperature is higher than range set by using LM35 temperature sensor. Hence, all the
objectives were achieved.
By following this overview, you can develop a basic IoT-based smart home system that provides remote control of home appliances through a user-friendly interface. The combination of Arduino or Raspberry Pi with a robust backend server and intuitive user interface creates a comprehensive and functional smart home solution.


























 












