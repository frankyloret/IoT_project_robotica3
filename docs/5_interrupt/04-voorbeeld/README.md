---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Voorbeeld: Het toggelen van twee leds met twee interrupts

```python
from machine import Pin
from time import sleep

sw1 = Pin(39, Pin.IN)
sw2 = Pin(34, Pin.IN)

led1 = Pin(21, Pin.OUT)
led2 = Pin(14, Pin.OUT)
led8 = Pin(13, Pin.OUT)

def callback_sw1(p):
    print('pin change', p)
    led1.value(not led1.value())
def callback_sw2(p):
    print('pin change', p)
    led2.value(not led2.value())
    
sw1.irq(trigger=Pin.IRQ_FALLING, handler=callback_sw1)
sw2.irq(trigger=Pin.IRQ_RISING, handler=callback_sw2)

while True:
  led8.value(not led8.value())
  sleep(3)
```

Hier worden twee Leds getoggled in twee afzonderlijke ISR van twee afzonderlijke interrupts.

:::info
Bestudeer de code goed en realiseer dit.
:::