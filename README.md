# JQ Home Assistant Configuration
My configuration for Home Assistant (https://home-assistant.io/)

## Custom Sensors / Devices (esphomeyaml)
See `/esp-sensors` directory for [esphomeyaml](https://esphomelib.com/esphomeyaml) configuration
 * 4x Multisensor (temp + humidity + motion) ([BRUH-based](https://esphomelib.com/esphomeyaml/cookbook/bruh.html))
 * Garage Car Presence Sensor (HC-SR04 ultrasonic)
 * Mini Blinds (stepper motor driver)
 * Power Strip (SM-SO301, flashed with tuya-convert)

## Devices in use:

 * HASwitchPlate x2
 * Synology NAS - Home Assistant host via Docker
 * Aeon Labs Z-stick - Z-Wave integration (overhead lights, switches, minimote)
 * MQTT via mosquitto
 * Hue - A19 bulbs + Hub + Strips
 * Chromecast - media player
 * Text-to-speech - Alexa announcements via Echo Dots and Echo Spot
 * Ubiquiti Unifi - presence detection
 * Apple HomeKit - presence detection bridge
 * Traccar - vehicle tracking
 * Nest - climate control
 * Flux - lighting temperature (via Hue)
 * Emulated Hue - lighting / script control via Amazon Alexa
 * Arlo - camera views inside HA dashboard, arming/disarming
 * Alarm.com - automated arming
 * Darksky weather
 * AirVisual air quality monitoring
 * Google Travel Time
 * Fast.com connection monitoring
 * UPS package notifications
 * System monitoring - CPU, RAM
 * Sunset, Time, Uptime, Workday sensors
 * Pushover notifications

## Presence Detection

Presence forms in use:
* WiFi detection via Ubiquiti access point
* HomeKit GPS based presence
* Car presence sensor in garage (esphomeyaml based)
* Car GPS Tracker via Traccar

## Automations:

### Morning

* Bring up the bedroom lights in daylight color gradually 30 min prior to wake up time (set via home assistant controls).
* On first motion in kitchen, bring up the lights, announce the weather forecast over kitchen speakers. If the current day is a work day, announce the travel time to work using Google travel time. Remind if a package is arriving.

### Away

* Turn off all lights and set Nest to away mode based off presence detection.
* Arm Arlo motion detection notifications
* Send push notification when away mode is activated.

### Return Home

* When arriving home, turn on entry lights for 10 minutes.
* Disarm Arlo motion detection notifications
* On first motion in kitchen after returning from away mode, play welcome message and bring up the main lights. Remind me to take out the trash, or get a package.

### Night

* Adjust lighting temperature via Flux periodically
* Turn on and off lights based off motion
* When bedtime is activated (via minimote or Alexa), play goodnight message, turn off main lights after 60 seconds, turn on bedroom lights, arm alarms, lock doors.
* After 10 minutes, slowly fade bedroom lights until completely off.
* On motion in kitchen, bring up kitchen lightstrips for 10 minutes.
* Turn off any lights still on after 2am.

### Misc

* 3D Printer on/off based off print status

### Notifications

* House temperature is below 55 degrees
* Sensor battery below 40%, check daily at 8pm
* Internet connection goes down or comes back up
* RAM usage on NAS is above 96%
* 3D printer job finished or failed
* Home Assistant startup
