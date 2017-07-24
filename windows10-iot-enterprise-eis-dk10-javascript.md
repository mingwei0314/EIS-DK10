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
    -   [Option 1: Use the development board, without sensors](#Device-Sample)
    -   [Option 2: Use the Machinery Predictive Diagnostic Maintenance System kit from NEXCOM](#Kit01-Sample)
-   [Next Steps](#NextSteps)

<a name="Introduction"></a>
# Introduction

**About this document**

This document describes how to connect CPS-200 device running Windows 10 IoT Core with Azure IoT SDK. This multi-step process includes:
-   Configuring Azure IoT Hub
-   Registering your IoT device
-   Build and deploy Azure IoT SDK on device

<a name="Prerequisites"></a>
# Step 1: Prerequisites

You should have the following items ready before beginning the process:

-   Computer with Git client installed and access to the
    [azure-iot-sdk-csharp](https://github.com/Azure/azure-iot-sdk-csharp) GitHub public repository.
-   [Setup your IoT hub][lnk-setup-iot-hub]
-   [Provision your device and get its credentials][lnk-manage-iot-hub]
-   CPS-200 device.

#### Install Visual Studio 2015 and Tools

-   To create Windows IoT Core solutions, you will need to install [Visual Studio 2015](https://www.visualstudio.com/en-us/products/vs-2015-product-editions.aspx). You can install any edition of Visual Studio, including the free Community edition.

    Make sure to select the **Universal Windows App Development Tools**, the component required for writing apps Windows 10:

<a name="PrepareDevice"></a>
# Step 2: Prepare your Device

-   Nothing to do here.

<a name="Build"></a>
# Step 3: Build and Run the Sample

<a name="Step_3_1_Connect"></a>
## 3.1 Connect the Device

-   Connect the board to your network using an Ethernet cable. This step is required, as the sample depends on internet access.

-   Plug the device into your computer using a micro-USB cable.

<a name="Step_3_2_Build"></a>
## 3.2  Build the Samples

<a name="Device-Sample"></a>
## Option 1: Use the development board, without sensors

-   Start a new instance of Visual Studio 2015. Open the **iothub_csharp_client.sln** solution (/azure-iot-sdk-csharp) from your local copy of the repository.

-   In Visual Studio, from **Solution Explorer**, navigate to the **UWPSample(Universal Windows)** project.

-   Locate the following code in the **ConnectionStrings.cs** file:

        public const string DeviceConnectionString = "<replace>";

-   Replace the above placeholder with device connection string you obtained in [Step 1](#Prerequisites) and save the changes.

-   Choose the right architecture (x86 or ARM, depending on your device) and set the debugging method to "Remote Machine":
    
-   To deploy the binaries on your device, right-click on the UWPSample project in the **Solution Explorer**, select **Properties** and navigate to the **Debug** tab:

    Type in the name of your device. Make sure the "Use authentication" box is unchecked.

-   Build the solution.

<a name="Step_3_3_Run"></a>
## 3.3 Run and Validate the Samples

### 3.3.1 Send Device Events to IoT Hub

-   In Visual Studio, from **Solution Explorer**, right-click the **UWPSample(Universal Windows)** project, click **Debug &minus;&gt; Start new instance** to build and run the sample. 

-   See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to observe the messages IoT Hub receives from the application.

### 3.3.2 Receive messages from IoT Hub

-   See [Manage IoT Hub][lnk-manage-iot-hub] to learn how to send cloud-to-device messages to the application.

<a name="Kit01-Sample"></a>
## Option 2: Use the Machinery Predictive Diagnostic Maintenance System kit from NEXCOM

### Machinery Predictive Diagnostic Maintenance System kit

The Machinery Predictive Diagnostic Maintenance System kit includes:

-   NEXCOM CPS 200 device + *Rockwell PLC/ Dector, XM Module*

-   Rotor kit

-   Inverter with Modbus/TCP Gateway

> [*http://www.nexcom.com/Products/industrial-computing-solutions/iot-solutions/iot-gateway/rotor-w-iot-gateway-iot-gateway*](http://www.nexcom.com/Products/industrial-computing-solutions/iot-solutions/iot-gateway/rotor-w-iot-gateway-iot-gateway)
>
> ![image01](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image1.jpeg)

### Connect the sensors

There are three parts: Main Set, Rotor kit and Inverter. Follow the
picture below to connect CH1 to CH1, CH2 to CH2 and Accelerometer to
Tachometer.

![image02](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image2.jpeg)

![image03](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image3.jpeg)

**Build and Run the sample**

GitHub source code

[*https://github.com/allanchen1971/IOTHubSample01*](https://github.com/allanchen1971/IOTHubSample01)

Run the application and click the “Connect” button to get the Modbus
data.

**Send Device Events to IoT Hub**

Then start send to IoT Hub.

We sent the Temperature/Humidity/MotoSpeed/DI/Input and control
Lamp/Fan/MotoSpeed to IoT Hub

![image04](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image4.jpeg)

**Receive messages from IoT Hub**

We receive the Temperature/Humidity/MotoSpeed/DI/Input and control
command: Lamp/Fan/MotoSpeed from IoT Hub

On the remote side, we send command (list below) from IotHub to device,

Speed: (0-100)/lamp:on/lamp:off/fan:on/fan:off

After device(Gateway) got the command, it will control the device to set
Fan On/Off and Lamp On/Off and control the motor speed.

Lamp On:

![image05](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image5.png)

Fan On:

![image06](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image6.png)

Speed:

![image07](media/nexcom-machinery-predictive-diagnostic-maintenance-system-kit/image7.png)

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

