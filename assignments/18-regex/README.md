# Uppgift 18 - Reguljära uttryck

## Läxa

Den här veckan ska ni skriva en regex-implementation med stöd för UTF-8.
Det kan vara ett kommandoradsverktyg (som `grep`), eller kanske ett
bibliotek (skriv tester i så fall!). Det ska finnas stöd för de
fyra grundläggande operationerna *kontatenering*, *alternativ* (|),
*upprepning* (\*) och *gruppering* (parenteser). Ni ska avkoda UTF-8
strängar själva (både i uttrycket och strängen som ska matchas) och
alltså inte använda inbyggda funktioner eller bibliotek för detta.
Det går bra att göra läxan i par.
Koden ska ligga i ett repo med namnet `<kth-id>-...-regex`.

Här är ett förslag på tillvägagångssätt,
men det kan finnas andra sätt också.

1. Implementera funktioner för att avkoda
   [UTF-8-strängar](https://en.wikipedia.org/wiki/UTF-8#Description)
   till codepoints och för att flytta fram pekaren.

2. Implementera [Thompsons' construction](https://en.wikipedia.org/wiki/Thompson's_construction)
   för att omvandla ett uttryck till en NFA, t.ex. med hjälp av [rekursiv
   medåkning](https://en.wikipedia.org/wiki/Recursive_descent_parser)
   (BNF-notation för reguljära uttryck finns i övningspresentationen).
   För att konstruera epsilon-closures kan ni använda djupet-först-sökning.

3. Implementera [subset-/powerset construction](https://en.wikipedia.org/wiki/Powerset_construction)
   för att omvandla NFA:n till en DFA.

4. Implementera matchning av strängar.

Det går också att exekvera NFA:n med hjälp av tillståndsvektorer.
Det är valfritt om man vill utöka syntaxen för att hantera t.ex.
`?` (matchar 0-1 ggr.), `+` (matchar 1+ ggr.) etc.

## Länkar
- [Pseudokod för epsilon-closure och epsilon-fri NFA](extra.pdf)
