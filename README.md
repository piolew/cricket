# Overview
[Cricket® Ultra-Low battery poered WiFi module](https://docs.google.com/document/d/1zjO7xJTKCzEvk4kBmdfn99eWAzofOHkFEcjfTbvVl10/edit?usp=sharing)

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

