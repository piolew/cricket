# FW 2.2

## Notes
This FW upgrade require erase both WiFi creadencial and configuration partitions.\
After FW upgrdate Cricket will back to binding mode.


## Bugs fixed
ISSUE #79 - When pressing BIN buttom Cricket fetch cofing from COTA even when COTA is disabled on the device.\
ISSUE #73 - Binidng UI missplaced on Apple devices.\
ISSUE #58 - WiFi password limited to 32 characters. Limit increased to 64 characters.\
ISSUE #54 - Cricket needs wake-up at least once to apply configuration.

## New features
ISSUE #72 - Ability to rename topics for each propery. This is only enabled when MQTT_CUSTOM is selected.\
ISSUE #76 - Added batt_voltage property for both HTTP tags and MQTT to report battery voltage.\
ISSUE #63 - Added Days for RTC configuration.\
ISSUE #50 - Enabled FW upgrade.
