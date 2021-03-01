# Objekterkennung Bayes

## Bayes Decision Theory
- Priors (a priori)
  - $P(C_k)$
- bedingte Wahrscheinlichkeit
  - $P(x|C_k$)
- posterior
  - $P(C_k|x) = \frac{P(x|C_k)P(C_k)}{P(x)}$
- Entscheide $C_i$ für das $i$, für welches $P(C_i|x)$ maximal
- äq. zu Liklihood Ratio test
  - Entscheide $C_1$, wenn $\frac{P(x|C_1)}{P(x|C_2)} > \frac{P(C_1)}{P(C_2) = \lambda}$

## Objekterkennung - appearance based methods
- Prinzip
  - Modelle aus großen Bildersammlungen lernen
  - sliding Window ansatz mit Skalierungen
  - jedes Fenster klassifizieren
- Aspekte / Designentscheidungen
  - Repräsentation des Objekts
    - globale und lokale Merkmale (z.B. Position und Wavelet Zerlegung)
  - Trainingsdaten
    - positive und negative Beispiele
  - Klassifikation und Lernmethode
    - z.B. naive Bayes Classifier