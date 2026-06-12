# SC56-11EWA

In deze bundel gaan we de 7-segment display met referentie SC56-11EWA (KingBright) gebruiken. Hoe de display er uit ziet is weergegeven in de volgende figuur.

![KingBright: SC56-11EWA: 14.22 mm (0.56 inch) Single Digit Numeric Display.](./images/disp.png)
![KingBright: SC56-11EWA: 14.22 mm (0.56 inch) Single Digit Numeric Display.](./images/SC56-11EWA.jpg)

![KingBright: SC56-11EWA: 14.22 mm (0.56 inch) Single Digit Numeric Display.](./images/layout.png)

De pinnummering begint bij de meeste IC’s (=Integrated Circuits) links boven. Bekijk deze component in vorige figuur heel goed en herken de pinnummering. In het schema met LED-dioden kan worden nagegaan welk LED-segment de pinnummering overeenkomt.

We weten dat een 7-segment display bestaat uit 7 langwerpige leds die de 7 segmenten vormen. Bij dit display is er nog 1 segment of leds die gebruikt kunnen worden als punt of komma (DP = decimale punt).

Wij willen de 7-segment display aansturen met de ESP32 feather van Adafruit. We weten dat we de uitgangen van de microcontroller hoog kunnen maken waarbij de spanning gelijk wordt aan 3,3V. Als we een led-segment willen doen oplichten van de SC56-11EWA dan moeten we aan de anode van de led een spanning leggen van 2V en dan verbruikt het segment een stroom van 10mA. Deze waarde haal je uit de datasheet van het display. Zie volgende figuur. Bij andere 7-segment displays kunnen dit andere waarden zijn en zoek je die best op in de datasheet.

![Elektrische en optische gegevens van de SC56-11EWA bij een omgevingstemperatuur van 25°C.](./images/datasheet.png)

Als deze spanning gelijk is aan 2V dan vloeit er een stroom van 20mA (2). De uitgangen van ESP32 feather van Adafruit kunnen gerust deze stroom leveren zonder beschadiging op te lopen. Natuurlijk is de spanning van de uitgangen van de microcontroller veel te hoog (=3,3V).
Om ervoor te zorgen dat de spanning maar 2V op de pin van een led-segment zal zijn moet er gebruik gemaakt worden van een voorschakelweerstand. Het schema om het led-segment A van de microcontroller aan te sturen is weergegeven in de volgende figuur. Wat nog ontbreekt is de waarde van de
voorschakelweerstand R1.

![Schema om segment A van het display aan te sturen met een microcontroller.](./images/schema1.png)

<div style="background-color:darkgreen; text-align:left; vertical-align:left; padding:15px;">
<p style="color:lightgreen; margin:10px">
Opdracht: Bereken de waarde van weerstand R1. Kies dan een weerstand uit de E12-reeks die je praktisch gaat gebruiken.
</p>
</div>


# Schema

![Schema om de SC56-11EWA aan te sturen met de ESP32 feather van Adafruit](./images/schema2.png)



