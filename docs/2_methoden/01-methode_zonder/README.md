---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Methoden

Methoden worden voornamelijk gebruikt als je in een programma steeds dezelfde stukken code herhaalt, om complexe code te vereenvoudigen of als je stukken van je programma wil opdelen in verschillende onderdelen.
Met een goede kennis en verstandig gebruik van functies kan je programma’s sneller en leesbaarder maken en dat maakt van je een goede programmeur.
Een methode krijgt steeds een naam en in python wordt die vooraf gegaan door het woord ***def***. Na de naam komen dan ronde haakjes waartussen al of niet gebruik gemaakt wordt van parameters.

:::warning
Het dient hier heel duidelijk vermeld te worden dat ieder eigen geschreven methode voor de executor moet gekend zijn, dit wil zeggen dat de methode best voor de oneindige loop wordt geschreven. De methode kan zich ook in een afzonderlijk bestand bevinden, dan horen de nodige verwijzingen te gebeuren.
:::

```python

EigenMethode() #declacratie van de eigen methode
  #hier komt de eigen methode

while True:#hier staat de oneindige lus
  #hier komt de code van de oneindige lus 
  #waar de EigenMethode wordt aangeroepen
```


Methoden kan men indelen in drie groepen, namelijk:
- Een methode zonder parameters;
- Een methode die iets uitvoert afhankelijk van één of meerdere variabelen die wordt meegegeven aan die methode;
- Een functiemethode die iets uitvoert afhankelijk van een meegegeven variabele maar die ook een resultaat teruggeeft.

# Methode zonder parameters.

In de volgende voorbeeld wordt een methode gemaakt die één keer alle getallen op het zeven segment display toont en daarna stopt. Door die methode telkens in de oneindige loop aan te roepen zal het tellen steeds opnieuw starten.

```python
from machine import Pin
from time import sleep
#declaratie van de gebruikte pinnen (setup)
SEG_A = Pin(21, Pin.OUT)
SEG_B = Pin(14, Pin.OUT)
SEG_C = Pin(32, Pin.OUT)
SEG_D = Pin(15, Pin.OUT)
SEG_E = Pin(33, Pin.OUT)
SEG_F = Pin(27, Pin.OUT)
SEG_G = Pin(12, Pin.OUT)

def ZevenSegmentDisplayZonderParameters(): 
    #eigen methode met naam en geen parameters

    #code om een 0 te tonen
    SEG_A.value(1)
    SEG_B.value(1)
    SEG_C.value(1)
    SEG_D.value(1)
    SEG_E.value(1)
    SEG_F.value(1)
    SEG_G.value(0)
    sleep(1)
    
    ############## enz...
 
while True: #oneindige loop
    #aanroepen van de eigen methode met zijn naam
    ZevenSegmentDisplayZonderParameters() 
```


De eigen methode krijgt hier de naam (is nu een zeer lange naam, dat hoeft niet, maar zorg steeds voor een duidelijke naam van de methode, Wat doet ze?) **ZevenSegmentDisplayZonderParameters**. Let op de methode staat in de code eerst geschreven, verder in de oneindige loop zal die methode worden aangeroepen, waar nodig. Tussen de haakjes ‘()’ staat er niets geschreven. Dit wil zeggen dat er geen parameters meegegeven worden aan de methode.

Het tweede grote deel is de loop-methode. Dit is waar de werking van het hoofdprogramma begint waar er allerlei bewerkingen worden uitgevoerd. In het hoofdprogramma wordt de methode **ZevenSegmentDisplayZonderParameters** aangeroepen. Bij de aanroep wordt er gesprongen naar de methode en wordt deze uitgevoerd.

De methode zal allerlei code uitvoeren. Als het einde van de methode bereikt is zal er teruggegaan worden naar de regel code, net na de aanroep van de methode in het hoofdprogramma. De code in het hoofdprogramma zal verder worden uitgevoerd.

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: 7-segment display aansturen met een methode zonder parameters
<ul style="color: white;">
<li>Schrijf een programma (met een methode) die een 7-segment display laat optellen van 0 naar 9. Tussen ieder cijfer plaats je een delay van 1 seconde. Herhaal de voorgaande cyclus in een oneindige lus.</li>
<li>Maak gebruik van de ESP32 feather van Adafruit, een 7-segment display (SC56-11EWA), een breadbord, voorschakelweerstanden en de nodige verbindingsdraden.</li>
<li>Teken eerst het schema in Visio</li>
<li>Bouw vervolgens de schakeling</li>
<li>Programmeer het programma en test het</li>
<li>Toon de werking aan de docent</li>
</ul>
</p>
</div>


