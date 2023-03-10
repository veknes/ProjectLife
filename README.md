# Project Life - Monitoring Movement, Heart Beat Rate and Blood Oxygen Level of Elderly People

**Group Name:** Smart Dolphins\
**Owners:** Veknes Benjaman; Saw Jun Chao

### 1.0 Introduction
Monitoring elderly people at home is an important way to ensure their well-being and safety, and to support their independence and quality of life.
There are several reasons why it is important to monitor elderly people at home:

- **Safety**\
Elderly people may be more vulnerable to accidents and injuries, such as falls, due to physical or cognitive impairments. Monitoring can help to identify potential safety hazards and take steps to address them.

- **Health**\
Elderly people may be at higher risk for certain health conditions, such as chronic diseases or infections. Monitoring can help to identify any changes in the elderly person's health and ensure that they receive necessary medical care.

- **Independence**\
Monitoring can help to ensure that elderly people are able to live independently for as long as possible. It can also provide reassurance to elderly people and their families that someone is available to help if needed.

- **Quality of Life**\
Monitoring can help to improve the quality of life for elderly people by ensuring that their needs are met and that they have social and emotional support.

- **Peace of Mind**\
Monitoring can provide peace of mind for family members and caregivers, who can be reassured that the elderly person is safe and well-cared for.

For example, elderly people are at higher risk for severe illness and death from recent COVID-19 for a number of reasons. As people age, their immune systems tend to become weaker, making it more difficult for their bodies to fight off infections. 
In addition, older people are more likely to have underlying health conditions, such as heart disease, diabetes, and lung disease, which can increase their risk of complications from COVID-19 [7].
Therefore, it is essential to monitor them regularly at home.

### 2.0 Use Case
This project consists of developing a STM32 based system for monitoring movement of elderly people at home and alerting family members through push notification if blood oxygen level, heart beat rate are not in normal range or if emergency push button is pressed.

### 3.0 Previous Research / Work
There are a few research done previously similar to this proposed system:

- **"Design of rescue and health monitoring bracelet for the elderly based on STM32"** (2019) [8]\
This study described the development of a bracelet, equipped with an STM32F103 microcontroller and an ST188 heart rate monitor, utilizes Bluetooth technology to communicate with a smartphone app for temperature and heart rate monitoring, as well as a one-button rescue function. The system, which also includes a MLX90614 temperature sensor, allows for body monitoring and emergency assistance. By pressing the help button, the user can quickly call an emergency contact and send their location and heart rate within two seconds.

- **"Design of Health Assistant Bracelet for the Elderly Based on STM32"** (2019) [8]\
This study described the design of a bracelet, equipped with an STM32F103VET6 microcontroller and an ST188 heart rate monitor, uses an InvenSense MPU6050 sensor to track steps and monitor sleep patterns through a connected smartphone app. In addition to providing health monitoring, the bracelet also has a one-button rescue function. By pressing the help button, the user can quickly call an emergency contact and send their location and health information to the emergency contact.

- **"Research and design of elderly health monitoring and anti-fall positioning alarm device based on STM32"** (2021) [8]\
This study described the development of a device, which utilizes an STM32 single chip microcomputer system with a modular design, includes a SIM800 C mobile communication module and a GPS positioning module to provide location and state information in the event of an unexpected fall. It also integrates sensors such as body temperature, heart rate, and step number to monitor the elderly person's health in real time, and sends an alarm if any data are abnormal. Additionally, the device includes a cloud monitoring app based on the E4A platform to allow for real-time monitoring of the elderly person's physical state.
 
### 4.0 System Architecture (Hardware)
The block diagram of the hardware connection is shown in Figure 1. The function and connection type of each components are described in Table 1.

<center><img src="/pictures/1_Hardware_Block_Diagram.png"></center>

Figure 1: Block diagram of hardware connection.

<center><br>Table 1: Function and connection type of components used.</center><br />
<center>

| Component  | Connection Type | Function |
| :-------: | :------: | :------: |
| 3-Axis Accelerometer | I2C | Provides acceleration data (the rate of change of velocity) for 3 axis |
| Oximeter and Heart Rate Sensor | I2C | Provides blood oxygen level and heart rate data |
| Push Button | INT | User input for emergency purpose | 
| ESP8266 | USART | Allows internet connectivity and sends data to cloud database (Firebase) |

</center>


### 5.0 Algorithm (Software)

**5.1 Implementing low power or sleep mode**
- Configure the RTC to wake up the STM32 periodically from low power modes to read sensors and upload collected data to Firebase Realtime Database.
- Configure push button interrupt to wake up STM32 to trigger Firebase Realtime Database to send emergency push notification to mobile application.

<center><img src="/pictures/2_Software_SleepMode_Block_Diagram.png"></center>

Figure 2: Block diagram of sleep and wake up mode software algorithm.

**5.2 TinyML model preparation for inferencing**
- Accelerometer data will be used to determine if the person are stationary, walking or running.
- Oximeter and heart beat rate data will be used to determine if it is in stable level or not.
- Preparing dataset for two senarios above to train model with Google Colab or utilizing pre-trained model (if available).
- Utilizing X-CUBE-AI expansion package (part of STM32Cube.AI ecosystem). It extends STM32CubeMX capabilities with automatic conversion and optimization of pretrained artificial intelligence algorithms, including neural network and classical machine learning models.
- X-CUBE-AI supports models trained with TensorFlow, Keras, PyTorch, Caffe and others. The model file needs to be in Keras (.h5), TensorFlow Lite (.tflite), or ONNX (.onnx) format.

<center><img src="/pictures/3_Software_TinyML_Block_Diagram.png"></center>

Figure 3: Block diagram of TinyML software algorithm.

**5.3 Google Firebase Realtime Database**
- Cloud database to store sensor data and send push notification to mobile application.

**5.4 Android Application**
- Developing a simple android application for monitoring data from Firebase Realtime Database and to receive push notification.
- Drag and drop based mobile application development such as MIT App Inventor or others.

## Appendix A: Bill of Materials (BOM)

<center>Table 2: Bill of Materials (BOM).</center><br />


<center>

| Component  | Unit | Cost / Unit (RM) |
| :-------: | :------: | :------: |
| STM32F407VET6 Development Board | 1 | 70 |
| ST-Link V2 USB | 1 | 20 |
| 3-Axis Accelerometer | 1 | 10 |
| Oximeter and Heart Rate Sensor | 1 | 10 |
| Push Button | 1 | 1 | 
| ESP8266 WiFi Serial Transceiver Module | 1 | 10 |
|  |  Total Cost (RM) | 121 |

</center>

## References

[1] Board Details and Schematics: [https://stm32-base.org/boards/STM32F407VET6-STM32-F4VE-V2.0.html](https://stm32-base.org/boards/STM32F407VET6-STM32-F4VE-V2.0.html)\
[2] STM32CubeIDE Tutorial:\
[https://www.st.com/resource/en/user_manual/um2609-stm32cubeide-user-guide-stmicroelectronics.pdf](https://www.st.com/resource/en/user_manual/um2609-stm32cubeide-user-guide-stmicroelectronics.pdf)\
[https://www.youtube.com/playlist?list=PLnMKNibPkDnFCosVVv98U5dCulE6T3Iy8](https://www.youtube.com/playlist?list=PLnMKNibPkDnFCosVVv98U5dCulE6T3Iy8)\
[3] Motion Sensing Dataset:\
[https://wiki.st.com/stm32mcu/wiki/AI:How_to_perform_motion_sensing_on_STM32L4_IoTnode#Create_an_STM32Cube-AI_application_using_X-CUBE-AI](https://wiki.st.com/stm32mcu/wiki/AI:How_to_perform_motion_sensing_on_STM32L4_IoTnode#Create_an_STM32Cube-AI_application_using_X-CUBE-AI)\
[https://github.com/STMicroelectronics/stm32ai/tree/master/AI_resources/HAR](https://github.com/STMicroelectronics/stm32ai/tree/master/AI_resources/HAR)\
[4] TinyML:\
[https://www.digikey.my/en/maker/projects/tinyml-getting-started-with-stm32-x-cube-ai/f94e1c8bfc1e4b6291d0f672d780d2c0](https://www.digikey.my/en/maker/projects/tinyml-getting-started-with-stm32-x-cube-ai/f94e1c8bfc1e4b6291d0f672d780d2c0)\
[5] ESP8266 STM32 Connection:\
[https://controllerstech.com/esp8266-webserver-using-stm32-hal/]( https://controllerstech.com/esp8266-webserver-using-stm32-hal/)\
[6] STM32 Low Power Mode:\
[https://controllerstech.com/low-power-modes-in-stm32/](https://controllerstech.com/low-power-modes-in-stm32/)\
[https://community.st.com/s/article/how-to-configure-the-rtc-to-wake-up-the-stm32-periodically-from-low-power-modes](https://community.st.com/s/article/how-to-configure-the-rtc-to-wake-up-the-stm32-periodically-from-low-power-modes)\
[7] COVID-19 Inpatient Deaths and Brought-in-Dead Cases in Malaysia:\
[https://www.researchgate.net/publication/361819420_COVID-19_Inpatient_Deaths_and_Brought-in-Dead_Cases_in_Malaysia](https://www.researchgate.net/publication/361819420_COVID-19_Inpatient_Deaths_and_Brought-in-Dead_Cases_in_Malaysia)\
[8] Previous Research Paper:\
[Design of rescue and health monitoring bracelet for the elderly based on STM32](https://ieeexplore.ieee.org/document/8785440)\
[Design of Health Assistant Bracelet for the Elderly Based on STM32](https://ieeexplore.ieee.org/document/8997765)\
[Research and design of elderly health monitoring and anti-fall positioning alarm device based on STM32](https://ieeexplore.ieee.org/document/9513059)
