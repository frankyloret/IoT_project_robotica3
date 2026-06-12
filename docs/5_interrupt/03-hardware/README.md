---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Hardware interrupts

Microprocessors kunnen worden ingesteld om specifieke taken uit te voeren wanneer er hardware- gebeurtenissen zich voordoen. Het principe van hardware interrupts is in vorige paragraaf al uitgelegd.
Hierdoor kan de hoofdcode zijn taken uitvoeren, en alleen naar bepaalde subroutines of functies springen als er iets fysieks gebeurt (Bijvoorbeeld een drukknop wordt ingedrukt of een signaalingang verandert van status).

Interrupts of onderbrekingen worden gebruikt om te zorgen voor snelle reactietijden als er iets gebeurt. Het enige echte nadeel van interrupt-systemen is het feit dat de programmeer- en codestructuren complexer zijn.

Het programmeren van hardware-interrupts bestaat uit drie delen, namelijk:
> - Instellen van de pin als ingang;
> - Koppelen van een interrupt aan de ingang, het meegeven van de naam van de methode (ISR) die moet uigevoerd worden samen met wanneer deze moet uitgevoerd worden (interrupt voorwaarde);
> - Als laatste het schrijven van de interruptroutine (ISR).

## Mogelijke pinnen die interrupts ondersteunen

Wij gebruiken de Huzzah32 feather van Adafruit zoals in volgende figuur is weergegeven.

![De digitale IO-pinnen van de Adafruit Huzzah ESP32 feather.](./images/esp.png)
![De digitale IO-pinnen van de Adafruit Huzzah ESP32 feather.](./images/esp32_2.jpg)

Enkel de pinnen met de gele labels, zoals in vorige figuur, kunnen als digitale ingangen gebruikt worden. Behalve pin 12 is niet aan te raden om te gebruiken als ingang omdat deze standaard is voorzien van een pull-down weerstand en deze mag bij het booten (=opstarten) niet beïnvloed worden. Het maximum aantal is dus 20. 

:::tip
Alle pinnen die als ingangen gebruikt kunnen worden, kunnen voorzien worden van een interrupt.
:::

## Code.

```python
from machine import Pin
from time import sleep

sw1 = Pin(39, Pin.IN)
sw2 = Pin(34, Pin.IN)

led1 = Pin(21, Pin.OUT)
led8 = Pin(13, Pin.OUT)

def callback(p):
    print('pin change', p)
    led1.value(not led1.value())
    
sw1.irq(trigger=Pin.IRQ_FALLING, handler=callback)
sw2.irq(trigger=Pin.IRQ_RISING | Pin.IRQ_FALLING, handler=callback)

while True:
  led8.value(not led8.value())
  sleep(3)
```

In de code is te zien dat de ingangen sw1 en sw2 gedeclareerd worden. Led1 en 8 worden dan weer gebruikt als uitgang.

## ISR
De `callback` methode is de *interrupt service routine* en wordt aangeroepen als er een interrupt zich voordoet op de sw1&2 ingangen. Binnen die methode wordt Led8 getoggled en wordt een parameter `p`die wordt meegegeven geprint. Deze bevat de Pin(nr) van de opwekker van de interrupt.

## Koppeling van de Pin-input aan een ISR.

Met het statement `Pin.irq` worden er enkele parameters ingesteld met betrekking tot de interrupt. Met de trigger parameter wordt ingesteld wanneer er een interrupt wordt gegenereerd. Bij sw1 is dat bij een dalende flank op de pin. Dalende flank wil zeggen dat de spannng van 3.3V naar 0V gaat. Bij sw2 is dit op zowel de dalende flank als op de stijgende flank. Met de handler parameter wordt de naam van de ISR-methode (functie) opgegeven.

:::tip
Bepaal zelf wat een dalende flank versus stijgende flank is bij een drukknop met een actief lage werking (pull-up R), teken het schema nog eens van die opstelling!!!
:::

> :bulb: **Opmerking:** Hier worden de twee interrupts verwezen naar dezelfde ISR. Dit is geen noodzaak. Iedere interrupt kan gerust zijn eigen ISR hebben.

## Hoofdloop

In de oneindige hoofdloop staat een eenvoudige routine die duidelijk is. Led8 wordt om de 3 seconden van toestand omgedraaid.

:::warning
Opmerkelijk is dat in de hoofdloop een sleep-commando staat. Nomaal kunnen er dan geen andere instructies worden uitgevoerd. Dit kan hier wel, test dit!!!! De sleep kan blijkbaar hier worden onderbroken door een interrupt. Probeer maar binnen de 3 sleep seconden eens de toetsen sw1 of 2 te activeren.
:::

De activatie parameter kan de volgende waarden aannemen:
> - LOW_LEVEL : Triggeren van de interrupt wanneer de pin laag is.
> - HIGH_LEVEL : Triggeren van de interrupt wanneer de pin hoog is.
> - FALLING : Triggeren van de interrupt bij een dalende flank van de ingang.
> - RISING : Triggeren van de interrupt bij een stijgende flank van de ingang.

