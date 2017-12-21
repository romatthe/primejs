# Een woordje uitleg

## Pseudocode

```
 Input: an integer n > 1.
 
 Let A be an array of Boolean values, indexed by integers 2 to n,
 initially all set to true.
 
 for i = 2, 3, 4, ..., not exceeding √n:
   if A[i] is true:
     for j = i2, i2+i, i2+2i, i2+3i, ..., not exceeding n:
       A[j] := false.
 
 Output: all i such that A[i] is true.
```

## Directe interpretatie in JavaScript

Volgende functie is een heel directe inpretatie van bovenstaande pseudocode waar x het getal is waarvoor we willen bepalen of het een priemgetal is

```javascript
function isPrime(x) {
    if (x < 2) {            // We willen enkel positieve getallen, en 0 en 1 zijn geen priemgetallen
        return false;
    }
    else {                  // Hieronder behandelen we alle andere gevallen
        possibleFactors = [];
        factors = [];
        matchingFactors = [];

        // Hier berekenen we alle mogelijke mogelijke factoren voor x
        for (i = 2; i < (x / 2) + 1; i++) {         // We bereknen elke mogelijke factor door te starten met het getal 2. Vervolgens verhogen we het getal telkens met 1. We blijven dit doen zolang dat getal kleiner is dan `(x / 2) + 1`
            possibleFactors.push(i);                // We bewaren deze factoren als een lijst in `possibleFactors`
        }

        // Vervolgens nemen we de factoren en delen we telkens x door de respectievelijke factor
        for (i = 0; i < possibleFactors.length; i++) {  // Hier overlopen we de volledige lijst met factoren, delen 
            factors.push(x / possibleFactors[i]);       // We slaan telkens het resultaat op van x gedeeld door de respectievelijke factor in een lijst genaamd `factors`
        }

        // Checks if the x divided by the possible factors is equal to any of the other possible factors
        // Daarna kijken we of er resultaten in `factors` zijn die gelijk zijn aan een van de factoren
        for (i in possibleFactors) {
            if (zFactors.indexOf(possibleFactors[i]) !== -1) {
                matchingFactors.push(possibleFactors[i]);  // Zoja, dan slaan we die op in de lijst `matchingFactors`
            }
        }

        // Indien we op zijn minst 1 van deze factoren hebben opgeslagen in `matchingFactors` kunnen we besluiten dat x een priemgetal is
        return (matchingFactors.length == 0);
    }
}
```

De bovenstaande voorbeeldimplementatie is niet bijzonder efficient, en de leesbaarheid is eveneens betwistbaar. We kunnen de functie immers terk vereenvoudigen

```javascript
function isPrime(number) {
    if (number < 2) {                   // (1)
        return false;               
    }
    else {                              // (2)
        // Takes all numbers that are half of x and below because they are possible factors
        for (var i = 2; i < number / 2 + 1; i++) {
            if (number % i == 0)
                return false;
        }

    return true;
}
```

1. 0 en 1 zijn geen priemgetallen. We filteren deze er op voorhand uit. Daarnaast behandelen we enkel 
2. Alle andere gevallen handelen we hieronder af

