---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---


# Programma

```python
from machine import Pin
from time import sleep

BIT_0 = Pin(13, Pin.OUT)
BIT_1 = Pin(27, Pin.OUT)
BIT_2 = Pin(15, Pin.OUT)
BIT_3 = Pin(14, Pin.OUT)


def BCDTeller(pCijfer):
  #vervolledig zelf deze methode
  #om de output bits aan te sturen
  
        
while True:
    for x in range(10):
        BCDTeller(x)
        sleep(0.5)
```

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: 7-segment display aansturen met een BCD naar 7 segment converter.
<ul style="color: white;">
<li>Bouw het schema en laadt de code in de ESP32 feather van Adafruit (pas de functiemethode aan).</li>
<li>Maak gebruik van de ESP32 feather van Adafruit, een 7-segment display (SC56-11EWA), een breadbord, voorschakelweerstanden en de nodige verbindingsdraden.</li>
<li>Teken eerst het schema in Visio</li>
<li>Bouw vervolgens de schakeling</li>
<li>Programmeer het programma en test het</li>
<li>Toon de werking aan de docent</li>
<li>Bespreek de werking van harware en software in het verslag</li>
</ul>
</p>
</div>