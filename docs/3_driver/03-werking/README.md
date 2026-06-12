---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---


# Werking van de CD4511BE

In de waarheidstabel kan je duidelijk zien welke signalen je aan de ingangen moet leggen om een bepaald getal op de display te tonen. De waarheidstabel is weergegeven in de volgende tabel.

![Vereenvoudigde waarheidstabel van de CD4511BE.](./images/tabel.png)

De CD4511BE heeft nog 3 externe ingangen namelijk, LT, BL en LE.

LT is de afkorting van Lamp Test. Als er 0V aan deze pin wordt aangeboden zullen alle segmenten van het display branden. Dit wordt gebruikt om te testen of alle segmenten werken. Dit is een actief lage ingang en daarom wordt er een invers symbool boven de benaming geplaatst. Wij leggen er 3,3V aan om deze functie te deactiveren.

BL is de afkorting van Blanking. Deze ingang is ook een actief lage ingang. Als er een 0V aan de ingang wordt aangelegd zullen alle segmenten gedoofd worden. Deze functie gaan we niet gebruiken en daarom leggen we er een spanning aan van 3,3V.

LE is de afkorting van Latch Enable en deze ingang dient om de schakeling van het IC te activeren of te deactiveren. Wij willen het IC gebruiken en daarom moet er een 0V signaal aan het IC worden aangesloten.

Voor meer informatie wordt hier verwezen naar de datasheet van het IC (zoek op internet naar PDF).

