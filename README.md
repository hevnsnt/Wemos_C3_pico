# Wemos_C3_pico
Information about the Wemos C3 Pico.  These are just my notes for getting the Pico working with ESPHome and HomeAssistant. There is a significant lack of documentation available for these new devices, so I am posting this publically hopefully to make your configuration easier. 

![WEMOS PICO ESP32-C3 Pinout](/images/c3_pico_v1.png)
![WEMOS PICO ESP32-C3 Back](/images/c3_pico_v1_back.png)


## Onboard RGB LED: Connected to Pin 7

### Example configuration entry for ESPHome
```
light:
  - platform: neopixelbus
    type: RGB
    variant: WS2812
    pin: 7
    num_leds: 1
    name: "RGBLed"
    id: RGBLed
```

### Set RGB to RED if not connected to wifi, green when connected to Wifi
```
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password

  # Enable fallback hotspot (captive portal) in case wifi connection fails
  ap:
    ssid: "ESP32-C3 Fallback Hotspot"
    password: "XXXXXXXXXXXXXXX"

  on_connect:
    - light.turn_on: 
        id: RGBLed
        red: 0%
        green: 100%
        blue: 0%
    - delay: 3s
    - light.turn_off:
        id: RGBLed
  on_disconnect:
    - light.turn_on: 
        id: RGBLed
        red: 100%
        green: 0%
        blue: 0%

```
