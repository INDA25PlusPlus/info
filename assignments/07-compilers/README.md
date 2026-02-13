# Uppgift 7 - Kompilatorer del två

Denna vecka ska ni implementera ett backend till er kompilator. Ni kan
välja att generera assembly direkt, någon form av IR (t.ex. QBE eller LLVM IR),
eller transpilera till ett annat språk.

Det går bra att generera kod direkt från ert syntaxträd. Det är inte nödvändigt
att göra ett eget IR eller lägga till optimeringar, men gör gärna det om ni vill.

Ni ska även skriva ett program som beräknar Fibonacci-tal i språket som
kompileras av er kompilator. Programmet ska gå att kompilera och köra på något
sätt. Ge instruktioner i ert repo.

Några användbara resurser:
* [Slides från genomgången](slides.pdf)
* [Bra bok om kompilatorer](https://www3.nd.edu/~dthain/compilerbook/compilerbook.pdf)
* [QBE](https://c9x.me/compile/)
* [LLVM IR Reference](https://llvm.org/docs/LangRef.html) (Komplett referens, lite väl tungt)
* [Introduktion till LLVM IR](https://mcyoung.xyz/2023/08/01/llvm-ir/) (Rekommenderas för LLVM)
