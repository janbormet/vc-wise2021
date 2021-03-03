# 3D Visualisierung

## 3D Daten
- Messwerte in 3D Raum $(x, y, z)$
- Messwerte skalar oder höherdimensional
- Gewinnung von 3D Daten
  - An Terrainpositionen $(x, y)$ die Höhe $z$ messen
  - Laserscanning
    - Laserstrahl auf Oberfläche projezieren
    - Triangulation
  - Range Images $r(u, v)$
    - Tiefeninformation
    - Pixelinformation als 3D Punkt $(u, c, r(uv)$
  - medizinische Bilddatein
    - 2 + 1D Gitter
  - Wetter

## Triangulation von Punktwolken
- unstrukturierte Punktmenge $s_i = (x_i, y_i, z_i)$ auf Oberfläche $S$
- einfache Oberfläche
  - planare Triangulation
  - 2D Dreiecksnetz mit $z_i$ Werten deformieren
- Dreiecks und Dreieckswinkelform bevorzugt
- Voronoi Diagramm
  - Jeder projezierte Punkt hat eine Zelle mit allen Punkten, die näher an ihm sind, als an jedem andderen projezierten Punkt
- Delaunay Triangulation
  - Voronoi Graphen
  - Dreiecksnetz ist Delaunay Triangulation gdw alle Umkreise aller Dreiecke im Netz leer sind
  - sonst Edge flipping

## Indirekte Volumenvisualisierung
- Volumen dargestellt in Regulärem 3D Raster
  - Voxel sind Volumenelemente
- indirekte Volumenvisualisierung
  - zu viele Informationen, also nur Teilmenge anzeigen
  - 2D Konturlinien
  - 3D Isoflächen
    - Trennung zwischen verschiedenen Konturen
- 2D Marching Squares
- 3D Marching Cubes
  - thresholding + Marching Cubes liefert große Polygonmodelle, Problem Rendering Performance
    - Culling von Geometrie
      - Backface Culling
      - View Frustrum Culling
      - Occlusion Culling (Transparenz!)
    - Mesh Reduktion
      - weniger Polygone
      - Genauigkeits vs. Performance
- Mesh Glättung
  - Artefakte reduzieren
  - Volumen erhalten
  - Laplacesche Glättung (Krümmung reduzieren)

## Direkte Volumenvisualisierugne
- indirekt
  - Generierung einer Volumen Metadarstellung
  - Komplexität hängt von Anzahl Polygone ab
- direkt
  - Visualisierung ohne Volumen Metadarstellung
  - Komplexität hängt von Anzahl Voxel und Auflösung der Anzeigefläche ab

## Volumenrendering Modell
- Density Emitter Model
- Volume Rendering Gleichung
- Volume Rendering Pipeling
  - Sampling (Abtastung)
    - Shannons Sampling Theorem! Samplingdistanz $> 0.5 \cdot$ Rasterauflösung
    - Interpolieren
  - Klassifikation und Beleuchtung
    - Farbwert und Transparenzwert berechnen
  - Komposition
    - Volume Rendering Gleichung numerisch apporximieren mit vorher berechneten Werten
    - Back to Front
      - Am Ende des Volumens beginnen
    - Front to Back
      - Am Anfang des Volumens beginnen