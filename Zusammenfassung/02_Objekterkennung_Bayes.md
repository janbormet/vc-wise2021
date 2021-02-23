# Objekterkennung und Bayes

## Anwendung
- Nummernschilder erkennen
- Überwachung
- Gesichtserkennung
- Flughafensicherheit
- Medizinische Bildverarbeitung
- autonomes Fahren

## Computer Vision
- Lochkamera Modell (Camera Obscura)
- "umgekehrte Grafik"
- Objekterkennung (Wie machen das Menschen?)

## Intuitionen Objekterkennung
- wichtige Komponenten der Beschreibuung
  - lokale Beschreibung / Merkmale
    - Augen, Mund, Nase
  - globale Anordnung der Merkmale
    - relative Position und Größe
- schnelle Generierung von guten Hypothesen
- Segmentierung der Bildbereiche
- Szenenkontext

## Bayes Decision Theroy
- Beispiel Buchstabenerkennung a und b
- Klassifizierungsproblem
- Priors (a priori Wahrscheinlichkeit)
  - $P(a)$
  - $P(b)$
  - $P(C_k)$
- bedingte Wahrscheinlichkeit
  - Merkmalsvektor x
  - $P(x | C_k)$
- posterior
  - $P(C_k|x) = \frac{P(x|C_k) P(C_k)}{P(x)} = \frac{P(x|C_k) P(C_k)}{\sum_j P(x|C_j)P(X_j)}$
  - $\text{Posterior} = \frac{\text{Likelihood} \cdot \text{Prior}}{\text{Normalization Factor}}$
- Ziel
  - Wahrscheinlichkeit der Fehlklassifikation minimieren
  - Entscheidungsregel finden
  - Entscheide $C_1$, wenn $P(C_1|x) > P(C_2|x)$
  - äq. zu Likelihood Ratio Test:
  - $\frac{P(x|C_1)}{P(x|C_2)} > \frac{P(C_1)}{P(C_2)} = \lambda$
- Verallgemeinerung
  - Entscheide $C_k$ ist Klasse k, wann immer diese die größte posteriori Wahrscheinlichkeit hat
  - $P(C_k|x)$

## Gesichtsdetektion
### Appearance-Based Methods
- Prinzip:
  - Erscheinungsmodelle aus großen Sammlungen von Bildern lernen
  - Sliding window Ansatz (Skalierungen nicht vergessen)
  - Jedes Fenster als "Gesicht" Oder "kein Gesicht" klassifizieren
- Aspekte:
  - Repräsentation des Objektes
    - lokale Merkmale
    - globale Anordnung merkmale
  - Trainingsdaten
    - positive Beispiele
    - negative Beispiele
  - Klassifikation und Lernmethode
- Beispiele Gesichtsdetektor Schneidermann Kanade 
  - Repräsentation der Objekte
    - Waveletzerlegung
    - lokale Merkmale: wavelet Koeffizienten - Frequenz der Gesichtsmerkmale ("Kanten"), Auge Mund
    - globale Anordnung: absolute Position der Frequenzen im Bild
  - Trainingsdaten
    - positive Beispiele möglichst vielfältig, auf 19x19 normalisiert, virtuelle Beispiele erstellt
    - negative Bilder
      - beliebige Bilder die kein Gesicht enthalten, Teilbilder von großen Bildern
  - Klassifikation und Lernmethode
    - Naive Bayes Classifiers
    - $P(C_k|x_1, x_2, ..., x_d) = \Pi_{i=1}^{d}\frac{P(x_i|C_k)}{P(x_i)}P(C_k)$
    - Merkmale $x_i$ sind wavelet Koeffizienten an bestimmten Positionen $(u, v)$
    - 2 Klasse $C_1 = \text{Gesichter }$, $C_2 = \text{alles andere}$

## Erkennungsarten
- Gesichtserkennung zählt zu den biometrischen Verfahren
- Verifikation
- Identifikation