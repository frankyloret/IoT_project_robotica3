# Software

Een deel van het programma om de 7-segment display op te laten tellen is afgebeeld in de volgende figuur. Enkel het eerste cijfer 0 staat in het programma. De cijfers 1, 2, 3, 4, 5, 6, 7, 8 en 9 moeten nog aangevuld worden.

```python
from machine import Pin
from time import sleep

SEG_A = Pin(21, Pin.OUT)
SEG_B = Pin(14, Pin.OUT)
SEG_C = Pin(32, Pin.OUT)
SEG_D = Pin(15, Pin.OUT)
SEG_E = Pin(33, Pin.OUT)
SEG_F = Pin(27, Pin.OUT)
SEG_G = Pin(12, Pin.OUT)

while True:
    #code om een 0 te tonen
    SEG_A.value(1)
    SEG_B.value(1)
    SEG_C.value(1)
    SEG_D.value(1)
    SEG_E.value(1)
    SEG_F.value(1)
    SEG_G.value(0)
    sleep(1)
    
    ############## nog alle andere getallen uitwerken
      
```


# Opdracht

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: Een 7-segment display laten optellen:
<ul style="color: white;">
<li>Schrijf een programma die een 7-segment display laat optellen van 0 naar 9. Tussen ieder cijfer plaats je een delay van 0,5 seconde. Herhaal de voorgaande cyclus in een oneindige lus.</li>
<li>Maak gebruik van de ESP32 feather van Adafruit, een 7-segment display (SC56-11EWA), een breadbord, voorschakelweerstanden en de nodige verbindingsdraden.</li>
<li>Teken eerst het schema in Visio</li>
<li>Bouw vervolgens de schakeling</li>
<li>Programmeer het programma en test het</li>
<li>Toon de werking aan de docent</li>
</ul>
</p>
</div>

