# Bilder

## Bildverbesserung
- Ortsraum
  - Pixeloperationen (unabhängig von Nachbarschaft)
  - Filteroperationen 
- Frequenzraum
  - Bildtransformation
    - DFT
    - DCT
  - Manipulation der Transformierten
  - Rücktransformation in Ortsraum

## Anwendungen
- Korrektru von nicht-Linearitäten der Kamera
- Anpassung Helligkeit Kontrast
- Bildnereiche hervorheben, unterdrücken
- Bild ausgleichen

## Kontexte
- Bildhelligkeit ist Mittelwert aller Grauwerte
- Bildkontrast ist Varianz aller Grauwerte

## Pixeloperationen
- Negativ
- Binärisierung / Thresholding
- Fensterung
- Kontrastspreizung
- Dynamikkompression
- Gammakorrektur
- Helligkeit
- Histogrammausgleich
- Differenz
- Mittelung
  - Unterdrückung von unkorreliertem Rauschen

## Filterung
- Ortsraum (convolutions, Filtermasken)
  - Mittelwertfilter (Box Filter)
  - Gaussian (normalisieren!)
  - Ableitungen (1., 2. (Laplacian, LoG))
- Frequenzraum
  - Hochpaß
    - tiefe Freq. abschneiden, scharfe Übergänge deutlicher
    - Mexican Hat
    - Summe $0$ im Ortsraum, positive und negative Werte
  - Tiefpaß
    - hohe Frequenzen abschneiden, blur, weniger Rauschen
    - Gaussglocke
    - Summe $1$ nur positive Werte
  - Bandpaß

## Kompression
- verlustlos vs verlustbehaftet
- JPEG
  - 1. Umwandlung $YC_RC_B$ Farbraum
  - 2. Farb-Subsampling
  - 3. DCT (Discrete Cosine Transform)
  - 4. Quantisierung (Betonung homogener Regionen, für Menschen nicht wahrnehmbare Informationen beseitigen)
  - 5. Kodierung der Koeffizienten
