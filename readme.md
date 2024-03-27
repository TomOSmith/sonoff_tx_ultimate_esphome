Do not use this yet.  It doesn't compile in ESPHome.  Trying to figure out package substitution to reduce file verbosity to handle all combinations of button / relay / led arrangement.

# Sonoff TX Ultimate ESPHome
A base configuration for Sonoff TX Ultimate switches for use with ESPHome packages.  Covers 1-4 relay counts and 86 (EUR) / 120 (US) variants.  Most of the configuration is done in /packages/txUltimate.base.yaml and the associated base files for ESP32 configuration (/packages/esp32.base.yaml) and general base configuration (/packages/device.base.yaml)

## Configuration
| Substitution   | Required | Type | Description |
| :------------- | :------- | :--- | :---------- |
| name           | true     | str  | Name of the device |
| ip             | true     | str  | IP address of the device |
| light_format   | true     | int  | LED layout of the device, must be 86 (EUR) or 120 (US) |
| button_count   | true     | int  | Number of buttons, must be 1 to 4 |
| relay_count    | true     | int  | Number of relays, must be 1 to 4 |
| button_on_time | false    | time | Time for button to be on (must be positive) |
| light_on_time  | false    | time | Time for lights to confirm button press (0 is disabled) | 
| haptic_on_time | false    | time | Time for haptic motor to confirm button press (0 is disabled) | 
| failsafe_mode  | false    | bool | Allow buttons to control in the event of wifi disconnection |


## Notes:
The buttons / lights are currently configured as per 120 (US) devices with buttons running from top to bottom.  The 86 (EUR) devices orient buttons left to right, but being square should be simple enough to rotate into the comparable orientation.  It's on my to do list to create configurations where buttons are setup left to right, but focussing on getting the configuration running with reasonable optimisation first (otherwise things get unhelpfully verbose).

The TouchPanel UART component comes from https://github.com/SmartHome-yourself/sonoff-tx-ultimate-for-esphome.  I had to comment out line 7 of the /components/tx_ultimate_touch/tx_ultimate_touch.h file as the binary_sensor.h file was preventing the compilation.  Ideally I'd like to revert the /packages/txUltimate_base.yaml to point at the github rather than the local copy.