# Homework 1 - Schackbibliotek

Läxan för följande två veckor är att implementera logiken till ett
schackspel (vems tur det är, hur pjäser får röra sig, schackning,
rockader, promovering, passant, ...). Som referens för reglerna finns t.ex.
[Wikipedia](https://sv.wikipedia.org/wiki/Schackregler). Koden **måste** vara
skriven i Rust. Ni ska implementera detta i form av ett **bibliotek** som ska
kunna användas av vem som helst. Ni ska **inte** skriva ett GUI (i nästa läxa
kommer ni att få skriva en GUI till någon annans biblotek). Men det kan vara
händigt att ha en enkel kommandoradsinterface för att hjälpa till med testning.
Fokusera på att skriva ett bibliotek som är lätt av en av era ++-kamrater
att använda. Se till att ert bibliotek har ett logisk och lättanvänt API,
kommentarer samt tester för att se till att koden fungerar.

## Mål
Vi rekommenderar att ni har en representation av brädet, kan hantera
vanliga drag och tagning av pjäser till nästa fredag.  Ni **ska**
använda er av Cargo och ni **ska** skriva tester till er kod. Lägg koden
i ett publikt gitrepo på github.com i INDA25PlusPlus organisationen,
"INDA25PlusPlus/**_[ditt_kth-id]_**-chess". Det är viktigt att ni gör denna läxa
ordentligt, eftersom att senare läxor kommer att bygga vidare på den.

### Vad är ett biblotek?
Ett biblotek har ingen `main.rs` fil utan använder en `lib.rs` fil
istället. Er kod ska inte vara skriven för att köras själv utan inehålla
`pub` funktioner som kan kallas av någon annan som ska implementera schack
för att hantera själva spel-logiken. Det är viktigt att ni testar er kod,
att skriva automatiserade tester är ett utmärkt sätt att göra det. se
[boken](https://doc.rust-lang.org/book/ch11-00-testing.html)...

## Hur ska API:n se ut?

Det är en del av uppgiften att bestämma vilka funktioner som behövs för att
någon ska kunna använda ert biblotek. Målet är att den som implementerar en GUI
till ert biblotek ska ha nästintill noll schacklogik i sin kod.

Viktigt är att:
- Er README sammanfattar hur ert API ska användas.
- Ert API ska vara så ergonomisk som möjligt, tänk på användaren!


### Tips

- Skriv inte objektorienterat (det blir jobbigt senare). Dvs undvik att använda traits.
- Om ni behöver inspiration spana in [chessprogrammingwiki](https://www.chessprogramming.org/Main_Page)
