# Über den Banknoten-Datensatz

> „Wenn man einen Dollarschein unter einem Mikroskop betrachtet, sieht er wie eine Gebirgslandschaft aus Tinte aus. Bei einer Fälschung wirkt er wie ein flacher Sumpf aus Punkten. Diese KI ‚sieht‘ nicht das Gesicht des Präsidenten; sie ‚fühlt‘ die Rauheit der Berge.“

![Illustration](images/illustration.png)

Dieser Datensatz wurde nicht erstellt, indem man Banknoten manuell mit einem Lineal vermessen hat. Er stammt aus einer Studie an der **University of Applied Sciences Ostwestfalen-Lippe (Deutschland)**.

Da sich professioneller Druck physikalisch stark vom Drucken zu Hause unterscheidet, kann ein neuronales Netzwerk — selbst ein kleines — diese Klassen sehr leicht voneinander trennen. Du solltest eine sehr hohe Genauigkeit erwarten (98–100 %).

- **Die Quelle:** Es wurden etwa 1.372 Banknoten gesammelt. Einige waren echt, andere waren hochwertige Fälschungen.
- **Der Prozess:** Es wurden nicht einfach iPhone-Fotos aufgenommen. Mithilfe einer Industriekamera, wie sie normalerweise zur Druckkontrolle eingesetzt wird, wurden die Banknoten mit hoher Auflösung (660 dpi) in **Graustufenbilder** digitalisiert.
- **Das Problem:** Ein Bild mit 400 × 400 Pixeln enthält 160.000 Datenpunkte (Pixel). Das ist für ein einfaches Modell zu groß und zu verrauscht. Daher musste die „Textur“ des Papiers in nur wenigen Zahlen zusammengefasst werden.
- **Die Lösung (Wavelet-Transformation):** Dabei handelt es sich um ein mathematisches Verfahren, das wie ein Mikroskop funktioniert und ein Bild in seine horizontalen, vertikalen und diagonalen Kanten zerlegt. Es trennt die „groben“ Informationen — die allgemeine Form der Banknote — von den „feinen“ Informationen, also den scharfen, winzigen Sicherheitsdetails.

### 2. Entschlüsselung der Merkmale (die „Übersetzung“)

Was bedeuten die Eingabewerte? _Ist das Bild scharf? Ist es komplex? Ist der Kontrast hoch?_

Echte Banknoten verwenden **Tiefdruck (Intaglio-Druck)** und Mikrodruck, wodurch extrem scharfe, klare Linien entstehen. Fälschungen, die häufig mit Laser- oder Tintenstrahldruckern hergestellt werden, sind „unschärfer“ oder weisen dort, wo eigentlich durchgehende Linien sein sollten, ein „Dithering“-Rauschen (winzige Punkte) auf.

Die vier Merkmale messen diesen Unterschied in der Textur:

| Merkmal | Mathematische Definition | Bedeutung für die „Banknote“ |
| --- | --- | --- |
| **Varianz** | Wie stark die Werte gestreut sind. | **„Kontrastintensität.“** Eine hohe Varianz bedeutet normalerweise, dass das Bild starke, markante Kanten und einen hohen Kontrast aufweist (wie bei scharfer Sicherheitsdruckfarbe). Eine niedrige Varianz deutet auf ein blasses oder verschwommenes Bild hin. |
| **Schiefe (Skewness)** | Wie asymmetrisch die Daten sind. | **„Verhältnis von Hell und Dunkel.“** Echte Banknoten weisen oft ein bestimmtes Verhältnis zwischen hellem Papier und dunkler Tinte auf. Eine Fotokopie kann dunkelgraue Bereiche in schwarze Flecken verwandeln und dadurch das Histogramm der Bilddaten verschieben. |
| **Kurtosis** | Wie „schwer“ die Verteilungsränder sind. | **„Schärfe der Kanten.“** Dieses Merkmal erkennt plötzliche Veränderungen. Eine echte Banknote weist sehr abrupte Übergänge auf (Papier–Tinte). Bei einer Fälschung sind die Übergänge weicher (Papier–verschwommene Kante–Tinte). Die Kurtosis erfasst diese „Ausreißer“ oder scharfen Sprünge. |
| **Entropie** | Die Zufälligkeit oder Unordnung der Pixel. | **„Komplexität.“** Echte Banknoten sind äußerst komplex und enthalten zufällig wirkende Sicherheitsmuster. Eine Fälschung kann diese Details verlieren und dadurch „glatter“ oder gleichmäßiger aussehen, wodurch sie eine geringere Entropie besitzt. |
