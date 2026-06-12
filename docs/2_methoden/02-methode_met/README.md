---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---



# Methode met meegeefparameters.

In de volgende code is de werking uitgelegd van een methode met parameters.

```python
from machine import Pin
from time import sleep
#setup : declaratie van de pinnen
SEG_A = Pin(21, Pin.OUT)
SEG_B = Pin(14, Pin.OUT)
SEG_C = Pin(32, Pin.OUT)
SEG_D = Pin(15, Pin.OUT)
SEG_E = Pin(33, Pin.OUT)
SEG_F = Pin(27, Pin.OUT)
SEG_G = Pin(12, Pin.OUT)

def ZevenSegmentDisplatMetParameters(pCijfer):
    #eigen methode met een parameter
    #code om een 0 te tonen
    if pCijfer == 0:
        SEG_A.value(1)
        SEG_B.value(1)
        SEG_C.value(1)
        SEG_D.value(1)
        SEG_E.value(1)
        SEG_F.value(1)
        SEG_G.value(0)
        sleep(1)
    
    ############## enz
#oneindige loop methode 
while True:
    for x in range(??):
        #aanroepen van de eigen methode
        #en het meegegeven van een parameter
        ZevenSegmentDisplayMetParameters(x)
```


In het hoofdprogramma (oneindige loop) wordt een *for-loop* gemaakt die opeenvolgend de getallen 0 tem 9 zal genereren. Dit getal komt in de variabele x te zitten. De eigen methode zal telkens worden aangeroepen waarbij het getal (die in de x-variabele zit) wordt meegegeven. Door dit doorgeefmechanisme wordt de inhoud van x doorgegeven aan de parameter (wat ook een variabele is met de naam pCijfer). x geeft dus zijn waarde door aan pCijfer.  

Binnen de eigen methode zal pCijfer worden geanalyseerd en wordt er gekeken welke waarde er in die variabele zit. Op basis van die waarde zullen de respectievelijke zevensegment pinnen worden aangestuurd. Tussen de haakjes ‘()’ staan er maar één parameter. Dit wil zeggen dat er maar 1 waarde zal worden meegegeven aan die methode die in de methode gebruikt zal worden. Dit kunnen er ook meerdere zijn.

Het tweede grote deel is de loop-routine. Dit is waar er allerlei bewerkingen worden uitgevoerd. In de loop-methode wordt de methode ***ZevenSegmentDisplayMetParameters(x)*** aangeroepen. Bij de aanroep worden de parameters meegegeven. Bij de aanroep wordt er gesprongen naar de methode en wordt deze uitgevoerd.

De methode zal allerlei code uitvoeren en zal in de verwerking de meegegeven parameters gebruiken. Als het einde van de methode bereikt is, zal er teruggegaan worden naar de regel code net na de aanroep van de methode. De code in de loop-methode zal verder worden uitgevoerd.

Na het beëindigen van de for-loop in de oneindige-loop zal de for-loop opnieuw herbeginnen.

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: 7-segment display aansturen met een methode MET parameters
<ul style="color: white;">
<li>Schrijf een programma (met een methode die een parameter bezit om het getal mee te geven) die een 7-segment display laat aftellen van 9 naar 0. Tussen ieder cijfer plaats je een delay van 1 seconde. Herhaal de voorgaande cyclus in een oneindige lus.</li>
<li>Maak gebruik van de ESP32 feather van Adafruit, een 7-segment display (SC56-11EWA), een breadbord, voorschakelweerstanden en de nodige verbindingsdraden.</li>
<li>Teken eerst het schema in Visio</li>
<li>Bouw vervolgens de schakeling</li>
<li>Programmeer het programma en test het</li>
<li>Toon de werking aan de docent</li>
</ul>
</p>
</div>
