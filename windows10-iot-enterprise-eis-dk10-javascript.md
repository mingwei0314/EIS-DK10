---
platform: windows 10 iot enterprise
device: eis-dk10
language: nodejs
---

Run a simple nodejs sample on eis-dk10 device running Windows 10 IoT Enterprise
===
---

# Table of Contents

-   [Introduction](#Introduction)
-   [Step 1: Prerequisites](#Prerequisites)
-   [Step 2: Prepare your Device](#PrepareDevice)
-   [Step 3: Build and Run the Sample](#Build)
    -   [Use the EIS-DK10 starter kit from Advantech](#Build)
-   [Next Steps](#NextSteps)

<a name="Introduction"></a>
# Introduction

**About this document**

This document describes how to connect EIS-DK10 device running Windows 10 IoT Enterprise with Azure IoT SDK. This multi-step process includes:
-   Configuring Azure IoT Hub
-   Registering your IoT device
-   Build and deploy Azure IoT SDK on device

<a name="Prerequisites"></a>
# Step 1: Prerequisites

You should have the following items ready before beginning the process:

-   Computer with Git client installed and access to the
    [azure-iot-sdk-node](https://github.com/Azure/azure-sdk-for-node) GitHub public repository.
-   [Setup your IoT hub][lnk-setup-iot-hub]
-   [Provision your device and get its credentials][lnk-manage-iot-hub]
-   EIS-DK10 device.

<a name="PrepareDevice"></a>
# Step 2: Prepare your Device

-   Install Nodejs
-   Install Node-RED
-   Install node-red-contrib-azureiothubnode
-   Install node-red-contrib-modbus

<a name="Build"></a>
## Use the EIS-DK10 starter kit from Advantech

### EIS-DK10 starter kit

The EIS-DK10 starter kit includes:

-   ARK-1123H
-   Temperature/Humidity Sensor
-   LED Indicator
-   Cooling Fan
-   Wireless I/O Module

> [*http://www.advantech.com/products/071c0784-5e9b-4bb8-bb07-2cb06da757a1/eis-dk10/mod_83b56167-5f19-4967-9d0a-cc3c67cecb36*](http://www.advantech.com/products/071c0784-5e9b-4bb8-bb07-2cb06da757a1/eis-dk10/mod_83b56167-5f19-4967-9d0a-cc3c67cecb36)

### Connect the sensors

Step 1: Connector sensor with cable
![image01](media/Connector-sensor-with-cable.JPG

Step 2: Connect WISE-4012 to Devices
![image02](media/Connect-WISE-4012-to-Devices1.JPG)
![image03](media/Connect-WISE-4012-to-Devices2.JPG)
![image04](media/Connect-WISE-4012-to-Devices3.JPG)

Step 3: Connect Power Converter Cable
![image05](media/Connector-sensor-with-cable.JPG)

Step 4: Connect Power Cable with Adaptor and System
![image06](media/Connect-Power-Cable-with-Adaptor-and-System.JPG)

Step 5: Done Assemble
![image07](media/Done-Assemble.JPG)

**Build and Run the sample**

Use Node-RED import flow (Send data to IoT Hub)


**Send Device Events to IoT Hub**

Then start send to IoT Hub.

We sent the Temperature/Humidity/LEO0/FAN to IoT Hub


**Receive messages from IoT Hub**

<a name="NextSteps"></a>
# Next Steps

You have now learned how to run a sample application that collects sensor data and sends it to your IoT hub. To explore how to store, analyze and visualize the data from this application in Azure using a variety of different services, please click on the following lessons:

-   [Manage cloud device messaging with iothub-explorer]
-   [Save IoT Hub messages to Azure data storage]
-   [Use Power BI to visualize real-time sensor data from Azure IoT Hub]
-   [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]
-   [Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]
-   [Remote monitoring and notifications with Logic Apps]   

[Manage cloud device messaging with iothub-explorer]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-explorer-cloud-device-messaging
[Save IoT Hub messages to Azure data storage]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-store-data-in-azure-table-storage
[Use Power BI to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-power-bi
[Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-live-data-visualization-in-web-apps
[Weather forecast using the sensor data from your IoT hub in Azure Machine Learning]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-weather-forecast-machine-learning
[Remote monitoring and notifications with Logic Apps]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-monitoring-notifications-with-azure-logic-apps
[lnk-setup-iot-hub]: ../setup_iothub.md
[lnk-manage-iot-hub]: ../manage_iot_hub.md

