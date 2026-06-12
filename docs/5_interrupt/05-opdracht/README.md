---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Opdracht: Het besturen van een kookvlak van een fornuis.

![Visualisatie van de opdracht.](./images/vb.png)

:::warning
Om dit probleem op te lossen zal er nood zijn aan een globale variabele waarmee in meerdere functies (methoden) zal moeten worden gewerkt.
Een voorbeeld van het gebruik van een globale variabele wordt in volgende code weergegeven
:::

```python
waarde = 0
.....
def methode():
  global waarde
  waarde += 1
  .....
while True:
  methode()
  print(waarde)
```

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: Kookvlak bediening
<ul style="color: white;">
<li>Schrijf een programma die het vermogen van een kookvlak van een fornuis aanstuurt met twee drukknoppen van de ESP32 shield. De stand van het vermogens gaan we visueel voorstellen door de 8 leds op de Nucleo-shield.
</li>
<li>Veronderstel dat je het vermogen van een kookvlak van een fornuis kan verhogen met de drukknop SW1 op de ESP32-shield.</li>
<li>Het vermogen kan je verlagen met de knop SW2 op de shield.</li>
<li>Gebruik voor de drukknoppen twee interrupts</li>
<li>De stand van het vermogen van het kookvlak visualiseer je met de 8 leds op de shield.</li>
<li>Bij start brandt er geen enkele led en staat het kookvlak uit.</li>
<li>Schrijf het programma door gebruik te maken van drie functies, namelijk een functie verhoogVermogen, een functie verlaagVermogen en een functie StuurLeds.</li>
<li>Maak gebruik van een (globale)variabele 'vermogen' die een waarde kan hebben van 0 t.e.m. 8.</li>
<li>Leg uit wat het verschil is tussen een lokale en een globale variabele, en waarom je hier een globale nodig hebt, en waarom dit niet zou lukken met enkel een lokale variabele.</li>
<li>Toon de werking aan de docent</li>
<li>Bespreek de werking van harware en software in het verslag</li>
</ul>
</p>
</div>