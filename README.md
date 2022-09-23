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

- ### Scheme

  The circuit must be assembled with the different sensors connected and working correctly, the same circuit and its connection is defined in the image where the project scheme is found.

- ### esp32_mqtt.ino

  When the sensors are connected to their respective esp-32, the esp32_mqtt.ino code must be loaded. It is important in line 65, for each node you must change the topic to which you are going to subscribe, that is, for each node you must put datos1, datos2, datos3, ..., datos# respectively.

- ### Mqtt.py

  This file has a python code that is used to subscribe to the topics that the esp-32 nodes have, it validates if there is a file and proceeds to save all the data it receives from the sensors in a data.csv file. This tool must be executed to obtain the data sample that will be entered into the anomaly detector for machine learning training.
  
- ### Ubidots.py
  
  This file has a python code that is used to subscribe to the topics that the esp-32 nodes have, it is responsible for uploading all the data obtained from the sensors to the web server in the ubidots cloud, where different alerts of according to the conditions and sensors of the crops. It is important to rely on lines 15 and 16, with the variables TOKEN and DEVICE_LABEL respectively. Where in the first variable the unique token of each ubidots account that is downloaded is entered, and the second variable is used to enter the name of the label where the data is saved. It is important to control how often the data is sent to the web server, since being in a free service has a limit of upload data per day.
  
## :octocat: Gmail Account

  Given that in order for the program to send emails, it is necessary to identify yourself with a login, since it represents a great security flaw to enter the email and password of the email, since it would be visible to anyone. It is necessary to convert the gmail account to security level 2 and generate an application key.
In the following link.

This key consists of a combination of 16 random characters that allows the program to send emails without having to write the main key.

## :octocat: Anomaly Detector

- ### Installation

  To correctly execute the anomaly detector program, the respective libraries must be installed, for this a 64-bit system is necessary and after the installation, an update of packages and libraries must be done.
  
  ```
  sudo apt-get update
  sudo apt-get dist-upgrade
  ```
  We make sure we have the python package management system installed and updated to its latest version.
  
  ```
  pip install --upgrade pip
  ```
  
  The libraries that are necessary for the execution of the program are installed.
  ```
  pip install tensorflow
  pip install pandas
  pip install matplotlib
  pip install paho-mqtt
  ```
- ### Execution
  #### Step 1. 
  
  Enter the file where the sample of the real data that was taken with the sensors using the mqtt.py tool is located, it must be entered with the name of sample.py
  
  #### Step 2.
  Generate the machine learning model file so that the program is able to learn from it, for this the train.py file is executed
  ```
  python train.py
  ```
  #### Step 3.
  With the generated model only the program is executed. anomaly_detector.py
  ```
  python anomaly_detector.py
  ```
  It is important to mention that the program will detect anomalies and notify infinitely with all the data obtained through mqtt subscription, for that it is recommended to put a delay of how often you want the code to be executed synchronized with the time that the sensors send , so that they are always updated and new data is obtained.

## :octocat: Intrusion Detection System
- ### Installation
 To correctly execute the anomaly detector program, the respective libraries must be installed, for this a 64-bit system is necessary and after the installation, an update of packages and libraries must be done.
  
  ```
  sudo apt-get update
  sudo apt-get dist-upgrade
  ```
  We make sure we have the python package management system installed and updated to its latest version.
  
  ```
  pip install --upgrade pip
  ```
  
  The libraries that are necessary for the execution of the program are installed.
  ```
  pip install tensorflow
  pip install pandas
  pip install numpy
  pip install json
  pip install joblib
  pip install paho-mqtt
  ```
- ### Execution

  #### Step 1.
  The model of the IDS is entered in its respective folder, the sample with the network traffic data in its respective folder and the different files with their functions that are necessary for the use of CIC-IDS2017
  
  #### Step 2. 
  We focus on the constants.py file where are the variables used for analysis, notification, module control, file location, etc.
  
  ##### Module and Feature Flags.
  Using a boolean control we can control different parts of the code that we want to be executed as a switch, if you want it to work it is defined as True, otherwise False is entered
  
  ##### Variables.
  We use the variables EMAIL_FROM and EMAIL_PASSWORD as sender email to send notification email in case of an attack, the email must be entered as a text variable using double quotes "" and the password must be an application password that was generated previously in point from Gmail Account
  
  For the EMAIL_TO variable, it is where the destination email address is entered as a string, that is, where the notification will arrive.
  
  For the UBIDOT_TOKEN and UBIDOT_DEVICE variables, for the first one the token is entered, which is the unique code generated by the ubidots account, instead for the second one the label with which the monitoring will be saved is entered and it is uploaded to ubidots information.
  
  ##### Network Interface
  In the variable CIC_INTERFACE we enter the interface of the network card that we want to analyze the traffic. In case of being connected by cable or Wi-Fi, the respective name and number must be entered, that is, eth0 or wlan0, and so on.
  
  ##### Directories and Files
  Included in these variables are the locations of files that are used throughout the different functions and execution of the code.
  
  #### Step 3.
  Given the complexity of the libraries and tools that the program has, since it analyzes system files, the program must be run with administrator permissions
  ```
  sudo nids.py
  ```
  
  
