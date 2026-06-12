---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Timer Interrupts met de ESP32

## Knipperled met een Timer – MicroPython

In dit voorbeeld leert u hoe u een LED kunt laten knipperen met behulp van een timer. Dit zal u helpen begrijpen hoe periodieke timers werken.

### Circuit Diagram
We zullen een LED laten knipperen die is aangesloten op GPIO 13. Sluit dus een LED aan op de ESP32 op die GPIO. U kunt de volgende diagrammen als referentie gebruiken.

![Schema van een knipperende led.](./images/fc.png)
![Schema van een knipperende led.](./images/schema.png)

### Code
In het volgende voorbeeld wordt de klasse Timer gebruikt om elke halve seconde een LED te laten knipperen. Deze code is compatibel met ESP32- en ESP8266-kaarten.

```python
from machine import Pin, Timer
from time import sleep

# LED pin
led_pin = 13
led = Pin(led_pin, Pin.OUT)

# Callback function for the timer
def toggle_led(timer):
    led.value(not led.value())  # Toggle the LED state (ON/OFF)

# Create a periodic timer
blink_timer = Timer(1)
blink_timer.init(mode=Timer.PERIODIC, period=500, callback=toggle_led)  # Timer repeats every half second

try:
    # Main loop (optional)
    while True:
        print('Main Loop is running')
        sleep(2)
except KeyboardInterrupt:
    # Keyboard interrupt occurred, deinitialize the timer
    blink_timer.deinit()
    print('Timer deinitialized')
    # Turn off the LED
    led.value(0)
```

In deze code, wordt gebruik gemaakt van een timer object met de naam `blink_timer`:

```python
blink_timer = Timer(1)
```

Daarna, wordt de timer geïnitialiseerd met volgende parameters:

```python
blink_timer.init(mode=Timer.PERIODIC, period=500, callback=toggle_led)
```

Dit betekent dat het timer-object (blink_timer) een methode (functie) iedere 500 milliseconden zal aanroepen. De naam van die methode is `toggle_led` en dit zal eindeloos gebeuren, tenzij het programma wordt gestopt. 

De `toggle_led` functie, zoals de naam doet vermoeden, zal een LED laten knipperen (omswitchen van de toestand (aan/uit)).

```python
# Callback function for the timer
def toggle_led(timer):
    led.value(not led.value())  # Toggle the LED state (ON/OFF)
```

De timer-callback-functies moeten één argument hebben dat automatisch wordt doorgegeven door het Timer-object wanneer de gebeurtenis wordt geactiveerd.

Met timers kun je ook andere taken op de hoofdlus laten draaien, zonder dat ze elkaar hinderen. In ons geval drukken we in de hoofdlus bijvoorbeeld elke twee seconden een bericht af.

```python
while True:
    print('Main Loop is running')
    sleep(2)
```

When the user stops the program (KeyboardInterrupt), we deinitialize the timer using the deinit() method and turn off the LED.

```python
except KeyboardInterrupt:
    # Keyboard interrupt occurred, deinitialize the timer
    blink_timer.deinit()
    print('Timer deinitialized')
    # Turn off the LED
    led_pin.value(0)
```

Test de code

## Blinking Multiple LEDs op verschillende Frequenties

Na het testen van het vorige voorbeeld is het gemakkelijk te begrijpen dat als u meerdere timers maakt, u meerdere taken op verschillende frequenties kunt uitvoeren. In dit voorbeeld knipperen we twee verschillende LED's. De ene knippert elke halve seconde en de andere elke twee seconden.

### Circuit Diagram
Sluit twee LED's aan op de ESP32 (om onderscheid te maken tussen de verschillende LED's gebruiken we verschillende kleuren):

> - Red LED: GPIO 13 knippert iedere halve seconde.
> - Yellow LED: GPIO 12 knippert iedere twee seconden.

De bedrading kan als volgt uitgevoerd worden:

![Schema met twee Leds.](./images/begin.png)

### Code
De volgende code gebruikt timers om twee verschillende LED's op verschillende frequenties te laten knipperen. 

```python
from machine import Pin, Timer
from time import sleep

# LEDs
red_led_pin = 12
red_led = Pin(red_led_pin, Pin.OUT)
yellow_led_pin = 13
yellow_led = Pin(yellow_led_pin, Pin.OUT)

# Callback function for the red timer
def toggle_red_led(timer):
    red_led.value(not red_led.value())  # Toggle the LED state (ON/OFF)
    print('red LED is: ', red_led.value())

# Callback function for the yellow timer
def toggle_yellow_led(timer):
    yellow_led.value(not yellow_led.value())  # Toggle the LED state (ON/OFF)
    print('yellow LED is: ', yellow_led.value())

# Create periodic timers
red_timer = Timer(1)
yellow_timer = Timer(2)

# Init the timers
red_timer.init(mode=Timer.PERIODIC, period=500, callback=toggle_red_led)  # Timer repeats every 0.5 second
yellow_timer.init(mode=Timer.PERIODIC, period=2000, callback=toggle_yellow_led)  # Timer repeats every 2 seconds

try:
    # Main loop (optional)
    while True:
        print('Main Loop is running')
        sleep(2)
        
except KeyboardInterrupt:
    # Keyboard interrupt occurred, deinitialize the timers
    red_timer.deinit()
    yellow_timer.deinit()
    print('Timers deinitialized')
    # Turn off the LEDs
    yellow_led.value(0)
    red_led.value(0)
```

In deze code, wordt gebruikt gemaakt van twee verschillende timers, voor iedere LED één:

```python
# Create periodic timers
red_timer = Timer(1)
yellow_timer = Timer(2)
```

Dan worden de corresponderende `callback functions` ingesteld met hun verschillende interval-tijden:

```python
# Init the timers
red_timer.init(mode=Timer.PERIODIC, period=500, callback=toggle_red_led)  # Timer repeats every 0.5 second
yellow_timer.init(mode=Timer.PERIODIC, period=2000, callback=toggle_yellow_led)  # Timer repeats every 2 seconds
```

De callback functie toggled gewoon de LED:

```python
# Callback function for the red timer
def toggle_red_led(timer):
    red_led.value(not red_led.value())  # Toggle the LED state (ON/OFF)
    print('red LED is: ', red_led.value())

# Callback function for the yellow timer
def toggle_yellow_led(timer):
    yellow_led.value(not yellow_led.value())  # Toggle the LED state (ON/OFF)
    print('yellow LED is: ', yellow_led.value())
```

Test de code.

## Opdracht:

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: Blokgolf met interrupt timers (1kHz)
<ul style="color: white;">
<li>Schrijf een programma die een blokgolfspanning op een uitgang genereert met een frequentie van 1kHz en een duty-cycle van 50%. (maak gebruik van een timer)
</li>
<li>Een tweede blokgolfspanning op een andere uitgang genereert met een frequentie van 100Hz en een duty-cycle van 50%. (maaak gebruik van een tweede timer)
</li>
<li>Knipperled (derde LED gebruiken) maken in de Loop-methode op een periode van 250ms. Hiermee toon je de onafhankelijkheid van de ISR aan tov. de standaard Loop-methode.
</li>
<li>Meet, controlleer en visualiseer beide signalen met een oscilloscoop</li>
<li>Toon de werking aan de docent</li>
<li>Bespreek de werking van harware en software in het verslag</li>
</ul>
</p>
</div>

> :memo: **Note:** In plaats van `period` als parameter te gebruiken kan er ook gebruikt gemaakt worden van `freq` als parameter waarbij de waarde dan de frequentie is (hoeveel keer per seconde de timer afloopt).




