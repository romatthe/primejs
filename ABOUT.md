# Een woordje uitleg

## Pseudocode

Op wikipedia vinden we een stukje pseudocode terug voor de Zeef van Eratosthenes:

https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes

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

Volgende functie is een heel directe inpretatie van bovenstaande pseudocode waar `number` het getal `n` is uit bovenstaande pseudocode.

```javascript
function sieve(number) {
    let numbers = Array(number + 1).fill(true);

    for (i = 2; i <= Math.sqrt(number); i++) {
        if (numbers[i] === true) {
            for (j = i * 2; j < number; j+= i) {
                numbers[j] = false;
            }
        }
    }

    return numbers;
}
```

De functie `sieve` geeft ons een volledige lijst terug van alle mogelijke priemgetallen kleiner of gelijk aan `number`.

Indien we aan de hand van de zeef willen bepalen of ons getal `number` daadwerkelijk een priemgetal is, volstaat het om het volgende toe te voegen.

```javascript
function sieve(number) {
    let numbers = Array(number + 1).fill(true);

    for (i = 2; i <= Math.sqrt(number); i++) {
        if (numbers[i] === true) {
            for (j = i * 2; j < number; j+= i) {
                numbers[j] = false;
            }
        }
    }

    return numbers;
}

function isPrime(number) {
    return sieve[number];
}
```

De functie `isPrime` maakt gebruik van de resulterende zeef die we terugkrijgen van de `sieve` functie, en kijkt vervolgens naar het resultaat geindexeerd op de plaats van de waarde van `number` (overigens het allerlaatste resultaat in de lijst).

Het is uiteraard verleidelijk om een vereenvoudigde versie hiervan te schrijven, bijvoorbeeld:

```javascript
function isPrime(number) {
      if (number < 2) {
        return false;
      }
      else {
        for (var i = 2; i < number / 2 + 1; i++) {
          if (number % i == 0)
            return false;
        }

        return true;
      }
    }
```

Zodra we echter gebruikt maken van `%` (de operator voor het bereken van de rest van een deling in JavaScript), kunnen we niet meer zeggen dat we gebruik aan het maken zijn van de klassieke Zeef van Eratosthenes.

Dit is een klassiek probleem, want het is gemakkelijk om talloze voorbeelden online voor het berekenen van priemgetallen in allerlei programmeertalen en zogezegde implementaties va de Zeef gebruiken deze techniek.

Een interessante paper hierover is bijvoorbeeld: https://www.cs.hmc.edu/~oneill/papers/Sieve-JFP.pdf

Hierin wordt weerlegd dat een klassiek voorbeeld van de Zeef in de programmeertaalH askell eigenlijk helemaal niet correct is.

Een goed voorbeeld in een functionele taal zoals Haskell is het volgende:

```haskell
primes = sieve [2..] 
            where
                sieve (p:xs) = p : sieve (minus xs [p, p+p..])
```

