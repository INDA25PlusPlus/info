# Uppgift 17 - Allocators

## Läxa
  - Implementera två typer av memory allocators
  - Använd er av något systemnivåspråk, helst C, C++ eller Zig
  - Det går bra att först allokera en region med `malloc`,
    och låta er allocator rå om den regionen
  - Annars kan ni försöka att allokera pages direkt med systemanrop
  - En kul utmaning är att försöka ersätta `malloc`
  - På Linux går det att "overrida" libc-versionen med
    ```
    $ LD_PRELOAD=./din_malloc.so <nåt kommando>
    ```

## Länkar
- [Slab allocator i Linux-kärnan](https://hammertux.github.io/slab-allocator)
- [Buddy allocators från tidigare OS-kurs](https://people.kth.se/~johanmon/ose/assignments/buddy.pdf)
- [Egna allocators i Rust](https://doc.rust-lang.org/1.9.0/book/custom-allocators.html)
