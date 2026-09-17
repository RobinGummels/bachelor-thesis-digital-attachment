# Digitale Beilage zum Anhang

Die digitale Beilage dokumentiert die Datengrundlage und die statistischen Auswertungen der Bachelorarbeit. Ihre Gliederung folgt den Themenbereichen A–D des Anhangs. Sie umfasst 32 Datentabellen, den numerischen Validierungsnachweis des explorativen Modellvergleichs sowie ein Datei- und ein Spaltenverzeichnis.

## Dateiformat und Einheiten

Alle CSV-Dateien verwenden UTF-8 mit BOM, Komma als Feldtrenner und Dezimalpunkt. Datumsangaben haben das Format JJJJ-MM-TT. Leere Felder kennzeichnen fehlende oder nicht anwendbare Angaben; bei Korrelationen können sie auch mathematisch undefinierte Werte anzeigen. Sie sind nicht als Nullen zu interpretieren. Die Spaltennamen sind deutsch und verwenden ae, oe und ue.

- `SPALTEN.csv` erläutert sämtliche Datenfelder einschließlich ihrer Einheiten.
- `DATEIEN.csv` enthält die Zeilenzahlen und SHA-256-Prüfsummen der Datentabellen sowie die Prüfsumme des Validierungsnachweises C11.

Die Einheit `1` bezeichnet dimensionslose Größen. Anteile liegen zwischen 0 und 1, sofern der Spaltenname nicht ausdrücklich `prozent` enthält. RIX-Werte sind in Prozent angegeben: Der Wert 3 entspricht 3 Prozent. Koordinaten beziehen sich auf ETRS89/UTM Zone 32N (EPSG:25832). Distanzen und Höhen sind in Metern, Windgeschwindigkeiten in m/s angegeben. Die Herkunft der Geländehöhen ist im Spaltenverzeichnis bezeichnet; ein gemeinsamer vertikaler Höhenbezug ist in den Begleitdaten nicht dokumentiert.

Die Beilage enthält technische Anlagentypen einschließlich gegebenenfalls darin enthaltener Nennleistungen. Individuelle Anlagenbeschreibungen, absolute beobachtete oder berechnete Erträge und absolute sektorale Energiemengen sind nicht enthalten. Reproduktionsgüten, Unsicherheiten und Transferfehler werden auf dimensionslosen Skalen angegeben. Die enthaltenen Koordinaten, technischen Angaben und Zeiträume ermöglichen eine räumliche Zuordnung zu realen Anlagen; die Positions- und Clusterkennungen stellen keine Anonymisierung dar.

## Kennungen und Tabellenverknüpfungen

Clusterkennungen wie `AS-01` sind über alle Untersuchungsstandorte eindeutig. Die Standortkürzel lauten:

| Kürzel | Standort |
|---|---|
| AS | Alpen-Sevelen |
| AM | Altenmellrich |
| BB | Bad Berleburg |
| BC | Borken-Coesfeld |
| LO | Lorup |
| OF | Ostfriesland |
| PA | Paderborn |
| RB | Rheda-Beckum |

Positionskennungen wie `AS-P001` identifizieren die untersuchten WEA- oder LiDAR-Positionen. Ein `clusterpaar` wie `AS-01--AS-02` bezeichnet ein ungeordnetes Paar. Bei gerichteten Transfers legen `referenzcluster` und `zielcluster` die Richtung fest. Das `referenzpaar` in D3/D4 bezeichnet die beiden gemeinsam verwendeten Referenzcluster. Innerhalb der Paarcodes sind die Clusternummern numerisch sortiert.

Die wichtigsten Verknüpfungen sind:

- A1 und A2 werden über `cluster`, A1 und B5 über `position` verbunden.
- B1 enthält die Merkmale und den beobachteten absoluten Logfehler jedes ungeordneten Paares. C2, C10 und D8 verweisen über `clusterpaar` auf diese Angaben.
- C1 enthält das gewählte Alpha je Hauptmodell und Teststandort. Für die 57 Merkmalskombinationen stehen diese Angaben in C6. Die Koeffizienten in C3 bzw. C7 sind über Modell und Teststandort zuzuordnen.
- D8 und D9 werden über Modell, Standort bzw. Teststandort, Merkmalsgewichtung und AOA-Grenzverfahren verbunden. Ein Fall liegt innerhalb der AOA, wenn `dissimilarity_index <= aoa_grenze_di` gilt.

Gegenrichtungen eines Transfers und mehrfach aufgeführte Modell- oder AOA-Varianten sind keine unabhängigen zusätzlichen Beobachtungen.

## A: Datengrundlage

**A1 – Positionen:** 178 untersuchte Positionen mit Clusterzuordnung, Positionsart, Anlagentyp, Koordinaten, RIX, Geländehöhe, Naben- bzw. Messhöhe und dokumentierten Zeiträumen. Die technischen Typbezeichnungen beziehen sich auf die 171 WEA. Für die sieben LiDAR-Positionen sind Anlagentyp, Rotordurchmesser und WEA-Betriebsdaten nicht anwendbar. Ihre Messzeiträume stehen unter Beobachtungsbeginn und -ende.

**A2 – Cluster:** 47 Cluster mit Positionsanzahl, räumlichen Merkmalen, mittleren Wakeverlusten, Reproduktionsgüten vor und nach empirischer Wakebereinigung sowie den verwendeten logarithmischen Standardunsicherheiten.

**A3 – Abschattende Positionen:** 804 zusätzliche standortbezogene Einträge mit Koordinaten, Gelände- und Nabenhöhe sowie dokumentierten Betriebsdaten. Dieselbe physische Anlage kann in mehreren Untersuchungsgebieten berücksichtigt sein; die Zeilenzahl ist daher nicht als Zahl eindeutig verschiedener Anlagen zu interpretieren.

## B: Transfergrundlage und Wake-Diagnosen

**B1 – Ungeordnete Paare:** 142 Modellfälle mit den sechs Prädiktoren, beobachtetem absolutem Logfehler und vorbereitetem Trainingsgewicht. Das Ziel der Gamma-Regression ist das Quadrat dieses absoluten Logfehlers.

**B2 – Gerichtete Transfers:** 284 Transfers mit Referenzcluster, Zielcluster und vorzeichenbehaftetem Log-Transferfehler `e`. Sein Betrag ist `abs(e)`, sein Quadrat `e^2` und die Transferreproduktion `exp(e)`. Die zugehörigen Clusterunsicherheiten stehen in A2, die Paarmerkmale in B1.

**B3 – Clustersektoren:** Zwölf 30-Grad-Anströmsektoren je Cluster mit Rauigkeitslänge, Waldflächenanteil, freier Windgeschwindigkeit und normiertem Energieanteil. Die Sektormitte wird im Uhrzeigersinn ab Nord angegeben. Die Energieanteile werden zunächst je Position auf die Summe eins normiert und anschließend innerhalb eines Clusters gleichgewichtet gemittelt. `sektorgewicht_0_bis_1` summiert sich deshalb über die zwölf Sektoren eines Clusters zu eins. Für ein Clusterpaar ist das Gewicht eines Sektors der Mittelwert der beiden Clustergewichte.

**B4 – Wake-Regressionen:** Standortbezogene OLS-Diagnosen des Zusammenhangs zwischen relativem Wakeverlust und Reproduktionsgüte. OLS bezeichnet die lineare Regression nach der Methode der kleinsten Quadrate. Die Intervalle und p-Werte beruhen auf der klassischen OLS-Inferenz und berücksichtigen weder räumlich abhängige Anlagenfehler noch Mehrfachtests.

**B5 – Grundlage der Wake-Residuen:** Unkorrigierte Reproduktionsgüten und relative Wakeverluste je WEA. Mit Interzept `b0` und Steigung `b1` aus B4 ergibt sich das Regressionsresiduum als `r - (b0 + b1 * Wakeverlust)`. Bei diesen Regressionen mit Interzept entspricht das Bestimmtheitsmaß R² dem Quadrat der Pearson-Korrelation.

Die Standardunsicherheit in A2 ist keine Varianz. Die vorbereiteten Trainingsgewichte in B1 sind auf den Mittelwert eins normiert und können größer als eins sein. Gleiche Gewichtssummen je Standort werden innerhalb der jeweiligen Trainingsfaltung hergestellt. Sektor- und Referenzgewichte summieren sich dagegen innerhalb ihrer jeweiligen Gruppen zu eins.

## C: Direkte Fehlerprognose und explorativer Modellvergleich

**C1–C4** dokumentieren die Standortkennzahlen, äußeren Vorhersagen, standardisierten Koeffizienten und innere Alpha-Validierung der vier Hauptmodelle:

| Modellbezeichnung | Bedeutung |
|---|---|
| Konstant | Gewichtete konstante Fehlerprognose |
| Distanz | Gamma-Regression mit horizontaler Entfernung |
| Wald + Wind | Gamma-Regression mit Waldanteilsdifferenz und Windgeschwindigkeitsdissimilarität |
| Vollstaendig | Gamma-Regression mit allen sechs Merkmalen aus B1 |

**C5–C11** dokumentieren den explorativen Vergleich aller 57 Merkmalskombinationen aus zwei bis sechs Prädiktoren. C5 enthält Rangfolge und Standortrobustheit, C6 die Standort-MAE und Alpha-Wahlen, C7–C9 die Koeffizienten und Stabilitätszusammenfassungen und C10 die äußeren Vorhersagen. C11 enthält den numerischen Abgleich mit den Notebook-Ergebnissen. Die Kombinationsnamen verwenden die Kurzformen Distanz, RIX, Gelaendehoehe, Rauigkeit, Wald und Wind für die sechs Prädiktoren aus B1. Die Merkmalsauswahl ist explorativ; ausschließlich Alpha wird in der inneren LOSO ausgewählt. Der vollständige Vergleich der 57 Kombinationen betrifft die direkte Fehlerprognose.

Die prognostizierte Größe in C2/C10 ist die Quadratwurzel des geschätzten mittleren quadrierten Logfehlers. Sie beschreibt ein RMS-artiges Fehlerniveau und entspricht nicht allgemein einem erwarteten absoluten Fehler oder einer reinen Standardabweichung. Die absolute Abweichung der direkten Fehlerprognose ergibt sich als:

`abs(prognostiziertes_rms_logfehlerniveau - beobachteter_absoluter_logfehler)`

Der direkte MAE ist der Mittelwert dieser Abweichungen. Der Makro-MAE mittelt die Standort-MAE mit gleichem Gewicht je Standort. OOF bedeutet, dass die Vorhersage aus einer äußeren LOSO-Faltung stammt, deren Trainingsdaten den gesamten betreffenden Standort ausschließen. Die vorgelagerte Wakebereinigung ist davon zu unterscheiden.

## D: Referenzgewichtung, AOA und TR6

**D1/D2** enthalten die kombinierten Logfehler je Zielcluster und die tatsächlich verwendeten Referenzgewichte mit allen verfügbaren Referenzen. **D3/D4** umfassen alle möglichen Kombinationen aus genau zwei Referenzen. Die Referenzgewichte liegen zwischen 0 und 1 und summieren sich je Zielcluster, Gewichtungsverfahren und gegebenenfalls Referenzpaar zu eins. In D1–D4 berücksichtigen die modellgestützten Gewichtungsverfahren die Quellunsicherheit.

**D5** enthält die Rangkorrelationen zur Referenzauswahl, **D6** die standortbezogene Gewichtskonzentration. Die effektive Referenzanzahl ergibt sich als `1 / Summe(w^2)`. **D7** vergleicht die Referenzgewichtung mit und ohne zusätzliche Quellunsicherheit. Diese Auswertung betrifft die Referenzgewichtung, nicht die Trainingsgewichte der Fehlermodelle. Der MAE der kombinierten Prognosen bewertet die tatsächlichen absoluten Logfehler der Zielprognosen.

**D8–D12** dokumentieren die AOA für das kompakte und das vollständige Fehlermodell. Für die Hauptauswertung sind gleichzeitig `merkmalsgewichtung = Koeffizientenbetraege` und `aoa_grenzverfahren = Oberer_Whisker` auszuwählen. D8 enthält 142 Paare × zwei Modelle × zwei Merkmalsgewichtungen × zwei Grenzverfahren. D9 enthält die Grenzwerte und Normierungsparameter, D10 die Merkmalsgewichte und Skalierungsparameter, D11 die standortübergreifenden Trainingsnachbarn und Trainings-DI. D12 fasst die Varianten zusammen.

Bei Trainingsmittelwert und Trainingsstandardabweichung in D10 gilt die Einheit des jeweiligen Merkmals; seine Bezeichnung entspricht dem Feldnamen in B1. Die normierten Merkmalsgewichte summieren sich je Modell, Teststandort und Gewichtung zu eins. Standardisierte Koeffizienten, Dissimilarity Index und AOA-Grenzen sind dimensionslos. Ein Trainings-DI verwendet den nächsten Nachbarn aus einem anderen Standort.

**D13** dokumentiert die Zahl gerichteter Transfers und die Ausschlüsse nach den drei verwendeten TR6-Kriterien: horizontale Distanz kleiner als Grenze B, absolute Geländehöhendifferenz kleiner als 100 m und absolute Nabenhöhendifferenz höchstens 40 Prozent der Zielnabenhöhe. Ausschlusszahlen können sich überlagern und dürfen nicht addiert werden. Ein ungeordnetes Paar zählt als vertreten, wenn mindestens eine Richtung die Auswahlkriterien erfüllt. Die Prüfung verwendet Clusterwerte und bildet lediglich die drei genannten Kriterien ab. Sie ist kein vollständiger Nachweis der Konformität mit FGW TR 6. Die technischen Feldnamen mit `tr6_konform` und die Kategorie `TR6_konform` bezeichnen in diesen Dateien diese TR6-orientierte Auswahl.

**D14** enthält die Standortkennzahlen der vier statistischen Vergleichsmodelle für alle Transfers und für die TR6-orientierte Teilmenge. Die Fehlermodelle werden für diesen Teilmengenvergleich nicht neu angepasst. Die AL-PRO-Auswertung wird in der Bachelorarbeit in zusammengefasster Form berichtet. Interne AL-PRO-Berechnungsvorschriften, Einzeltransfer-Unsicherheitswerte und standortbezogene AL-PRO-Kennzahlen sind nicht Bestandteil der Beilage.
