---
mathjax:
  presets: '\def\lr#1#2#3{\left#1#2\right#3}'
---

# Methode met teruggeef waarde

## Uitleg over de `return`-functie in Python

In Python wordt de `return`-instructie gebruikt binnen een functie om een waarde terug te sturen naar de plek waar de functie werd aangeroepen. Dit maakt functies flexibel en herbruikbaar, omdat je het resultaat van de functie kunt gebruiken in andere delen van je code.

Een functie kan:
- **Eén waarde** teruggeven.
- **Meerdere waarden** teruggeven als een tuple.
- **Niets teruggeven**, in welk geval de standaardwaarde `None` wordt teruggestuurd.

---

## Basisvoorbeeld van een `return`-functie

Hieronder staat een voorbeeld van een eenvoudige functie die twee getallen optelt en het resultaat teruggeeft:

```python
def som(a, b):
    # Bereken de som van twee getallen
    return a + b
```
Hierbij zijn a en b twee parameters die de functie nodig heeft om zijn taak uit te voeren.

De return-instructie wordt gebruikt om het resultaat terug te sturen naar de plek waar de functie is aangeroepen.

## Aanroepen en opvangen van de returnwaarde

De waarde die door `return` wordt teruggestuurd, kan worden opgevangen en gebruikt in andere delen van je programma. Hier is een voorbeeld:

```python
# Aanroep van de functie en opvangen van de returnwaarde
resultaat = som(5, 3)

# Print de returnwaarde
print("De som is:", resultaat)
```

Bij het aanroepen van de functie wordt de returnwaarde opgevangen in een variabele, hier de variabele `resultaat`.

