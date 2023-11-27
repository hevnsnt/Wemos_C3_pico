# Wemos_C3_pico
Information about the Wemos C3 Pico.  These are just my notes for getting the Pico working with ESPHome and HomeAssistant. There is a significant lack of documentation available for these new devices, so I am posting this publically hopefully to make your configuration easier. 


## RGB LED: Connected to Pin 7

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

### Set RGB to green if connected to Wifi
```
interval:
  - interval: 1s
    then:
      if:
        condition:
          wifi.connected:
        then:
          - light.turn_on: RGBLed
        else:
          - light.turn_off: RGBLed
```
