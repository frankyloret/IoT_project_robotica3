---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Voorbeeld seriële communicatie bij de ESP32

In het voorbeeld gaan we tekst versturen via de seriële monitor in Visual code naar de ESP32.
De seriële monitor verstuurt de data en komt terug binnen in de ESP32 via de RX van UART2. 
Deze data wordt doorgestuurd via UART2 waarbij er een teller en tekst aan de data wordt toegevoegd. De teller is een geheel getal. Alle data wordt doorgestuurd via de TX van UART2.


Hardwarmatig om alles te testen wordt de TX van UART2 verbonden met de RX van UART2 zoals in volgende figuur. Omdat de TX verbonden is met de RX komt de verzonden data terug binnen via de RX van UART2.

De binnenkomende data via de RX van UART2 wordt vervolgens terug doorgestuurd naar de seriële monitor die verbonden is met UART0. Bij de data wordt er nog wat tekst en een teller meegestuurd.
De teller is een kommagetal.

## Schema

![Voorbeeld van een seriële communicatie.](./images/schema.png)

## Software

```python
from machine import Pin, UART
from time import sleep
uart1 = UART(2, baudrate=115200, tx=17, rx=16)

led = Pin(13, Pin.OUT)
teller1 = 3
teller2 = 0

while True:
    
    uart1.write(f"{teller1}\r\n")
    sleep(0.1)
    if uart1.any():
        gelezen = uart1.readline()
        #tekst = gelezen.decode('utf-8').strip()
        tekst = gelezen.decode()
        try: 
            teller2=int(tekst)
            teller2 = (teller2 * 2)/100.0
            print ('Teller 1= ',teller1, ' Teller 2= ', teller2)
            teller1 += 1
        except ValueError:
            print("Geen geldig getal:", tekst)
    sleep(1)
    led.value(not led.value())

```

## Testen van het programma

Na het starten van het programma zie je in de seriële monitor iedere seconde een lijn bijkomen.

![Testen van het voorbeeld van de seriële communicatie.](./images/result.png)






