[<img src="/gfx/Leaflet-small.png" alt="drawing" width="200"/>](https://drive.google.com/file/d/1iJMbLQAMSyVuPYkd0Aa7GaR6Jpp-wKcA/view?usp=sharing)

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


<img src="/gfx/Cricket-with-desc-small.png" alt="drawing" width="800"/>

# Examples of what you can build
* <a href="https://www.thingsonedge.com/post/manage-your-blog-from-your-live-site" target="_blank"><b>IoT: Wi-Fi moisture sensor powered on a battery</b></a>

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
Press and hold a button on Cricket for <b>5 seconds</b> until the LED is constantly lit.
It opens the "<b>toe_device</b>" WiFi hotspot.<br>
<img src="/gfx/Cricket-with-button.png" width="300"/>
<h4>Step 2.</h4>
Once the LED is constantly lit Cricket opened the "<b>toe_device</b>" private Wi-Fi hot spot. Connect to this hot spot either from a laptop or smartphone with the following credentials:<br>
SSID: <b>toe_device</b><br>
No password is required<br><br>
<img src="gfx/1_connect_to_hotspot_.png" width="200"/>
<h4>Step 3.</h4>
Once connected, open a private web page: <a href="http://192.168.4.1/index.html" target="_blank"><b>http://192.168.4.1/index.html</b></a>
<br><b>NOTICE: make sure LED is still ON! If is OFF repeat the steps from the beginning (Step 1.)</b><br>
Now you can pass your Wi-Fi network credentials and click CONNECT. If you passed correct SSID and Password then after few seconds the device should report it is online and the LED will be OFF.
<br>
Congratulations! Now your device is live and connected to the internet!<br>

# Connectivity
There are two ways of publishing data from the moduke to the online service.

MQTT - module comes with already integrated MQTT connectivity
HTTP - module can be configured to push HTTP Push request to desired location with customized payload

MQTT connectivity is always enabled and if there is any data to publish the module will perform MQTT publish to the specyfic topic.
Then, client can connect to ThingsOnEdge MQTT broker and subscribe for that topic to receive recent data update.

PICTURE

If user already using another MQTT broker it is possible to establish connection between 2 brokers in such way that client's broker subscribe specyfic topic from
ThingsOnEdge broker.

PICTURE

Available topics for Cricket

| Topic | mqtt.thingsonedge.com |
| cliend_id | any |




# MQTT
Module connecting to its own MQTT broker which can be used free of charge bu the user.
Every data send over MQTT from the module uses separate MQTT topics. 

List of of all topics

Topic teample
**/{SN}/{prop}**
where<br>
**{SN}**    - Module unique serial number <img src="gfx/Cricket-serial-number-400px.png" width="150"/><br>
**{prop}**  - Module property/sensor type

|{prop}   | Format | Unit | Example  | Description  | 
|---|---|---|---|---|
| temp | dd.d | C | 12.5  | Temperature from on-board sensor  |
| batt  | ddd  | decimals  | 124  | Current battery voltage level represented as 8bits decimal value  |
| io2  | ddd | decimals  | 100  | Current level on the IO2 port, if IO2 is configured as digital this is either 0 or 1  |
| io1_wake_up  | ddd | decimals  | 1  | The payload of that topic is 1 if board was woken up using IO1 pin otherwise os 0. This message is only published if either IO1 wake-up is triggered or "Force updates on" is enabled in the module configuration.  |

d- single decimal digit


## Connecting to the ThingsOnEdge MQTT broker
MQTT broker server requires authentication by providing login and password which is unique for each module.
Module serial number shnould be use for both password and user when connecting from MQTT client.




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

