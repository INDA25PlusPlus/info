# Uppgift 10 - Machine Learing
Läxa:
1. Implementera ett neuralt nätverk utan ML-biblotek
2. Träna ert NN på MNIST datasetet
3. Förbättra modellen
4. `goto 2`

Arbete med ML är mycket testa och misslyckas, alla metoder funkar inte för alla problem.

Läxan ska pushas till ett repo med namnet ***kth-id*-ml**.

## Om MNIST
MNIST är hello world för ML. Det är ett lätt problem att få resultat på men det finns fortfarande mycket rum att arbeta på en lösning.

Några ställen att få tag i MNIST:
- [MNIST for Rust](https://docs.rs/mnist/latest/mnist/)
- [MNIST for Python](https://pypi.org/project/python-mnist/)
- [Rådata (urpsrungslänk, trasig)](http://yann.lecun.com/exdb/mnist/)
- [Rådata (vår kopia)](https://github.com/INDA25PlusPlus/mnist/)

Det finns hundratals andra MNIST-källor.

### Referens resultat på MNIST
| Resultat | Hur bra är det?|
| -------- | -------- |
| 90% | Förväntat resultat för enkel SGD | 
| 98% | Väldigt bra resultat | 
| 99.7% | Resultat i världsklass |

(Obs! Dessa är resultaten på testdata som modellen inte fått se under sin träning)

## Exempel på förbättringar
* Avtagande learning rate
* Early stopping
* Momentum 
* Convolutional layer
* Dropout layers

## Hur man backpropar
[3Blue1Brown](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi), väldigt bra serie om NN:s, Gradient Descent och MNIST (del 3-4 är en underbar resurs för backpropagation).

### Ekvationer för att få ut gradienter
För ett lager som vid forward propagation tar en vektor X ger ut en output vektor Y och vid backward propagation tar $\frac{dE}{dY}$ och ger ut $\frac{dE}{dX}$.

Obs! I ekvationerna nedan antar att aktiveringsfunktionerna behandlas som separata lager.

#### Dense hidden layers (sans activation)
Error beroende av *vikter* för ett lager:  
$\frac{dE}{dW} = \frac{dE}{dY} * X^T$
där X är input till lagret och $\frac{dE}{dY}$ kommer från det efterföljande lagret. 

Error beroende av *bias* för ett lager:  
$\frac{dE}{dB} = \frac{dE}{dY}$

Error beroende på *input* för lagret:  
$\frac{dE}{dX} = W^T * \frac{dE}{dY}$

Obs! Notera att $\frac{dE}{dX}$ måstye beräknas innan vikterna uppdateras.

### Activation layer 
Ett aktiveringslager med aktiveringsfunktionen $\sigma$.

Error beroende på *input* för aktiveringsfunktionen:  
$\frac{dE}{dX} = \sigma'(\frac{dE}{dY})$

### Ett lager i ett NN (vikter, bias och activation)
Kan representeras som ett lager med endast vikter+bias följt av ett med bara aktiveringsfunktion, väldigt smidigt!

## [Slides](https://docs.google.com/presentation/d/1e7eKdCQiuVJrRPgCUhhxhiDKNht9klhqUGT0JXfwAZg/)
