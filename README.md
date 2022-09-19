# :wave: Intrusion Detection System ⚠

## ✅ Desarrollo de un sistema inteligente de detección de Intrusos en una infraestructura IoT para agricultura de precisión.

Presentado por:
Génessis Mabel Enríquez Lalangui y Cristopher David Vega Salazar

## :octocat: Contents
- Anomaly Detector Software
- Intrusion Detecion System Software
- scheme.png
- esp32_mqtt.ino
- Mqtt.py
- Ubidots.py

## :octocat: Requirements
- Raspberry Pi 4 Model B
- Raspbian 64 bits OS
- IoT network hardware

## :octocat: Tools
- Scheme
The circuit must be assembled with the different sensors connected and working correctly, the same circuit and its connection is defined in the image where the project scheme is found.

- esp32_mqtt.ino file
When the sensors are connected to their respective esp-32, the esp32_mqtt.ino code must be loaded. It is important in line 65, for each node you must change the topic to which you are going to subscribe, that is, for each node you must put datos1, datos2, datos3, ..., datos# respectively.

