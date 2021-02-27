# 3D Visualisierung

## 3D Daten
- Messwerte werden im 3D Raum verteilt
- jeder Wert hat 3 Koordinaten $(x, y, z)$
- Werte können gleichmäßig oder ungleichmäßig verteilt werden
- Ein Messwert kann skalar oder höherdimensional sein
- Gewinnung von 3D Daten
  - An beliebigen Positionen $(x, y)$ eines Terrains die Höhe $z$ messen
  - Laserscanning
    - laserstrahl auf Oberfläche projezieren
    - Triangulation
  - Range Images $r(u, v)$
    - Tiefeninformation
    - Pixelinformation als 3D Punkt $(u, v, r(u, v))$
  - medizinische Bilddaten
    - bildgebende Geräte um physikalische Eigenschaften zu messen
      - MRI
      - CT
      - Ultraschall
    - Ergebnis ist Stapel von parallelen, manchmal äquidistanten Slices
      - 2 + 1D Gitter
  - Wetter
    - Wetterparameter werden auf verschiedenen Höhen gemessen und simuliert
    - Zellen einer bestimmten Größe (einige Kilometer) in einem regulären Raster
    - Skalare oder vektorielle Daten

## Triangulation von Punktwolken
- unstrukturierte Punktmenge $s_i = (x_i, y_i, z_i)$ auf Oberfläche $S$
- für einfache Oberfläche (ohne Falten):
  - Punkte können auf eine Ebene projeziert und dann trianguliert werden
    - planare Triangulation
  - 2D Dreiecksnetz wird dann entsprechend den $z_i$ Werten deformiert
- bevorzugte Triangulationen
  - Dreiecksform und Dreieckswinkel
    - idealerweise gleichseitig
    - Knotengrad 6
  - Vorteile
    - Aussehen
    - numerische Stabilität
    - Post Processing
- Voronoi Diagramm
  - Jeder projezierte Punkt hat eine Zelle mit allen Punkten, die näher an ihm sind, als an jedem anderen Punkt
- Delaunay Triangulation
  - man betrachte den Graphen der ("mittel") Punkte im Voronoi Diagramm
  - Ein Dreiecksnetz ist eine Delaunay Triangulation, gdw alle Umkreise aller Dreiecke im Netz leer sind
  - ansonsten Edge Flipping, bis dies der Fall ist
  
## Indirekte Volumenvisualisierung
- 3D Volumen
  - Reguläres 3D Raster
  - Volumenelemente sind Voxel (Gitterpunkte in diesem Gitter) $(i, j, k)$
  - Slice Dicke:
    - Abstand in Slice-Auswahl-Richtung
    - oft größer als Pixelabstände (ansitropische Volumen)
- Nachbarschaft
  - Voxel sind adjazent zu einem Referenzvocel
  - in 2D:
    - Kanten: N4
    - Kanten + Ecken: N8
  - in 3D:
    - Flächen: N6
    - Flächen + Kanten: N18
    - Flächen + Kanten + Ecken: N26
- indirekte Volumenvisualisierung
  - Menge von Volumendaten enthält viele Informationen
    - langsames Rendering
    - verdeckung von hinteren Elementen
  - $\rightarrow$ Nur Teilmenge des Volumens zeigen
    - oberflächenorientiert
  - 2D: Konturliniern
    - Linien der selben Höhe
    - Wert ist entlang der Konturlinien konstant
    - Ausrichtung des Gefälles ist orthogonal zu den Konturlinien
  - 3D: Isoflächen
    - Trennung zwischen verschiedenen Strukturen -> Eingrenzung
    - Visualisierung dieser Eingrenzung -> Erkennung der Strukturen
    - Voxel an Eingrenzung haben gleiche Intensität
    - implizierte Fläche
      - $i(x) = V(x) - \tau = 0$ mit Voxelwert $V(x)$ und Isowert $\tau$ 
      - Aufteilung der Datenmengen in innen $i(x) > 0$ und außen $i(x) < 0$
      - Definition eines Isowerts $\rightarrow$ Thresholding der Daten
- 2D Marching Squares
  - Bildzellen durch 4 umgebende Pixel definiert
  - Pixel werden betrachetenm wenn sie $>=$ des Isowert sind
  - 16 mögliche Kombinationen
  - Beschränkung auf 5 Fäle, wenn Rotation und Invertierungen der Pixel-Status berücksichtigt werden
  - Annahme: Eine Kontur passiert eine Zellengrenze zwischen zwei benachbarten Pixeln -> Generierung einer Kontur, die Zellengrenzen kreuzt
- 3D Marching Cubes
  - Eine Volumenzelle ist durch 8 umgebende Voxel definiert
  - 256 mögliche Kombinationen, 15 Äquivalenzklassen nach Beachtung der Symmetrien
  - thresholding + marching cubes liefert große Polygonmodelle
    - Verbessern der Rendering Performance
      - Culling von geometrie
        - Backface Culling
        - View Frustum Culling
        - Occlusion Culling (Transparenz beachten!)
      - Mesh Reduktion
        - weniger Polygone zu rendern
        - Genauigkeit vs Performanz
- Mesh Glättung
  - Ziel: Gute Visualisierung bereitstellen
    - Artefakte reduzieren
    - Löscher entfernen
  - herausforderung: Volumen erhalten
    - quantitative Informationen könnten benötigt werden
  - Laplasche Glättung
    - Reduzierung hochfrequenter Oberflächeninformation
    - Reduktion vom Krümmungen (deshalb Laplace)

## Direkte Volumenvisualisierung
- indirekt
  - Generierung einer Volumen 
  - Komplexität hängt von der Anzahl der Polygone ab
- direkt
  - Visualisierung ohne Generierung einer Metadarstellung
  - Komplexität hängt von Anzahl Voxel und Auflösung der Anzeigefläche ab

## Modell für Volumenrendering
- Density Emitter Model
  - Man betrachte nur Emission und Absorption
  - Jeder Voxel in Datenmenge ist eine Lichtquelle
  - Das Licht wird schwächer während es durch die Vilumendatenmenge wandert
  - Das Medium ist eine homogene Dichtewolke
- Volume Rendering Gleichung
  - kann man sich eh nicht auswendig merken
- Volume Rendering Pipeline 3Basisoperationen
  - Abtastung (Sampling)
    - Ansammlung von Voxelwerten an bestimmten Orten
    - Position dieser Orte ist durch Abtastdistanz $\Delta s$ festgelegt
    - Shannons Sampling Theorem! (Aliasing)
      - Samplingdistanz $>$ 0.5 $\cdot$ Rasterauflösung
    - interpolieren, wenn zwischen Rasterpositionen
      - nearest Neighbour
      - Trilinnear
      - B-Space
  - Klassifikation und Beleuchtung
    - Berechunbg von Farbwert und Transparenzwert
    - $Q_k$ und $t_j$
    - Berechnen des beleuchteten Anteils
      - Abtastungen als gerichtete Lichtquelle (Shading)
  - Komposition
    - Akkumulation der abgetasteten klassifizierten und beleuchteten Werte
    - numerische Approximation der Volumen Rendering Gleichung
    - $I(s) = I_0 \Pi_{k=0}^{n-1} t_k + \sum_{k = 0}^{n-1}Q(k \cdot \Delta s) \cdot \Delta s\Pi_{j = k+1}^{n-1}t_j$
    - Back to Front Komposition
      - An Abtastposition am Ende des Volumens beginnen
      - in Richtung des Sichtpunktes gehen und dabei Anteile berechnen
    - Front to Back Komposition
      - An Abtastposition am Anfang des Volumens beginnen
      - Richtung Ende gehen und dabei Anteile berechnen
- Wie sollen gemessenene und abgetastete Werte auf optische Eigenschaften abgebildet werden?
  - Transferfunktionen
    - Farbwert $Q$
    - Transparenzwert $t$
    - $tf_i: V \rightarrow O_i$
      - Definitionsbereich Voxelwerte und Wertebereich optische Eingenschaften
  






















