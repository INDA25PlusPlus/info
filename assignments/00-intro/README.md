# Homework 0

Välkommen till ++ gruppen! På fredag kommer vi ha vår första övning, men fram till dess så har ni följande läxa som ska vara färdiga innan övningen kl 15.00.

## Läxa

### Förberedelse
1. Skapa ett github-konto (public github, *inte* kth:s github enterprise), om ni inte redan har ett.
2. Skicka ert github användarnamn till oss på discord så lägger vi till er i github organisationen INDA25PlusPlus.
3. Installera [Rust](https://www.rust-lang.org/tools/install)
4. Installera en utvecklings miljö (tex VSCode + [Rust Analyzer](https://rust-analyzer.github.io/))

### Läsning
- Läs kapitel 1-10 i [rust boken](https://doc.rust-lang.org/book/)

### Lös uppgifter
- Lös följande kattis uppgifter:
    1. [A Different Problem](https://kth.kattis.com/courses/DD2016/plusplus25/assignments/q4npcz/problems/different)
    2. [Avstånd till kanten](https://kth.kattis.com/courses/DD2016/plusplus25/assignments/q4npcz/problems/kth.javap.kant)
    3. [Summera tal](https://kth.kattis.com/courses/DD2016/plusplus25/assignments/q4npcz/problems/kth.javap.sumsort)
	4. Frivillig uppgift: [Cyber-Clara och anmälningslistorna](https://kth.kattis.com/courses/DD2016/plusplus25/assignments/q4npcz/problems/kth.grupdat.anmalningslistorna)

Lösenordet för KTH kattis kursen är "jag_gar_plus_plus".

Skicka in lösningarna till kth kattis och lägg upp lösningarna i ett **privat** gitrepo i GitHub organisationen INDA25PlusPlus med namnet “_[ditt-kth-id]_-hw0”, till exempel: ludviggl-hw0

## Om Rust
I DD1337 kommer vi primärt att använda Rust. Inför nästa veckas läxa är det viktigt att ni har någorlunda koll på grunderna, så använd dessa uppgifter för att bekanta er med språket.

## I/O i Rust och Kattis
Kattis rättar era uppgifter automatisk, er kod ska ge output via standard output (dvs ```print!``` och ```println!```) och ta input vid Standard input.

Att ta input från kattis i Rust kan vara lite förvirrande i början, om ni kör fast kan ni använda kodsnuttarna nedan:

```rust
use std::io;
use std::io::prelude::*;

fn main() {
    let mut buffer = String::new();
    
    // Reads the entirety of standard input into a String
    io::stdin().read_to_string(&mut buffer).unwrap();
    ...
}

```
För att konvertera en String till en lista med numeriska värden:
```rust 
	let nums: Vec<i32> = my_string.split_whitespace().map(|w| w.parse().unwrap()).collect::Vec<i32>();
	let a = nums[0];
	let b = nums[1];

```

För att iterera över rader i inputen i en loop:
```rust
for line in buffer.lines().iter() {
	...
}
```

Kattis har även mer hjälp för att använda rust: https://kth.kattis.com/help/rust.
