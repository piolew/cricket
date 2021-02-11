# 2.2
## Notes
This FW upgrade requires to erase both WiFi credentials and configuration partitions.
After FW upgrade Cricket will back to binding mode.
## Bugs fixed
ISSUE #79 - When pressing BIN button Cricket to fetch config from COTA even when COTA is disabled on the device.\
ISSUE #73 - Binding UI misplaced on Apple devices.\
ISSUE #58 - WiFi password limited to 32 characters. Limit increased to 64 characters.\
ISSUE #54 - Cricket needs wake-up at least once to apply the configuration.
## New features
ISSUE #72 - Ability to rename topics for each property. This is only enabled when MQTT_CUSTOM is selected.\
ISSUE #76 - Added batt_voltage property for both HTTP tags and MQTT to report battery voltage.\
ISSUE #63 - Added Days for RTC configuration.\
ISSUE #50 - Enabled FW upgrade.
