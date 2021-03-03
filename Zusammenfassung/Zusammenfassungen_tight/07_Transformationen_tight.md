# Transformationen
## Transformationen in Grafikpipeline
- Modelling Transformations
  - 3d-Objekte im Taum anordnen und positionieren
- Viewing Transformations
  - Betrachterstanddpunkt wählen und positionieren (meist Ursprung, Blick in negative z-Achse)
- Projection Transformation
  - viewing volume projezieren (sichtbarer Ausschnitt der Szene)
- Viewport Transformations
  - in Bildschirmkoordinaten transformieren

![Transformations in der Grafikpipeline](../Bilder_07_Transformations/Auswahl_011.png)

## Affine Abbildungen
- Arten
  - Translation
    - $b$
  - Rotation
  - Skalierung
    - Hauptdiagonale von $A$ mit skalierungswerten füllen
  - Scherung
    - Hauptdiagonale $1$, rest mit Scherungsparametern füllen
- Eigenschaften
  - Geraden auf Geraden
  - beschränkte Objekte bleiben beschränkt
  - Verhältnisse von Längen, Flächen, Volumen bleiben
  - Parallel bleibt parallel
  - $\phi(v) = A(v) + b$
- Jede 3D affine Abbildung lässt sich durch eine 4x4 Matrix ausdrücken (homogene Koords)
$\begin{pmatrix}x' \\ y' \\ z' \\ 1\end{pmatrix} = \begin{pmatrix}a_{11} & a_{12} & a_{13} & b_x \\ a_{11} & a_{22} & a_{23} & b_y \\ a_{31} & a_{32} & a_{33} & b_z \\ 0 & 0 & 0 & 1\end{pmatrix} \cdot \begin{pmatrix} x \\ y \\ z \\ 1 \end{pmatrix}$

## Projektion
- projektive Abbildungen
  - Geraden auf Geraden
  - Schnitte von Geraden bleiben erhalten
  - Flächen auf Flächen
  - Reihenfolge von Punkten auf projektiven Geraden bleiben erhalten
  - Winkel ändern sich
    - Parallelität geht verloren
    - Parallelen schneiden sich in FP
    - Rechtecke auf Vierecke
    - $=>$ keine affinen Abbildungen
- perspektivische Projektion
  - Projektionsstrahlen treffen sich im Ausgangspunkt
  - natürliche Menschenwahrnehmung
  - Abstand zwischen Objekten und Projektionsebene geht ein
  - Längeverhältnisse ändern sich
  - Winkel ändern sich
  - parallele Geraden bleiben nicht parallel
- parallele Projektion
  - weniger Realismus
  - Winkel bleiben
  - parallel bleibt parallel
  - zB Medizin

## 3D Interaktion mit 2D Eingabegeräten
- Ansätze
  - Desktop
  - Multi Window
  - direktes 2D Maus Mapping
  - Manipulatoren