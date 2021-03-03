# Bildverarbeitung

## Deblurring
- blurry Bild $g$ gegeben ($G$ in Fourier Raum)
- finde nicht blurry Bild $f$
- $F = A^{-1}F

## Probleme
- 1. numerisch instabil
  - sehr kleine Werte im Filter abschneiden
  - Inverser Filter (Komplexe Zahlen, vorallem im Hintergrund)
  - Komplex konjugierter Filter
    - $F = \frac{A^*}{|A|^2}G$
    - $=>$ keine komplexen Zahlen mehr
- 2. Rauschen $f = a(f) + n$
  - beide Filter ungeeignet bei verrauschten Bildern

## Einschrittverfahren Wiener Filter
- $F = \frac{A^*}{|A|^2+R^2}G$
- R ist Verhältnis Rauschen zu Signal 
- keine Komplexen Werte mehr in Rekonstruktion
- R intelligent wählen
  - zu groß -> Tiefpaß
    - $A$ ist Tiefpaß. Bild wurde mit $A$ geblurrt. Beim inversen Anwenden von $A$ werden Kanten verwischt, Rauschen entfernt, grobe Strukturen behalten
  - zu klein
    - $A$ ist Hochpaß. Bild "wurde mit $A$ geblurrt". Beim "inversen" Anwenden von $A$ wird also ein inverser Hochpaß angewandt und Kanten/ grobe Strukturen werden entfernt, Verstärkt rauschen!
  - optimal -> Bandpaß
- Nachteil
  - nur ein Filter für gesamtes Bild, ein Wert für R
  - keine lokalen, spezifischen Veränderungen
- Scale Space Ansatz
  - immer mehr Terme mit Ableitungen höherer Ordnung hinzufügen

## Mehrschrittverfahren / Iterative Methoden
- Idee Energie minimieren (Energiie $\approx$ Intensität in den Pixeln)
- Perona Malik
  - Rauschen verwischen
  - Kanten verstärken
  - konvergiert nicht gegen optimale Lösung -> **Stoppzeit**
- Total Variation
  - Rauschen verwischen
  - Kanten verstärken
  - Rauschen Modell verwendet -> **Distance Penalty**

