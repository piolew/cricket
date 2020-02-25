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

In normal operation board is in off state and waits for wake_up signal which can be provided either by applying HI level voltage to the WAKE_UP signal or from internal RTC chip which is configured from the cloud service.
Once the board wakes up it perform initialization and properties evaluation, if any of the enabled properties is changed the module will initialize WiFi conenctio and send updated values to the cloud service using either MQTT or HTTP Post method.

<img src="https://github.com/thingsonedge/cricket/blob/master/gfx/Operation.svg" alt="drawing" width="800"/>




### Wake_up singal
The module can operate 


## Recomended operating conditions

|Operating Condition   | Symbol | Min | Typ | Max | Unit
|---|---|---|---|---|---
|Supply voltage| BATT | 1 | 3 | 3.5 | V
|Operating temperature|  | -40 | 20 | 125 | ℃
|Wake up voltage| Wake_up | 1 | 3 | 3.5 | V
||||||

# Configuration

# Binding

# MQTT

# HTTP Push 



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

