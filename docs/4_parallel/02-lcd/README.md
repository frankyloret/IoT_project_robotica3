---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Parallel LCD-display

We zullen een 2x16 LCD-karakter display gebruiken dat werkt met de HD44780 parallelle interface
met een voedingsspanning van 3,3V. Er zijn veel vergelijkbare LCD’s te vinden met dezelfde
hardware-configuratie en functionaliteit maar met een voedingsspanning van 5V, bij deze LCD’s komt
een logisch 1 van de IO’s overeen met 5V. Bij onze 1 x2 LCD is alles 3,3V en dus ook het logisch 1
niveau van het LCD.
Het schema en een de code is identiek als er gebruik gemaakt wordt van een 2x20 of 4x20 LCD.

![Een 2x16, een 2x20 en een 4x20 LCD.](./images/lcd1.png)

> **Het volgende moet worden bereikt om het LCD-scherm aan te sluiten:**
>
> - Hardware-integratie: we moeten het LCD-scherm op de juiste IO-pinnen aansluiten.
> - Modulaire codering: aangezien er veel processen moeten worden voltooid, is het zinvol om
LCD-functies in modulaire bestanden te definiëren. Daarvoor gaan we gebruik maken van
een bibliotheek LiquidCrystal die we eerst moeten importeren.
> - Initialisatie van het LCD: een specifieke reeks stuursignalen moet naar de LCD worden
gestuurd om deze te initialiseren.
> - Gegevens uitvoeren: we zullen moeten begrijpen hoe het LCD-scherm controlegegevens
omzet in leesbare tekens.

Het is een display dat we gebruiken heeft 2x16 tekens met een ingebouwde datacontrollerchip (=HD44780) en een geïntegreerde achtergrondverlichting.
Het LCD-scherm heeft 16 aansluitingen, zoals in volgende tabel is weergegeven.

![Aansluiting van het 2x16 karakterdisplay.](./images/tabel.png)


> **De bediening en interface van het LCD wordt als volgt samengevat:**
> - Het display wordt geïnitialiseerd door besturingsinstructies naar de relevante configuratieregisters in het LCD-scherm te sturen. Dit wordt gedaan door RS, R/W en E allemaal laag in te stellen en vervolgens de juiste gegevens via bits DB0-DB7 te verzenden.
> - We zullen het LCD-scherm in een 4-bit-modus gebruiken, wat betekent dat we alleen de laatste 4-bits van de databus (DB4-DB7) gebruiken. Dit betekent dat we het LCD kunnen bedienen met slechts 7 digitale lijnen, in plaats van 11 die nodig zijn voor de 8-bits modus.
> - Nadat elke databyte is verzonden, moet de Enable-bit hoog en laag worden gemaakt. Dit vertelt het LCD dat de gegevens gereed zijn en verwerkt moeten worden.
> - Zodra het LCD-scherm is geïnitialiseerd, kunnen weergavegegevens worden verzonden door de RS-bit in te stellen. Nogmaals, nadat elke byte met weergavegegevens is verzonden, moet de Enable-bit hoog en laag worden gemaakt.

We hebben uiteraard digitale IO-pinnen nodig om aan elk van de LCD-datapinnen aan te sluiten. We hebben 4 digitale uitgangen nodig voor de 4-bits instructies en 3 digitale uitgangen voor de RS-, R/W- en E-besturingsvlaggen te manipuleren.
In volgende tabel zijn de pinnen die we gaan gebruiken om aan het display aan te sluiten weergegeven.

![Aansluiting van het 2x16 karakterdisplay.](./images/tabel2.png)

::: tip
In het algemeen gebruiken we het LCD alleen in de schrijfmodus, dus verbinden we de R/W pin permanent aan de GND.
:::

## Schema

![Hardware schema van de 2x16 LCD.](./images/schema.png)

## Programma

Het programma maakt gebruik van enkele methoden. De naam van een methode verklaart hier en daar wel iets over de werking van die methode. Het is ook mogelijk om al die methoden in een afzonderljk bestand onder te brengen en dit bestand dan te importeren in het hoofdprogramma. Het is dan als het ware een bibliotheek. 

:::warning
De code komt niet overeen met de hardware (zie schema). Pas dus de code op de gepaste wijze aan, of wijzig de hardware opstelling.
:::


```python
import machine
import utime
 
rs = machine.Pin(13,machine.Pin.OUT)
e = machine.Pin(12,machine.Pin.OUT)
d4 = machine.Pin(14,machine.Pin.OUT)
d5 = machine.Pin(27,machine.Pin.OUT)
d6 = machine.Pin(26,machine.Pin.OUT)
d7 = machine.Pin(25,machine.Pin.OUT)
 
def pulseE():
    e.value(1)
    utime.sleep_us(40)
    e.value(0)
    utime.sleep_us(40)


def longDelay(t):
    utime.sleep_ms(t)

def shortDelay(t):
    utime.sleep_us(t)

def send2LCD4(BinNum):
    d4.value((BinNum & 0b00000001) >>0)
    d5.value((BinNum & 0b00000010) >>1)
    d6.value((BinNum & 0b00000100) >>2)
    d7.value((BinNum & 0b00001000) >>3)
    pulseE()
def send2LCD8(BinNum):
    d4.value((BinNum & 0b00010000) >>4)
    d5.value((BinNum & 0b00100000) >>5)
    d6.value((BinNum & 0b01000000) >>6)
    d7.value((BinNum & 0b10000000) >>7)
    pulseE()
    d4.value((BinNum & 0b00000001) >> 0)
    d5.value((BinNum & 0b00000010) >> 1)
    d6.value((BinNum & 0b00000100) >> 2)
    d7.value((BinNum & 0b00001000) >> 3)
    pulseE()

def setUpLCD():
    rs.value(0)
    send2LCD4(0b0011)#8 bit
    send2LCD4(0b0011)#8 bit
    send2LCD4(0b0011)#8 bit
    send2LCD4(0b0010)#4 bit
    send2LCD8(0b00101000)#4 bit,2 lines?,5*8 bots
    send2LCD8(0b00001100)#lcd on, blink off, cursor off.
    send2LCD8(0b00000110)#increment cursor, no display shift
    send2LCD8(0b00000001)#clear screen
    utime.sleep_ms(2)#clear screen needs a long delay

def setCursor(line, pos):
    b = 0
    if line==1:
        b=0
    elif line==2:
        b=40
    returnHome()
    for i in range(0, b+pos):
        moveCursorRight()
    
def returnHome():
    rs.value(0)
    send2LCD8(0b00000010)
    rs.value(1)
    longDelay(2)

def moveCursorRight():
    rs.value(0)
    send2LCD8(0b00010100)
    rs.value(1)

def displayString(row, col, input_string):
    setCursor(row,col)
    for x in input_string:
        send2LCD8(ord(x))
        utime.sleep_ms(100)
 
setUpLCD()
rs.value(1)
for x in 'Hello World!':
    send2LCD8(ord(x))
    utime.sleep_ms(100)

setCursor(1,1)
displayString(2,0,"VIVES Kortrijk")
```

## Realiseer

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: Realiseer het bovenstaand project.
<ul style="color: white;">
<li>Maak gebruik van de ESP32 feather van Adafruit, een 2x16 LCD, een breadbord.</li>

<li>Bouw vervolgens de schakeling</li>
<li>Programmeer het programma en test het</li>
<li>Toon de werking aan de docent</li>
<li>Bespreek de werking van harware en software in het verslag</li>
</ul>
</p>
</div>

