# Uppgift 11 - Komplexitet och Korrekthet

## 1 Induktion
Använd induktion för att bevisa dessa formler:

![](https://i.imgur.com/pGImUwO.png)

![](https://i.imgur.com/RdMxyax.png)

## 2 Iterativ korrekhet

Bevisa korrekthet för denna iterativa funktion och ange dess tidskomplexitet:

```c
double expIterative(double x, int n) {
    double res = 1.0;

    for (int i = 0; i < n; i++) {
        res *= x;
    }
    return res;
}
```

## 3 Rekursiv korrekhet
Bevisa korrekthet för denna rekursiva funktion och ange dess tidskomplexitet:

```c
double expRecursive(double x, int n) {
    if (n <= 4) {
        return expIterative(x, n);
    }

    return expRecursive(x, n / 2) * expRecursive(x, (n + 1) / 2);
}
```

## Inlämning

Döp repot till *kth-id*-complexity. Godkända inlämningsformat:
* Latex-kod
* Typst-kod
* PDF
* Markdown
* Plain text (om den är läsbar)

## Material
* [Slinginvarianter, video](https://www.youtube.com/watch?v=vVdDyI1PIUU)
* [Slinginvarianter](https://yourbasic.org/algorithms/loop-invariants-explained/)
* [Mästarsatsen, video](https://www.youtube.com/watch?v=sorlJiiWDRA)
* [Mästarsatsen](https://yourbasic.org/algorithms/time-complexity-recursive-functions/)

