# Overview

Cricket is a ultra-low battery powered WiFi module, which can last for years on single batteries. 
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


Reference-style: 
![alt text][cricket_overview]

<img src="https://github.com/thingsonedge/cricket/blob/master/gfx/UseCases.png" alt="drawing" width="200"/>

[cricket_overview]: https://github.com/thingsonedge/cricket/blob/master/gfx/UseCases.png "Logo Title Text 2"


# MQTT topics 

Topic template
/{SN}/{prop}

where :
SN    - Module unique serial nuber 
prop  - Module property

## List of cricket properties


|Name   | Format | Unit | Example  | Description  | 
|---|---|---|---|---|
| temp | dd.d | C | 12.5  | Temperature from on-board sensor  |
| batt  | ddd  | decimals  | 124  | Current battery voltage level represented as 8bits decimal value  |
| io2  | ddd | decimals  | 100  | Current level on the IO2 port, if IO2 is configured as digital this is either 0 or 1  |
| io3  | d | decimals  | 1  | Level on the IO3 port either 0 or 1  |

d- single decimal digit

Battery voltag ecan be calculate using formula:
batt_vcc = batt * (3.5/256)

