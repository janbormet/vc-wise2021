# Bildverarbeitung

## Deblurring
- Man hat ein blurry Bild g
- Annahme: Es gibt ein normales Bild f, sodass (im Fourrier-Raum) $G = A \cdot F$ mit Gaussfilter $A$
- $F = A^{-1}G$
- Problem, Blurring Kernel A kann unendlich klein werden -> numerisches Problem. Rauschen und/oder kleine Fehler in G werden stark verstärkt.

## Problem 1 - Numerische instabilität
- Inverse Fouriertransformation (F/A)
  - Werte im Filter abschneiden
  - Wenn $< 10^{-10}$, dann 0 setzen
- Inverser Filter
  - Bild besteht (speziell im Hintergrund) dann aus komplexen Zahlen
- Komplex Konjugierter Filter
  - $F = \frac{A^*}{|A|^2}G$
  - rekonstruiertes Bild hat jetzt keine komplexen Zahlen mehr

## Problem 2 - Rauschen
 - $g = a(f) + n$
 - Sowohl inverser als auch komplex konjugierter Filter haben Probleme mit Rauschen

## Jacques Hadamard - korrekt gestellte Probleme - Konsequenzen
- korrekt gestellt (Blurring)
  - stabile Algorithmen
  - rauschen wird geglättet
- nicht korrekt gestellt (Deblurring)
  - instabile Algorithmen
  - Rauschen wird verstärkt
- Regularisierung notwendig:
  - Zusätzliche Annahmen hinzufügen
  - Glätte, Infos über das Rauschen

## Einschrittverfahren - Wiener Filter
- Problem 2 (Es gibt immer Rauschen)
  - Regularisierung des Filters im Fourierraum
  - $F = \frac{A^*}{|A|^2 + R^2} G$
  - auch "verschmiertes Bandpassfilter"
  - R ist Verhältnis Rauschen zu Signal
  - Entfernt Rauschen (immernoch etwas Blurring)
  - Keine komplexen Werte in Rekonstruktion
- Parameter $R$ intelligent wählen:
  - zu groß (> Tiefpaß Filter)
    - behält grobe Struktur
    - verwischt Kanten
    - entfernt Rauschen
  - zu klein (> Hochpaß Filter)
    - entfernt grobe Struktur und Kanten
    - verstärkt Rauschen
  - optimal (> Bandpaß Filter)
    - entfernt Rauschen
    - behält grobe Struktur
    - verstärkt Kantenstruktur leicht (deblurring)
  - Bewertung
    - Vorteile
      - Schnell
      - häufig verwendet
      - beliebt
      - leicht zu implementieren
    - Nachteile
      - Nur ein Filter für das gesamte Bild
      - keine lokalen, spezifischen Verbesserungen
      - Ein Wert für R
    - Verbesserungsansätze
      - lokale Verfeinerungen mit mehreren Komponenten
      - iterative Verfeinerung als Mehrschrittverfahren
  - Ansatz mit mehreren Komponenten - Scale Space Ansatz
    - subtrahieren des Laplace Operators
    - Terme mit Ableitungen höherer Ordnugn hinzufügen
  - Rekapitualation:
    - Blurring und Rauschen model kann verwendet werden, um Bilder zu deblurren
    - Deblurring ist instabil
    - Wiener Filter funktioniert im Allgemeinen gut, aber Parameterabschätzung notwendig

## Mehrschrittverfahren / Iterative Methoden
- Sei $E$ die Energie eines Bildes $L$
  - $E(L) = \frac{1}{2} \int_{xy}L^2dxdy$
  - Energie sagt aus, wieviel Intensität in den Pixeln vorhanden ist
  - Minimierung der Energie führt zu einem optimalen Bild (bzgl. definierter Energie)
  - Berechnung durch Variationsableitung oder iterativen Prozess
- Variationsableitung
  - Verallgemeinerung der normalen Ableitung
  - Notation $\delta E(L)$
  - hier: als Blackbox betrachten
  - Wenn $E(L) = \frac{1}{2} \int_{xy}L^2dxdy$
    - $\delta E(L) = L$
    - Minimum $\delta E(L) = 0$
      - $L = 0$ und $E(L) = 0$
  - Wenn $E(L) = \frac{1}{2} \int_{xy}L_x^2 + L_y^2dxdy$
    - $\delta E(L) = -(L_{xx} + L_{yy}) = - \Delta L$
    - Minimum weniger trivial, Überführung in partielle Differentialgleichung
      - $L_t = -\delta E(L)$
    - Gegen Lösung iterieren (Heat Equation)
      - $L_t = \Delta L$
  - Auf diese Wiese können nicht so gut Interessante Bilder generiert werden. Daher andere Energien:
- Perona Malik
  - Rauschen verwischen
  - Kanten verstärken 
  - Smart Energy Term + **Stoppzeit**
- Total Variation
  - Rauschen verwischen
  - Kanter verstärken
  - Smart Energy Term + **Distance Penalty**
- Rekapitulation
  - Diffusion kann **lokal anpassbar** an Bildstruktur gemacht werden
  - non-linear PDEs beinhalten lokale Bildsableitungen und sind nicht analytisch lösbar
  - iterative Prozesse sind notwenidg, da sie graduelle Änderungen des Bildes in jedem Iterationsschritt zeigen
  - Einfachste Gleichung: Perona Malik. Diffusion $c$ ist hier Funktiton der lokalen Kantenstärke
  - hohe Gradientenstärken verhindert Blurring lokal -> Kantenerhaltendes Glätten -> Deblurring und verstärkten Kanten bei Kanten $>k$ und Blurring (Rauschen) bei kleineren Kanten
  - Stoppzeit notwendig, da zu viele Iterationen zu schlechtem Ergebnis führen
- Im vergleich dazu Total Variation:
  - kein Blurring, Stufenkanten bevorzugt
  - Denoising
  - keine Stopzeit benötigt (konvergiert zur optimalen Lösung)
  - $\lambda$ vom Rauschen abhängiger Parameter
  - sehr kompliziert
  - mathematisch sehr interessant

## Zusammenfassung
- Mit Blurring und Rauschen Modell kann man versuchen Bilder zu deblurren. Deblurring instabil
- Wiener Filter funktioniert gut, benötigt aber Parameterabschätzung
- Deblurring auch als iterativer Prozess möglich -> immer mehr Terme hinzufügen, Ergebnis verfeinern
- Energiemininmierungsmethoden benötigen korrekt definierte Energie für das Bild
- Lösungen mithilfe von PDEs. Diffusion lokal anpassbar an Bildstruktur
- Perona Malik verwendet lokale Kantenstärken. Deblurring für starke Kanten, Blurring für Rauschen
- Rauschen beschränkt klug gestaltete PDEs, die zu einem optimalen Bild führen