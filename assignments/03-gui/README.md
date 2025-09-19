# Uppgift 3 - Chess GUI

Nu är det dags att sätta era schackbibliotek på prov!
Skapa ett repo under INDA25PlusPlus med namnet *[kth_id]-gui*.

## Bibliotek för grafik
Ert program ska vara grafiskt och köras i skrivbordsmiljö.
För att bygga schackspelet kan ni använda något av följande bibliotek:
* [GGEZ](https://ggez.rs/) (enklast, rekommenderat)
* [Piston](https://www.piston.rs/)
* [Bevy](https://bevyengine.org/)

Det finns exempel kod på GGEZ's hemsida som gör det lätt att komma igång.

## Hur man importerar biblioteket i cargo:

Under `[dependencies]` i Cargo.toml:
```toml
namn_pa_bibliotek = { git = "https://github.com/INDA25PlusPlus/repo" }
```
Här är det viktigt att namnet i vänsterledet matchar det som står i Cargo.toml i bibliotek-repot.


## Fördelning av bibliotek

 | Du       | Biblioteket du ska använda |
 |----------|----------------------------|
 | eahla    | hermanha-chess             |
 | hermanha | jonsh-chess                |
 | jonsh    | julina-chess               |
 | julina   | leben-chess                |
 | leben    | rsoderh-chess              |
 | mblomst  | nhg-chess                  |
 | nhg      | puhl-chess                 |
 | puhl     | rsoderh-chess              |
 | rsoderh  | sofiefu-chess              |
 | sofiefu  | wilmerfh-chess             |
 | wilmerfh | eahla-chess                |

* Om det finns bugg(ar), gör ett (konstruktivt) issue i repot
* Kanske t.o.m. ett pull request om du hittar lösningen själv?
* Saknade specialdrag räknas inte som en bugg
* Dyker det upp större problem, hör av dig så går det att byta bibliotek!
* Om du vet att det saknas dokumentation, fixa det ASAP.

