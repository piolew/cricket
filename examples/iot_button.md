# Description
This and example of IoT smart button powered by 2xAAA batteries.
This example can be used to control diferent devices supported by IFTTT or other services with HTTP post API.

Once button is pressed, the Cricket module sends HTTP post request to desired address.

# Assembly

<img src="https://github.com/thingsonedge/cricket/blob/master/examples/iot_button_fritzing.png" alt="drawing" width="800"/>

# Configuration


|Name   | Value | Notes |
|---|---|---|
|RTC| OFF | |<br>
|IO1| Wake up | |<br>
|IO2| OFF | |
|IO3| OFF | |
|Battery monitor| OFF | |
|IO1 Wake Up| YES | |
|RTC Wake Up| NO | |
|io1_wakeup| http://maker.ifttt.com/trigger/button_event/with/key/xxxxxxxxxxx | Leave data empty, this must be taken from Webhooks from IFTTT
||||
