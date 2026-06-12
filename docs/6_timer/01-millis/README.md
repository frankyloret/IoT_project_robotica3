---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# The MicroPython class Timer

De MicroPython-`machine`-module wordt geleverd met een klasse genaamd `Timer` die methoden biedt om periodiek een callback-functie uit te voeren binnen een bepaalde periode of eenmaal na een vooraf gedefinieerde vertraging. Dit is handig voor het plannen van evenementen of het uitvoeren van periodieke taken zonder voortdurend de verstreken tijd te controleren.

Een overzicht van de mogelijkheden van de `Timer` constructor:

## Het maken van een Timer-object

Om een ​​timer-object te maken, hoeft u alleen maar de constructor Timer() aan te roepen en als argument de timer-ID door te geven, als volgt:

```python
my_timer = Timer(id)
```

Vervolgens initialiseert u een timer met behulp van de methode `init()` op het object `Timer()` en geeft u als argument de timermodus, periode en de callback-functie door. Hier is een voorbeeld:


```python
my_timer.init(mode=Timer.PERIODIC, period=1000, callback=timer_callback)
```

Hiermee wordt een periodieke timer geïnitialiseerd die de functie timer_callback elke 1000 milliseconden (1 seconde) uitvoert. U kunt de periodeparameter wijzigen in elke gewenste periode.

In plaats van de callback-functie periodiek aan te roepen, wilt u deze wellicht ook eenmalig uitvoeren na een vooraf gedefinieerde tijd. Daarvoor kunt u de Timer.ONE_SHOT-modus als volgt gebruiken:

```python
my_timer.init(mode=Timer.ONE_SHOT, period=1000, callback=timer_callback)
```

Deze coderegel configureert een timer (my_timer) zodat deze in een one-shot-modus wordt uitgevoerd, waarbij de opgegeven callback-functie (timer_callback) na 1000 milliseconden wordt geactiveerd.

> :bulb: **Opmerking:** Meer info omtrent timers in Micropython is te vinden in de [MicroPython documentation.](https://docs.micropython.org/en/latest/library/machine.Timer.html)

