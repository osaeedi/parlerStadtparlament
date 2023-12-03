# Open Data St.Gallen

Datendownload und -preprocessing sowie automatische Klassifikation von Parlamentsgesch�ften 

## Einleitung

Wirtschaftsingenieurwesen Studierende im 6. Semester der Ostschweizer Fachhochschule in St.Gallen, haben von der Stadt St.Gallen und insbesodere Nicola Wullschleger (Projektmanager Open Data, Stadt St.Gallen) eine praxisorientierte Aufgabenstellung erhalten, um diese im Modul Machine Learning unter der Leitung des Dozenten Dr. Beat T�dli zu bearbeiten.




### Ausgangslage

Die Stadt St.Gallen betreibt seit September 2019 ein Open Data Portal auf dem unpers�nliche, unkritische Daten der Stadtverwaltung ver�ffentlicht werden. Mit der Ver�ffentlichung von sogenannten Open Government Data (OGD) als maschinenlesbare Datens�tze will die �ffentliche Verwaltung einen Beitrag zur F�rderung von Transparenz, Partizipation, und Innovation leisten. Neben Statistikdaten, Geodaten, Verkehrsz�hldaten oder Sensordaten geh�ren dazu auch Daten aus dem Politik- und Verwaltungs-Bereich, wie beispielsweise �ffentliche Vergaben oder die st�dtischen Budgets.

Nun plant die Stadt St.Gallen die Ver�ffentlichung eines umfangreichen Datensatzes des st�dtischen Ratsinformationssystems. Darin beinhaltet sind die traktandierten Gesch�fte des Stadtparlaments St.Gallen seit dem Jahr 2001. Den behandelten Gesch�ften sind verschiedenen Eigenschaften wie das Sitzungsdatum, die Art des Gesch�fts, oder auch die Aktenplannummer (sprich das Thema) zugeordnet. Damit lassen sich die rund 4000 Gesch�fte nicht nur thematisch filtern, sondern es lassen sich auch politikwissenschaftliche Analysen bspw. �ber die Themenschwerpunkte im Verlauf der Jahre durchf�hren.

### Problemstellung

Die Gesch�fte des Stadtparlaments k�nnen grossmehrheitlich in zwei Arten unterteilt werden:

Die Sachgesch�fte, welche von Seiten der Verwaltung angestossen, bearbeitet und traktandiert werden (1750 Gesch�fte).
Die Parlamentarischen Vorst�sse, bestehend aus Interpellationen, Motionen und Einfachen Anfragen, welche von Seiten der Stadtparlamentarierinnen und Stadtparlamentariern eingebracht werden (1840 Gesch�fte).

W�hrend die Sachgesch�fte einer thematischen Aktenplannummer wie Schule, Kultur, Entsorgung, etc. zugeordnet werden, erhalten die parlamentarischen Vorst�sse eine Aktenplannummer nach der entsprechenden Gesch�ftsart. Dies f�hrt zu folgender thematischer H�ufung der Gesch�fte.

 
Erl�uterung: Die erste S�ule "Stadtparlament" wird durch die grosse Anzahl an parlamentarischen Vorst�ssen bestimmt, w�hrend die Sachgesch�fte in die restlichen Kategorien eingeteilt werden.

Diese Verzerrung der Themen f�hrt zu einem geringeren Mehrwert des Datensatzes, weil

die Filterung nach Aktenplannummer (Thema) unvollst�ndige Resultate ergibt,
politische Themenanalysen nur die Sachgesch�fte und somit die Verwaltungsseite abdecken, und
damit ein politikwissenschaftlicher Vergleich der Gesch�ftsthemen zwischen Verwaltungsseite und Parlamentsseite verunm�glicht wird.

### Ziel

W�hrend eine manuelle Neuzuordnung der parlamentarischen Vorst�sse m�glich w�re, ist sie ressourcentechnisch unrealistisch. Aus diesem Grund soll dieser Mangel des Datensatzes, mittels Data Mining kategorisiert werden. Ziel ist es, die parlamentarischen Vorst�sse den bestehenden thematischen Kategorien zuzuordnen und die Genauigkeit der maschinellen Zuordnung auszuweisen. Fehlerhafte Zuordnungen sollen m�glichst vermieden werden, um die Qualit�t der Filterfunktion des Datensatzes zu gew�hrleisten. Mittels der ausgewiesenen Genauigkeit k�nnten ungenaue Zuordnungen durch Verwaltungsmitarbeitende �berpr�ft oder manuell zugeordnet werden. Damit kann die Machine Learning Anwendung den Nutzen des Datensatzes massiv steigern, w�hrend der manuelle Aufwand innerhalb der Verwaltung minimal gehalten wird.

### Datenstruktur

Die Themen, sprich die Aktenplannummern enthalten verschiedene Ebenen, welchen die Sachgesch�fte und parlamentarischen Vorst�sse zugeordnet wurden. Die hierarchische Struktur des Aktenplans sieht wie folgt aus:

Ebene 1: 9 Kategorien
Ebene 2: 35 Kategorien
Ebene 3: 175 Kategorien
Ebene 4: 1094 Kategorien
etc.

Aus diesem Grund ist eine Zuordnung auf Basis von Ebene 2 realistisch. Der Aktenplan auf Ebene 2 beinhaltet 35 Kategorien, wovon 29 im vorliegenden Datensatz verwendet wurden. 12 Kategorien enthalten weniger als 20 Gesch�fte, weshalb sie in der Kategorie "sonstige Themen" zusammengefasst wurden. Neben der Kategorie "Stadtparlament", in der die parlamentarischen Vorst�sse enthalten sind, verbleiben somit die 17 folgenden Kategorien, welchen die Gesch�fte zugeordnet werden sollen:

- B�rgerschaft					
- Entsorgung
- Finanzhaushalt					
- Kultur
- Organisation der Verwaltung		
- Schulen
- Soziales, Sozialhilfe			
- Sport
- Stadtrat						
- Stadtwerke
- St�dtisches Personal			
- Umweltschutz
- Verkehr, Telekommunikation		
- Verkehrsbetriebe
- �ffentliche Ordnung und Sicherheit	
- �ffentliches Bauen
- Sonstige Themen

## Installation
### Code aus Gitlab holen
- in der Konsole 

		git clone ssh://git@gitlab.ost.ch:45022/beat.toedtli/opendatasg.git

ausf�hren.

### Anaconda virtuelles Environment generieren
- ev. bestehende Environments anzeigen:

		conda info --envs  
- ev. bestehendes Environment l�schen:

		conda remove -n male --all

- [Virtual Environment generieren](https://de.acervolima.com/richten-sie-mit-anaconda-eine-virtuelle-umgebung-fur-python-ein/#google_vignette)

		conda env create -n male --file male.yml
		conda activate male
		pip install pdfplumber
		python -m spacy download de_core_news_md
		#ev. alternativ:
		python -m spacy download de_core_news_md --user

**Notiz: Mamba ist viel schneller als conda, daher die Empfehlung stattdessen dies zu benutzen:**

		mamba env create -n male --file male_mamba.yml
		conda activate male
		python -m spacy download de_core_news_md
		#ev. alternativ:
		python -m spacy download de_core_news_md --user

- Conda aktivieren

		conda activate male

## Daten herunterladen

		python daten-stadt-sg.py

## Ausf�hren der Erkennung
Mit 
	python main.py
wird die `inputcsv`-Datei (siehe `config.ini`) gelesen und um zus�tzliche Spalten erg�nzt, welche die Vorhersagen enthalten.

### Known Issues
- Pip und Conda passen nicht gut zusammen- leider gibt es aktuell kein brauchbares pdfplumber Paket in conda
- Die abgespeicherten Pickle-Dateien der Scikit-Learn-Klassifikatoren sind in �lteren Scikit-Learn Versionen erstellt worden als die Scikit-Learn Version, die mit der `male.yml`-Datei installiert wird. Daher entstehen `UserWarning`-Warnmeldungen in der Konsole.

## Authors and Acknowledgment
Mitwirkende Studenten:
- Biel Luca
- Bucheli Mathias
- Hensch Andreas
- Vonplon Maurice
- Wagner Pascal
Dozierender und aktuell Repository-Verantwortlicher: 
- [Dr. Beat T�dtli](beat.toedtli@ost.ch)
Danke auch Nicola Wullschleger und der Open Data Plattform der Stadt St.Gallen f�r den Use Case!

## License
Aktuell ist der Code noch Closed-Source.

## Project status
Wird weiterentwickelt. Mitarbeit jederzeit willkommen!
