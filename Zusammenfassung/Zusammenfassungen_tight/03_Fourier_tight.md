# Fourier
## Polarkoordinaten
- $P(r| \varphi)$
- $x = r cos(\varphi)$
- $y = r sin(\varphi)$
- $z = |z| e^{i\varphi}$
- $e^{i\varphi} = cos(\varphi) + isin(\varphi)$

## Dirichlet Bedingungen
- Anzahl unstetigkeiten innerhalb einer Periode endlich
- Anzahl max und min innerhalb einer Periode endlich
- in jeder Periode integrierbar

$=>$ Funktion lässt sich als Summe von $sin$ und $cos$ Termen darstellen
time
## Fourier Reihe
- $f(x)$ eine $2\pi$ periodische Funktion, welche Dirichlet erfüllt
- $f(x) = \sum_{n = 0}^{\infty}(a_n cos(nx) + b_nsin(nx))$
- Berechnung der Koeffizienten
  - $a_0 = \frac{1}{2\pi}\int_{-\pi}^{\pi}f(x)dx$
  - $a_m = \frac{1}{\pi}\int_{-\pi}^{\pi}f(x)cos(mx)dx$ mit $m>0$
  - $b_m = \frac{1}{\pi}\int_{-\pi}^{\pi}f(x)sin(mx)dx$
  - für gerade Funtionen sind alle $b_n = 0$
  - für ungerade Funtionen sind alle $a_n = 0$

## Fouriertransformation
- $f(x) \rightarrow F(u)$
- invers: $F(u) \rightarrow f(x)$
- Zerlegung einer Funktion (eines Signals) in Frequenzbestandteile
- Faltung im Ortsraum entspricht Multiplikation im Frequenzraum

## Abtasten Sampling
- Sei $f(x)$ bandbegrenzt durch $u_G$ d.h. $F(u) = 0$ für $|u| > u_G$
  - Dann sollte Abtastfrequenz $\frac{1}{\Delta x} > 2u_G$ sein
    - Kopien von $F(u)$ überlappen sich nicht
    - Frequenzspektrum von $F(u)$ kann vollständig aus dem Abtastsignal und dessen Werten berechnet werden
  - sonst
    - Aliasing
