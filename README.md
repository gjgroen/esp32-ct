# Cheap Yellow Display
Deze repository hoort bij de masterclass over ESPHome en LVGL voor Computer!Totaal. We gebruiken in de masterclass een Cheap Yellow Display in combinatie met ESPHomne en de bibliotheek LVGL. Daarmee kun je grafische gebruikersinterfaces bouwen. Het touchscreen heeft het typenummer ESP32-2432S028. In de map esphome vind je een werkend voorbeeld (cyd-demo.yaml). Een vergelijkbare demo voor de Elecrow 5 inch en 7 inch touchscreens volgt nog.

Merk op dat er ook een (oudere) variant van dit touchscreen is met de ILI9341. In dat geval gebruik je `model: ILI9341` en `invert_colors: false`.

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
- https://github.com/Lumics/EspressiShotTimer. Project op basis van PlatformIO, VSCode en Arduino met tips voor componenten.

# Deurbel slim maken
Een ouderwetse deurbel met beltrafo werkt doorgaans met beltransformator die 8 volt wisselspanning geeft. Voor zo’n €5 kun je deze slim maken, zonder ingrijpende wijzigingen. Je hebt niet meer dan een ESP32, led, optocoupler (zoals de 4N35) en een weerstand van 1k (afhankelijk van de wisselspanning) om de stroom naar de led te beperken. Home Assistant krijgt nu de melding als er op de bel wordt gedrukt, en daarmee kun je bijvoorbeeld een tweede bel of gong laten rinkelen, of een mp3-bestand op een slimme luidspreker afspelen. Je kunt het natuurlijk op allerlei manieren uitbreiden. Zo zou je een push notificatie naar je smartphone kunnen sturen of een snapshot maken van een camera bij de voordeur.

Op https://td-er.nl/2014/05/12/bestaande-en-kaku-deurbel/ zie je een voorbeeld voor een schakeling waarmee je een deurbel met beltrafo slim kunt maken. Alleen gebruik je nu geen KaKu-zender maar een ESPHome. We hebben voor de aansluiting de onderstaande YAML-code gebruikt in ESPHome.

```
binary_sensor:
  - platform: gpio
    id: button
    name: DeurbelButton
    pin:
      number: GPIO14
      mode: INPUT_PULLUP
      inverted: true
    filters:
      - delayed_off: 100ms
```
