# Dokumentation der GPT4o-Übersetzung des Bullingerkorpus

**Dominic P. Fischer und Martin Volk**, 26. Mai 2025

Im April 2025 hat Dominic Fischer alle Briefe, für die wir eine manuelle
Transkription haben, mit GPT (Version 4o) nach Englisch übersetzt.
Ausgangssprachen waren Latein und Frühneuhoch-Deutsch. Die Briefe
enthalten auch Einschübe in Griechisch und Hebräisch. Die wenigen Briefe
in Französisch, Griechisch und Italienisch wurden ebenfalls auf die
gleiche Art übersetzt.

Das umfasst alle Briefe der HBBW-Edition (Band 1 bis und mit 21) sowie
alle Briefe mit provisorischer Transkription. Die Briefe mit
automatischer Transkription haben wir nicht übersetzt.

- Da wir vorab experimentell nachgewiesen haben, dass die
  **Zusammenfassung** (das Regest) eines Briefes (manuell erstellt für
  alle Briefe in der HBBW-Edition) die MÜ-Qualität steigert, hat Dominic
  jeweils Brieftext plus zugehöriges Regest als Eingabe an GPT
  geschickt. Alle Regesten hat er zuvor mit GPT-4o von Deutsch nach
  Englisch übersetzt unter Einbezug von Meta-Information. Der Prompt war
  "_The following summary summarises a letter that is part of Heinrich
  Bullinger's correspondence of the 16th century. The letter was
  written on \_\_\_\_ by \_\_\_\_in \_\_\_\_ and addressed to \_\_\_\_
  in \_\_\_\_. Translate it from German to English while preserving the
  XML-tags._"

- Da wir vorab experimentell nachgewiesen haben, dass **lexikalische
  Information** in Fussnoten die MÜ-Qualität steigert, hat Dominic die
  Information (typischerweise ein oder zwei Worte in modernem Deutsch
  als Erklärung für ein Wort oder eine Phrase in Frühneuhoch-Deutsch)
  jeweils in runden Klammern an der Stelle der lexikalischen Fussnote im
  Brieftext eingefügt.

Dieses Vorgehen hat für die MÜ der überwiegenden Mehrheit der Briefe gut
funktioniert. Bei wenigen, sehr langen Briefen ist die MÜ mitten im
Brief abgebrochen. Diese Briefe hat Dominic manuell in zwei Teile
aufgeteilt, die Teile mit GPT übersetzt und die Übersetzungen dann
zusammengefügt.

# Prompt

_The following letter is part of Swiss reformer Heinrich Bullinger\'s
correspondence in the 16th century. It was written on \_\_\_\_ by
\_\_\_\_in \_\_\_\_ and addressed to \_\_\_\_ in \_\_\_\_. Translate it
from \_\_\_\_ to English while preserving the XML-tags: **Brieftext**._

\*Make sure to translate proper nouns into their modern German
equivalents. Words in parentheses are lexicon notes that explain the
meaning of the preceding word(s). As a help for your translation,
consult this summary: **Regest in English.\***

Metadaten wie Sprache, Absender und Adressat des Briefes wurden von den
XML-Korpus-Dateien extrahiert und in den Prompt eingebaut. Bei fehlenden
Metadaten wurde der entsprechende Teil ausgelassen und der Prompt
automatisch entsprechend angepasst (z.B. keine Information über
Absender, Ort und Datum -> Der erste Satzteil fällt weg: "_It was_
_addressed to \_\_\_\_ in \_\_\_\_."_).

Bei Eigennamen wurde die Anweisung "into modern German" mitgegeben, auch
wenn der Text auf Englisch übersetzt wurde. Dies, da sich viele der
Akteure und Ortschaften im deutschsprachigen Raum befinden und deshalb
oft moderne deutsche, nicht englische Namensvarianten besitzen.

# Filterung von Brieftext und Regest

**Brieftext**: Die \<div\>- und \<p\>-Tags haben wir übernommen, um die
hierarchische XML-Struktur beizubehalten. Von jedem Paragraphen \<p\>
wurden alle Sätze extrahiert, bereinigt und zusammengefügt. Die
Bereinigung beinhaltete das Extrahieren von Namen aus ihren Tags
(\<persName\> oder \<placeName\>) und von lexikalischen Fussnoten,
welche in Klammern an den Ort ihres Auftretens gesetzt wurden. Zuletzt
wurden generische Normalisierungsschritte (z.B. mehrere Leerzeichen ->
ein einziges Leerzeichen) unternommen.

**Regest**: Das Vorgehen hier war dasselbe, wobei die Regesten keine
\<div\>-Tags beinhalteten.

# Integration von lexikalischen Fussnoten und Regest

Lexikalische Fussnoten (typischerweise Entsprechungen in modernem
Deutsch für einzelne Wörter oder Phrase in Frühneuhochdeutsch, nie für
Latein) wurden in Klammern direkt in den Brieftext an der Stelle ihres
Auftretens eingesetzt. Dies wurde so vorgenommen, weil bei Fussnoten nur
die Stelle im Text markiert ist, nicht aber, auf wie viele der
vorangehenden Wörter sie sich beziehen (z.B. Brief HBBW 794: "\[...\]
_Fellix Müller, den duech scherer (Tuchscherer) \[...\]."_)

Das Regest wurde – nach oben beschriebener Bereinigung – direkt in den
Prompt eingefügt.

# Qualitätsüberprüfungsmechanismen

## \<div\> und \<p\>-Abgleich

Das Original wurde mit \<div\>- und \<p\>-Tags in den Prompt gegeben, um
so direkt XML erzeugen zu können. Es lag deshalb nahe, die Anzahl Tags
zwischen Original und Übersetzung abzugleichen (sowie sicherzustellen,
dass die Übersetzung XML-wohlgeformt ist).

8567 Briefe haben in Ausgans- und Zielsprache dieselbe Anzahl Tags, 51
Briefe haben eine abweichende Anzahl \<p\>-Tags (zunächst waren es 85
Briefe, 34 davon aber konnten in weiteren Versuchen mit gezieltem
Prompting noch richtig aligniert werden).

Die manuelle Überprüfung einer Stichprobe dieser 51 Briefe hat ergeben,
dass häufig bereits im originalen XML unnötige Paragraphen bestehen,
z.B. 10404: *\[\...\] presertim \<p\> Zurzachenses \[\...\]*. In keinem
der Fälle aber besteht das Problem, dass sich durch die falsche
Alignierung etwas mit der Regest-Alignierung verschiebt.

Auch bei Fällen, in denen in der Übersetzung weniger Paragraphen als im
Original vorhanden sind, wurden Paragraphen bei der Übersetzung
ausgelassen. Der Längenvergleich bestätigt dies.

## Längenvergleich übersetzte Briefe

Um sicherzustellen, dass jeweils der vollständige Brief übersetzt wurde,
wurde ein Längenvergleich vorgenommen. Die übersetzten Briefe wurden
nach Leerzeichen aufgesplittet, genauso wie die originalen Briefe (in
der Form, in der GPT4o sie im Prompt gefüttert bekam).

Der Vergleich der dadurch erhaltenen Tokenzahlen lieferte ein
Durchschnittsverhältnis von 1:1,3 (Länge Original gegenüber Länge
Übersetzung). Das erscheint insofern sinnvoll, als 80% der Briefe in
Latein sind, wobei Latein eine morphologisch reiche Sprache ist, die mit
weniger (Leerzeichen-separierten) Wörtern auskommt.

Sechs Briefe haben \<= 90% der Länge des Originals. Die manuelle
Überprüfung hat gezeigt, dass dies allesamt frühneuhochdeutsche Briefe
sind.

Zwei Briefe haben \>= 170% der Länge des Originals. Beides sind kurze
lateinische Briefe, genauso wie die 31 Briefe zwischen 160% und 170%
Länge.

Unter den 51 inkorrekt alignierten Briefen finden sich keine Briefe mit
Länge \>= 160% oder Länge \<= 90% des Originals.
