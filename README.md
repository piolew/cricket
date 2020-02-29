[<img src="https://github.com/thingsonedge/cricket/blob/master/gfx/Leaflet-small.png" alt="drawing" width="200"/>](https://drive.google.com/file/d/1iJMbLQAMSyVuPYkd0Aa7GaR6Jpp-wKcA/view?usp=sharing)

# Overview

Cricket is a ultra-low battery powered Wi-Fi module, which can last for years on a single battery. 
It requires zero-code for building IoT devices an no hub to conenct to the internet.
It comes with a pre-installed software, which is integrated into Cloud. 
Connect devices to the internet out of the box either from a smartphone or a laptop from any web browser. 
Manage devices remotely and integrate to other systems using MQTT protocol. 


Main features:
* Can operate on a single AAA battery
* Ultra-low power, true 0A current when not in operation
* Built-in RTC used for wake_up
* Built-in temperature sensor
* Analog or Digital input for sensor
* Over-the-Air FW upgrade
* Cloud enabled HW configuration
* Battery monitor
* MQTT
* Easy integration with IFTTT


<img src="https://github.com/thingsonedge/cricket/blob/master/gfx/UseCases.png" alt="drawing" width="800"/>


TBD
MEasure Wake-up hi level 

# HW description

## Pins definition

|Pin   | Description | 
|---|---|
|BATT| Power supply VDD to the board, this can be connected directly to the battery |
|3V3| Output power from internal regulator. This is always 3.3V regardless on BATT voltage level |
|WAKE_UP|HI level on that pin will turn board on|
|IO2|Ditigal or Analog input signal|
|IO3|Reserved|
|GND|Ground|
|||

# Module operations
The Cricket have 2 mode of operations 

* Normal
* Binding 


<img src="https://github.com/thingsonedge/cricket/blob/master/gfx/Operation.svg" alt="drawing" width="800"/>

In normal operation board is powered off, in this state it needs aprox 250nA for RTC operation.
The board will stay off till either external WAKE_UP singal is provided or internal RTC is anabled and alarm is triggered. 
Once the board is woke up it perform FW initialization and preapare board for normal operation, this usually takes around 600ms. Next, board will read current configuration from its storage and evaluate all enabled sensors.
All sensors or parameters are enabled or disabled via configuration in the cloud service.

Sensor evaluation process
Check if sensor is enabled
Read last sensor from the flash storage
Read current sensor value 
Compare sensor value

If any from enabled senosors are enabled and current value is diferent than last value recorder the board will start cloud update process which involves WiFi connectivity and cloud update using MQTT or HTTP post method.
If neither of enabled sensor have new evaluated value the board will turn off imidiatelly till next wake up signal provided.

This mechanism allows to be very power efficient when opetate on the battery.

# Ultra low-power scenarios

## Use cases 

1. Push button to send event notification to the cloud
When powered on 2xAAA alkaine batteries it can perform aprox 10K event notificaition delivery to the cloud regardless of the idle time. As long as battery likage is not big it can operate 5-10 years to porovide 10K putton press events.
When powered on 2AAA lithium batteries it can perform aprox 15K push buttons events.

2. Temperature sensor 
As above using 2xAAA alkaine batteries bosard can send aprox 10K notificsation to the cloud.

Assuming the board will use RTC to wake-up every 1hr to measure temperature it can operate mroe than 1 year.

lifetime = 10000 / (24*365) = 1.14 years = 1 year 2 months
This is very pessimistic calkulation when it assumed the remperature is changed at least 0.5℃ every hour.
Realisticly in most of the enviroments the temperature will change 4x less frequent, the board can then operate 4x longer.

lifetime = 10000 / (6*365) = 4.6 years = 4 year 7 months


# Configuration

# Connect to Wi-Fi network
Connect Cricket to the internet with Wi-Fi network in a few steps. All you need to do is to activate Cricket's private Wi-Fi hotspot and then open a private web page to pass your Wi-Fi network credentials.

Please follow the steps below:

<h4>Step 1.</h4>
Press and hold a button on Cricket for 5 seconds until the LED is constantly lit.
It opens the "<b>toe_device</b>" WiFi hotspot.<br>
<img src="/gfx/Cricket-with-button.png" width="300"/>
<h4>Step 2.</h4>
Once the LED is constantly lit Cricket opened the "<b>toe_device</b>" private Wi-Fi hot spot. Connect to this hot spot either from a laptop or smartphone with the following credentials:
SSID: <b>toe_device</b>
Password: <b>thingsonedge</b>
<img src="gfx/1_connect_to_hotspot_.png" width="200"/>
<h4>Step 3.</h4>
Once connected, open a private web page: <a href="http://192.168.4.1/index.html" target="_blank"><b>http://192.168.4.1/index.html</b></a>
<b>NOTICE: make sure LED is still ON! If is OFF repeat the steps from the beginning (Step 1.)</b>
Now you can pass your Wi-Fi network credentials and click CONNECT. If you passed correct SSID and Password then after few seconds the device should report it is online and the LED will be OFF.
<br>
Congratulations! Now your device is live and connected to the internet!

# MQTT
Module connecting to its own MQTT broker which can be used free of charge bu the user.
Every sensor data is published using separate topics and can be read by MQTT client usually MQTT client mobile application or MQTT Client service.

## Connecting to the ThingsOnEdge MQTT broker

MQTT broker server requires authentication by providing login and password this is unique per each module.
For each module login and password is a module serial number provided on the back of the board.


| url | mqtt.thingsonedge.com |
| cliend_id | any |
| login | module serial number|
| password | module serial number|

Each message is delivered using retained flag, therefore last value of each sensor is cached in the server.

### MQTT topics 

Template

**/{SN}/{prop}**

where
SN    - Module unique serial nuber 
prop  - Module property/sensor type

|Name   | Format | Unit | Example  | Description  | 
|---|---|---|---|---|
| temp | dd.d | C | 12.5  | Temperature from on-board sensor  |
| batt  | ddd  | decimals  | 124  | Current battery voltage level represented as 8bits decimal value  |
| io2  | ddd | decimals  | 100  | Current level on the IO2 port, if IO2 is configured as digital this is either 0 or 1  |

d- single decimal digit

Analog signal can be converted to voltage using following formula

Vanalog = digital_value * (3.5/256)


# HTTP Push 


## Recomended operating conditions

|Operating Condition   | Symbol | Min | Typ | Max | Unit
|---|---|---|---|---|---
|Supply voltage| BATT | 1 | 3 | 3.5 | V
|Operating temperature|  | -40 | 20 | 125 | ℃
|Wake up voltage| Wake_up | 1 | 3 | 3.5 | V
||||||






## List of cricket properties




Battery voltag ecan be calculate using formula:
batt_vcc = batt * (3.5/256)

