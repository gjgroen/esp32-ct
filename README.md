# Cheap Yellow Display
We gebruiken in de masterclass een Cheap Yellow Display met LVGL in ESPHome. 

![Touchscreen](https://github.com/gjgroen/esp32-ct/blob/main/09_cyd.jpg)

## Aansluitschema
Hier zie je de aansluitingen. In dit voorbeeld is een BME 280 aangesloten via de I2C-bus.
![Aansluitschema](https://github.com/gjgroen/esp32-ct/blob/main/aansluitingen.png)

## GPIO
Een kleine beperking bij displays met ingebouwde ESP32 is dat er maar enkele gpio-pinnen beschikbaar zijn, terwijl die wel nodig kunnen zijn om extra componenten aan te sluiten. Meestal is wel een I2C-interface beschikbaar. Via slechts twee pinnen kun je dan een zogeheten io-expander aansluiten, bijvoorbeeld de MCP23017 of SX1509. Die geven je 16 extra gpio-pinnen, waarbij de SX1509 ook pwm-signalen ondersteunt voor bijvoorbeeld het dimmen van leds. Je hebt vaak nog wel een passende connector nodig.

```
i2c:
  sda: GPIO27
  scl: GPIO22
  scan: true
  id: i2c_bus_a
```

## Extra tips
Op deze websites vind je nog aanvullende tips voor dit scherm:
- https://github.com/witnessmenow/ESP32-Cheap-Yellow-Display
- https://github.com/BOlaerts/ESP32-2432s028
- https://macsbug.wordpress.com/2022/08/17/esp32-2432s028/


# Espresso-timer
Op de volgende websites vind je tips en instructies voor het bouwen van een shottimer voor, in dit voorbeeld, een Lelit Mara X. 
- https://github.com/alexrus/marax_timer?tab=readme-ov-file. Dit project gebruikt een reed-content en werkt met elke espressomachine met vibratiepopmp. 
- https://github.com/alexrus/marax_timer?tab=readme-ov-file. Dit project werkt alleen voor de Mara X en gebruikt de seriële interface om te bepalen wanneer de pomp wordt gestart.

# Deurbel slim maken
Op https://td-er.nl/2014/05/12/bestaande-en-kaku-deurbel/ zie je een voorbeeld voor een schakeling waarmee je een deurbel met beltrafo slim kunt maken.
