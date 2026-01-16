# Uppgift 14 - SIMD

## Läxa

Den här veckan ska ni använda er av SIMD ([Single Instruction Multiple Data](https://en.wikipedia.org/wiki/Single_instruction,_multiple_data))
för att optimera ett program. Ni kan välja att antingen fortsätta jobba på er raytracer, eller att optimera något
annat problem.

1. Lös problemet med och utan SIMD.
2. Använd ett benchmarkingbibliotek för att jämföra lösningarna.
   För att få meningsfulla resultat kan ni testa att kompilera utan optimeringar.
3. Presentera resultatet i er README.
4. Lägg kod och README i ett nytt repo med namnet `kth_id-simd`. Om ni väljer
   att jobba vidare på raytracern, lägg bara upp er README, och dokumentera
   vilka ändringar ni gjort.

## Länkar
* [Dokumentation av Intels SIMD intrinsics](https://www.intel.com/content/www/us/en/docs/intrinsics-guide/index.html#)
* [Beskrivning av syntaxen](http://www.nacad.ufrj.br/online/intel/Documentation/en_US/compiler_c/main_cls/intref_cls/common/intref_overview_naming.htm)
* [ubench](https://github.com/sheredom/ubench.h), benchmarkingbibliotek för C/C++
* [Benchmarking i Rust](https://doc.rust-lang.org/nightly/unstable-book/library-features/test.html)
* [`portable_simd`](https://doc.rust-lang.org/std/simd/struct.Simd.html) i Rust
* [`std::arch::x86_64`](https://doc.rust-lang.org/std/simd/struct.Simd.html)
