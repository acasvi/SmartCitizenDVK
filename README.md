Smart Citizen Kit DVK
=====================

**Smart Citizen Kit Develoment Kit (DVK) for RTX4100 and Arduino Due**

<img src="https://smartcitizen.me/img/sck_dvk.jpg" alt="SCK_DVK" style="width: 100%"/>

This shield has been designed to work with the [Arduino Due](http://arduino.cc/en/Main/arduinoBoardDue)

## First Steps

### Installing the toolchain

The tool chain includes primarily a pre-processor, a compiler, and a linker. The RTX41xx relies on the GCC ARM Embedded tool chain from ARM.

Prior to installation, download the GNU tools for ARM embedded processors installation file from: https://launchpad.net/gcc-arm-embedded/+milestone/4.7-2013-q3-update

Download the `gcc-arm-none-eabi-4_7-2013q3-20130916-win32.exe` file, save to disk and run the `.exe` file. 

Don't forget to click “Add path to environment variable” checkbox at the end of the installation.

Refer to **[RTX4100_User_Guide_Tools_Installation_UG2.pdf](https://github.com/fablabbcn/SmartCitizenDVK/blob/master/Documentation/RTX4100/RTX4100_User_Guide_Tools_Installation_UG2.pdf)** for a further explanation about installation the toolchain and SDK.

### Installing the SDK

After installing the Tool Chain, it is time to install the RTX41xx Software Development Kit (SDK). 

Go to the following link: [www.rtx.dk/LPW/RTX4100](http://www.rtx.dk/LPW/RTX4100) and click on DOWNLOAD link on top right.

You have to sign up to download the latest SDK(AmelieSdk_v1.6.0.58.exe).

Once you have downloaded open the .exe to start the installer.

The SDK delivery from RTX includes the following items:

* Sample code implementing the following applications: 
    * Blinky: Small example application that uses a timer to flash a LED on the demo board.
    * TCP Server/client
    * UDP Server/client
    * Terminal Application
    * 3 different Temperature Sensor implementations, demonstrating various low power capabilities.
    * TempSensorSoftApCfg, demonstrating how it is possible to configure a module by booting it in SoftAP mode with telnet support.
    * SoftApTcpServer, demonstrating an AP implementation with TCP server.
    * WebServer, demonstrating a very simple WEB server implementation.
    * Tcp2Uart, demonstrates a simple implementation of a data pipe
    * Cloud reference applications, demonstrating various cloud solutions 
    * Header files for available APIs.
    * Build environment: Build scripts, linker files etc. are provided for ARM GCC Em-bedded tool chain.
    * RTX EAI Port Server: PC application used for communicating with the hardware.
    * CoLA Controller DLL: Used for selecting active image and updating firmware.
    * CoLA Controller GUI: Example application using the DLL. In the end product the DLL could be used directly from e.g. an Eclipse IDE.

It is assumed that the SDK has been installed in c:\AmelieSdk\vX.XX, and the following description of the folder structure is relative to this location.

The following folders are at top level: 

* **3Party** – includes source files from 3rd parties. The most important file found here is the “efm32lib” from Energy Micro which is used to access the peripherals of the MCU.
* **ColaController** – The PC tool used to download Co-Located Applications to the module via the UART.
* **Components** – Source code to some common components used when the CoLA is built.
* **Documents** – Documentation folder.
* **Include** – Common header files.
* **Projects** – This is where you find the reference CoLA applications
* **Tools** – A set of tools used when the CoLA is built. This also includes the RtxBuild system used for the build process.

In the Project folder (Projects\Amelie\COLApps) you find the following folders:

* **Apps** – A set of reference applications 
	* Blinky – The source code for the Blinky application
	* Blinky/Build/RTX4100_WSAB – Build folder for RTX4100 module on WSAB.
	* Blinky/Build/RTX4140_WSAB – Build folder for RTX4140 module on WSAB.
* **Config** – This folder holds various configuration header files required to build the reference applications.
* **Rsx** – PC tool for API mail trace via UART.
* **Scripts** – build/linker scripts.

In the Components folder (Projects\Amelie\Componets) you find the following folders: 

* **Api** – Some API header files
* **ApiMps** – API mail packing and sending helper functions
* **Drivers** – Implementation of various hardware drivers 
* **PtApps** – Protothread based application framework used by all reference applica-tions except Blinky. 

Refer to RTX4100_User_Guide_Tools_Installation_UG2.pdf for a further explanation about installation the toolchain and SDK.

### Application Development

For start with the **application development** refer to chapter 4 on [RTX4100_User_Guide_Application_Development_UG3.pdf](https://github.com/fablabbcn/SmartCitizenDVK/blob/master/Documentation/RTX4100/RTX4100_User_Guide_Application_Development_UG3.pdf)

For **terminal commands to configure WIFI** module refer to chapter 5 on [RTX4100_User_Guide_Module_Evaluation_UG1.pdf](https://github.com/fablabbcn/SmartCitizenDVK/blob/master/Documentation/RTX4100/RTX4100_User_Guide_Application_Development_UG3.pdf)

For **API used to program Co-Located Applications (CoLA)** on top of the Amelie Wi-Fi platform refer to [AmelieApi_V0106_N0052.pdf](https://github.com/fablabbcn/SmartCitizenDVK/blob/master/Documentation/RTX4100/AmelieApi_V0106_N0052.pdf)

## Software

All the boards come with:

* Arduino firmware *[SmartCitizen_DVK.ino](https://github.com/fablabbcn/SmartCitizenDVK/tree/master/Firmware)* uploaded. 
* RTX firmware uploaded
* CoLA application for terminal communication with WIFI module uploaded, for available **terminal commands** refer to chapter 5 on *[RTX4100_User_Guide_Module_Evaluation_UG1.pdf](https://github.com/fablabbcn/SmartCitizenDVK/blob/master/Documentation/RTX4100/RTX4100_User_Guide_Module_Evaluation_UG1.pdf)*

To use the RTX Shield connect an usb cable in the programming port of the Arduino Due, the one closest to the DC power jack.

As you can see, the RTX shield has two push buttons, S1 and S2. With this two buttons you can change between 4 modes of operation.

**MODE 1**

This is the default mode when you connect the board, green LED is ON. This mode send through usb-serial, at 9600 bauds, the values captured by the temperature and humidity sensors and give you if a SD Card is detected or not. You can find this values in the main() function of  SmartCitizen_DVK.ino.

**MODE 2**

If push **S1**, green LED start to blinking. You are on terminal mode. If CoLa app for terminal communication is uploaded, yelllow LED ON, you can talk through USB-serial with the RTX WIFI module. If you push again S1, you'll go back to MODE 1.

**MODE 3**

If you push **S2**, blue LED ON, you can upload CoLA applications with **ColaController, **the PC tool used to download Co-Located Applications to the module via the UART. You can find this tool on ColaController folder inside Amelie SDK folder.

**MODE 4**

If you push **S2** again, green and blue LED ON, you will enter in RTX firmware uploading mode, then blue LED start to blinking.

To perform the Firmware update:

1. Download the firmware file **RTX41xx_Platform_Firmware_Update_Pack_v1.6.0.52.zip** from the RTX [download center](http://www.rtx.dk/Download_Center_Login-3980.aspx). 
2. Unzip the file to your harddrive. As this document is included in the above ZIP file you have probably already downloaded the file.

*NOTE: Each time you plug the arduino due with the shield to your computer automatically reses the mode to mode 1.*

## Hardware

SmartCitizen DVK shield design files are available [here](https://github.com/fablabbcn/SmartCitizenDVK/hardware).

### RTX4100 - Low power wifi module

* [http://www.rtx.dk/RTX41xx_Wi-Fi_modules-3921.aspx](http://www.rtx.dk/RTX41xx_Wi-Fi_modules-3921.aspx)

* [http://www.rtx.dk/Wi-Fi_Documentation-4028.aspx](http://www.rtx.dk/Wi-Fi_Documentation-4028.aspx)

The RTX41xx Wi-Fi Module is a low power solution, which is achieved through the use of the  Energy Micro Gecko and Atheros AR4100 Wi-Fi SiP.


**The I/O's include:**

* Power supply pins
* ADC ports, DAC ports
* GPIO ports
* UART, SPI, I2C
* Timers

### NC7SZ157P6X – MUX

[http://www.mouser.com/ds/2/149/NC7SZ157-96268.pdf](http://www.mouser.com/ds/2/149/NC7SZ157-96268.pdf)

The mux is used to select from Arduino which serial port of the RTX4100 you want to use.

You can select between two serial ports:

* −LEU1: (LEUART) is used for the Terminal application (such at Putty), for example.
* −US1: (USART) is used for CoLA loading, SW debugging and Platform updates (using the CoLA Controller)

### MCP1725-3002E/SN LDO REGULATOR

[http://ww1.microchip.com/downloads/en/DeviceDoc/22026b.pdf](%22http:)

3V fixed voltage regulator

### CD74HC4050M High-to-Low Voltage Level Converter

[http://www.mouser.com/ds/2/405/schs205i-101882.pdf](http://www.mouser.com/ds/2/405/schs205i-101882.p)

IC used as logic level converter between Arduino and the RTX4100 module.

### SDCARD

[http://www.mouser.com/ds/2/185/e60900232-38395.pdf](http://www.mouser.com/ds/2/185/e60900232-38395.pdf)

To hold the SD card we are using the DM3CS holder. The SD card is powered at 3V and communicates with the RTX4100 through SPI protocol.

### SHT21 Humidity and Temperature Sensor IC

[http://www.sensirion.com/fileadmin/user_upload/customers/sensirion/Dokumente/Humidity/Sensirion_Humidity_SHT21_Datasheet_V4.pdf](http://www.sensirion.com/fileadmin/user_upload/customers/s)

### LEDS

* LED1 YELLOW: Connected to RTX4100 pin 27, for testing Blink Colapp example
* LED2 BLUE: Connected to Arduino Analog0 pin
* LED3 GREEN: Connected to Arduino Analog1 pin