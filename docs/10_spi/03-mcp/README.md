---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Aansturen van een MCP23S09 SPI-IO-expander

In de volgende figuur wordt een blokschema van MCP23S09 weergegeven. Het IC kan gebruikt worden om via SPI of I²C het aantal IO-pinnen uit te breiden met 8.

![Blokschema van een MCP23S09 IO-expander.](./images/schema.png)

Met volgende code:

```python
from machine import Pin, SoftSPI
from time import sleep

sckPIN = Pin(5)
misoPIN = Pin(19)
mosiPIN = Pin(18)

spi = SoftSPI(sck=sckPIN, mosi=mosiPIN, miso=misoPIN, baudrate=400000)           # Create SPI peripheral 0 at frequency of 400kHz.
                                        # Depending on the use case, extra parameters may be required
                                        # to select the bus characteristics and/or pins to use.
cs1 = Pin(17, mode=Pin.OUT, value=1)      # Create chip-select on pin 17 LEDS.
cs2 = Pin(16, mode=Pin.OUT, value=1)      # Create chip-select on pin 16 Switchen.

cs1(0)
spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x05") #selectie IOCON register
spi.write(b"\x20") #data voor IOCON register
cs1(1)

sleep(0.01)

cs1(0)
spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x00") #selectie IODIR register
spi.write(b"\x00") #data IODIR register (allemaal outputs)
cs1(1)

sleep(0.01)

cs1(0)
spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x09") #selectie GPIO register
spi.write(b"\xAA") #data GPIO register (schrijven van output data) Leds werken via Pullup, dus 0 = oplichten
cs1(1)
for value in range(256):
    cs1(0)
    spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
    spi.write(b"\x09") #selectie GPIO register
    spi.write(bytes([value]))
    cs1(1)
    sleep(0.05)


#vanaf hier de configuratie van de drukknoppen
cs2(0)
spi.write(b"\x40") ##adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x05") #selectie IOCON register
spi.write(b"\x20") #data voor IOCON register
cs2(1)

sleep(0.01)

cs2(0)
spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x00") #selectie IODIR register
spi.write(b"\xFF") #Data IODIR register (het zijn allemaal inputs)
cs2(1)

sleep(0.01)

cs2(0)
spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x06") #selectie GPPU register (om pullup R op de pinnen in te schakelen)
spi.write(b"\xFF") #Data IODIR register (het zijn allemaal inputs)
cs2(1)

sleep(0.01)

cs2(0)
spi.write(b"\x40") #adres van de MCP23S09 SPI device (schrijfmodus)
spi.write(b"\x01") #selectie IPOL register (of een ingang invers of niet wordt gelezen)
spi.write(b"\xFF") #Data IPOL register (alle ingangen worden invers gelezen)
cs2(1)

sleep(0.01)

while True:
    cs2(0)
    spi.write(b"\x41") #adres van de MCP23S09 SPI device (LEESmodus)
    spi.write(b"\x09") #selectie GPIO register
    lees = spi.read(1) #lezen van 1 byte
    cs2(1)
    #print(lees)
    print("GPIO Status: {:08b}".format(lees[0]))
    sleep(0.1)
    



```

## Opdrachten:

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht1: ESP32 als SPI Master en een 8bit GPIO slave.
<ul style="color: white;">
<li>Voor een ontwerp met een ESP32 feather van Adafruit heeft men te weinig uitgangen en wil men deze uitbreiden met een MCP23S09.</li>
<li>Bouw een schema met de ESP32 feather van Adafruit, de ESP32 shield en een MCP23S09 waarbij men de toestand van 2 drukknoppen op de shield weergeeft op 2 leds die aangesloten zijn op de IO-expander.</li>
<li>Sluit 2 rode leds aan met een voorschakelweerstand. Zorg dat de stroom door de leds niet groter wordt dan 5mA. Bereken zelf de voorschakelweerstand.</li>
<li>Sluit een led aan op GP0 en op GP7.</li>
<li>Gebruik SW1 en SW4 van de ESP32 shield.</li>
<li>Als de drukknop SW1 wordt ingedrukt moet de led op GP0 branden. Als SW1 wordt ingedrukt niet is ingedrukt moet GP0 niet branden.</li>
<li>Als de drukknop SW4 wordt ingedrukt moet de led op GP7 branden. Als SW4 wordt ingedrukt niet is ingedrukt moet GP7 niet branden.</li>
<li>Men gebruikt wel SPI maar de adressen moeten hier ook juist aangesloten zijn. Zowel hardwarematig als softwarematig.</li>
<li>Bouw, programmeer en test</li>
</ul>
</p>
</div>