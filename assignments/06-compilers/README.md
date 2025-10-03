# Uppgift 6 - Kompilatorer

Denna vecka ska ni implementera ett frontend till en egen kompilator. Nedan
finns en lista på vad ni behöver göra.

> 1. Hitta på eller låna ett enkelt programmeringsspråk

Ett krav är att det ska gå att beräkna Fibonacci-tal i språket. Ni kan utgå från
detta för att räkna ut vad för features ert språk behöver, och lägga till andra
features senare om det finns tid. Det är till exempel inte nödvändigt (men en
kul utmaning) att implementera funktionsdefinitioner/-anrop.

> 2. Skriv en grammatik för språket i Backus-Naur-form

En beskrivning av Backus-Naur-form (BNF) finns [här](https://en.wikipedia.org/wiki/Backus%E2%80%93Naur_form). För att testa er
grammatik kan ni använda er av det [här](https://bnfplayground.pauliankline.com/) online-verktyget. Vi kommer dock ha
lite slappare krav på BNF-notationen (ni kommer t.ex. inte behöva specificera hur blanksteg hanteras).
Det går även bra att definiera slutsymboler (tokens) som reguljära uttryck. Grammatiken behöver inte heller
var entydig. En bra referens är [denna](https://cs.wmich.edu/~gupta/teaching/cs4850/sumII06/The%20syntax%20of%20C%20in%20Backus-Naur%20form.htm)
BNF-beskrivning av språket C. Spara grammatiken som _grammar.txt_ i repot.

> 3. Implementera stegen lexical analysis och parsing

Den enklaste metoden för att parsa är [rekursiv medåkning](https://en.wikipedia.org/wiki/Recursive_descent_parser), men det finns
även andra metoder. Det är *inte* tillåtet att använda en så kallad _parser generator_, som t.ex. `yacc`.

> 4. Implementera en funktion för att skriva ut syntaxträdet

Hur ni vill representera trädet i text är frivilligt.
Nedan är ett exempel på hur det kan se ut för ett stycke Python-kod.

```python
if a > 0:
    return a + 1
else:
    return a - 1
```

```
if (if)
  binop (>)
    variable (a)
    number (0)
  return (return)
    binop (+)
      variable (a)
      number (1)
  return (return)
    binop (-)
      variable (a)
      number (1)
```

Ett annat alternativ är att försöka återskapa källkoden (då har ni i princip gjort en enkelt kodformaterare).

Andra saker att tänka på:
* Dokumentera hur programmet används. Efter första veckan vill vi kunna ge det en fil och få ett syntaxträd printat.
* Tveka inte att ställa frågor i gruppchatten.
* Repot ska heta *kth_id-compiler*.

Några användbara resurser:
* [Slides från genomgången](assignments/06-compilers/slides.pdf)
* [Bra bok om kompilatorer](https://www3.nd.edu/~dthain/compilerbook/compilerbook.pdf)
* [Wikipediaartikel om rekursiv medåkning](https://en.wikipedia.org/wiki/Recursive_descent_parser)
