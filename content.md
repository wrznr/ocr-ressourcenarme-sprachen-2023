layout: true
  
<div class="my-header"></div>

<div class="my-footer">
  <table>
    <tr>
      <td style="text-align:right">Böhmak</td>
      <td style="text-align:left">Sorbisches Institut Bautzen</td>
    </tr>
    <tr>
      <td style="text-align:right">Würzner</td>
      <td style="text-align:left">Sächsische Landesbibliothek – Staats- und Universitätsbibliothek</td>
    </tr>
  </table>
</div>

<div class="my-title-footer">
  <table>
    <tr>
      <td style="text-align:left"><b>Wito Böhmak</b></td>
      <td style="text-align:right"><b>Kay-Michael Würzner</b></td>
    </tr>
    <tr>
      <td style="text-align:left">Sorbisches Institut Bautzen</td>
      <td style="text-align:right">SLUB Dresden</td>
    </tr>
    <tr>
      <td style="font-size:8pt"><b>14.September 2023</b></td>
    </tr>
    <tr>
      <td style="font-size:8pt">Workshop „KI für kleinere Sprachen“</td>
    </tr>
  </table>
</div>

---

class: title-slide
count: false

# Automatische Texterkennung für ressourcenarme Sprachen
## am Beispiel des Obersorbischen

---

# Überblick

- Hintergründe zum Obersorbischen
- Maschinelles Lernen am Beispiel der automatischen Texterkennung
- Training von OCR-Modellen
- Methoden der ML-gestützen Layouterkennung
- prototypische Workflows mit Werkzeugen aus OCR-D

---

class: part-slide
count: false

# Hintergründe zum Obersorbischen

---

# Hintergründe zum Obersorbischen
[Obersorbisch - hornjoserbšćina](https://www.sorabicon.de/hsb/kulturlexikon/artikel/prov_gs5_2lv_23b/)
.cols[
.fifty[
- westslawische Sprache
    * Sorbisch = Niedersorbisch und Obersorbisch
    * 20000–25000 Sprecherinnen und Sprecher in der Oberlausitz
    * zwischen Bautzen (Budyšin), Kamenz (Kamjenc) und Hoyerswerda (Wojerecy) 
    * im Deutschen bis 1945 *Wendisch* benannt
]
.fourty[
<p style="margin-top:-30px">
<img src="https://upload.wikimedia.org/wikipedia/commons/7/7c/Sorbisches_Siedlungsgebiet.png" />
</p>
]
]

---

# Hintergründe zum Obersorbischen

.cols[
.fifty[
- obersorbische Schriftsprache der Gegenwart
    * Vereinheitlichung zweier Traditionslinien
    * katholisches und evangelisches Schrifttum
- erstes gedrucktes obersorbisches Buch 1595: Wjacław Warichius: „Der kleine Catechismus“
- zu Beginn des 18. Jh. zwei obersorbische Schriftsprachenvarianten
- seit Mitte des 19.Jh. Bestrebungen zur Vereinheitlichung (analoge Rechtschreibung, Antiqua)
]
.fourty[
<p style="margin-top:-30px">
<img src="https://digital.slub-dresden.de/data/kitodo/LuthDer_1737590336/LuthDer_1737590336_tif/jpegs/00000032.tif.original.jpg" />
</p>
]
]

---

# Sorbisches Institut

.cols[
.fifty[
- Gründung Anfang 1992
    * außeruniversitäre Einrichtung zur Erforschung von Sprache, Geschichte und Kultur der Sorben in der Ober- und Niederlausitz
    * Vorgänger: 1951–1991 Institut für sorbische Volksforschung in der DDR
    * sorbisches wissenschaftliche Institut in Tradition der *Maćica Serbska*
- zwei standortübergreifende (Bautzen und Cottbus) Forschungsabteilungen
    * Kulturwissenschaften und Sprachwissenschaft 
]
.fourty[
<img src="img/sihaus.jpg" />
    ]
    ]

---

# Sorbisches Institut

- öffentliche wissenschaftliche Bibliothek und Archiv mit Forschungs- und Servicecharakter (Sorbische Zentralbibliothek und Sorbisches Kulturarchiv)
- „Lětopis“ als interdisziplinäres Fachorgan
    * zwei spezifische Schriftenreihen sowie digitale Angebote
- mehr als 70 Mitarbeiter (hoher Anteil an Drittmittel-Projekten)

---

# Ausgangssituation

- Digitalisierungen am SI seit 15 Jahren
- Landesdigitalisierungsprogramm (LDP) Sachsen,  
  koordiniert am Dresdner Digitalisierungszentrum der SLUB
- 2016–2017 im Rahmen des LDP Digitalisierung historischen Schrifttums: 
    + Antiqua – ungenügende Volltext-Qualität
    + Fraktur – keine Volltext-Erzeugung
- besonderes Problem **Fraktur Sorbisch**: 
    - slawische Diakritika, bisher keine verlässliche automatische Texterkennung (OCR)
    - mehrere Schreibweisen, Übergänge

---

# Wissenschaftlich nachnutzbare Volltexte
 
<!-- Für wen? -->


- strukturierter Volltext mit digitaler Präsentation
    - u.a. für Wissenschaftler, Heimatforscher, Journalisten, breiten Bildungsbereich
    - u.a. für Search/Retrieval, Textkorpora, hist. Wörterbücher
- Belieferung mit Forschungsdatenrepos (Ground-Truth)  
  und Sprachressourcen (Modelle)

<!-- GT: manuell erfasster Text (idealerweise fehlerfrei), mit -Text-Zuordnung -->
<!-- Minderheitensprache/ressourcenknappe Sprache -->
<!-- Synergien zwischen Zwecken und Rollen der Beitragenden -->

---

## Ein Beispiel: Serbske Nowiny 23.3.1878 <br/>(überwiegend Fraktur)

<table>
   <tr>
        <td>        
<img src="https://i.imgur.com/jPcGYZz.png" width="400px"/>
        </td>
        <td>
<img src="https://i.imgur.com/ZTrMzQ3.png" width="600px"/>
        </td>
    </tr>
</table>


```xml
<head><lb/>Ze Serbow.</head>
<p>
<lb/>
S Budyſchina. Jene nowiny w tychle dnjach žortniwje
<lb/>
měnjachu, ſo je ſapocžatk nalěcźa lětſa tak hubjeny był, ſo to ani
<lb/>
najſtarſche žaby pomnicź njemóža, a ſo drje ßu ſchkórzy hwiſdali,
<lb/>
ale to najſkerje teho dla, ſo bychu ßo trochu ſhrěli...
</p>
```

---

## Sorbische Druckzeichen Antiqua/Fraktur
![](https://i.imgur.com/wcWyYml.jpg =700x)

*Jan Arnošt Smoler: Mały Sserb aby Serske a Njemske Rosmłowenja atd. = Wendisch-Deutsche Gespräche nebst einem wendisch-deutschen und deutsch-wendischen Wörterbuche, sowie einem Verzeichnisse von Ortsnamen, einer Darlegung der Aussprache und Orthographie und Zugabe der gebräuchlichen Eidesnormen, Bautzen 1841*
<!-- .element: style="font-size: 20px" -->

---

## Wo noch? – Fraktur und Antiqua Tschechisch
![](https://i.imgur.com/wpZz2ky.png)

*Alphabete orientalischer und occidentalischer Sprachen,  
zsgest. von Friedrich Ballhorn, 8., verb. Aufl., Leipzig 1859*
<!-- .element: style="font-size: 20px" -->

---

## Erste Studie zu Ground-Truth / Trainingsmodell in 2019

OCR für ressourcenarme Sprachen am Beispiel des Obersorbischen  
(Kay-Michael Würzner & Wito Böhmak, Abstract zum Dt. Bibtag 2020 + DFG-Antrag):

- Bericht über manuelle (und iterative) Erstellung von **GT** für Fraktur-Obersorbisch und **Training** eines Tesseract-Modells per Finetuning von `Fraktur`
- Untersuchung mit ABBYY Recognition Server und Tesseract auf ihre  
  **Eignung** für die Erzeugung wissenschaftlich nachnutzbarer Volltexte
- sowohl ABBYY Recognition Server mit dem Modell `Altdeutsch/Gothic`  
  als auch Tesseract mit dem sprachunabhängigen Modell `Fraktur`  
  erzielten **schlechte** Genauigkeit
- Erstellung von GT und eigenem Trainingsmodell `hsb_frak` mit einfachem Workflow: **Machbarkeit**


| | ABBYY | Tesseract | Tesseract (nachtrainiert) |
| --- | --- | --- | --- |
| Zeichenfehlerrate: | 12-17% | 8-11% | 0,5-3,7% |


<!-- also: "Lösungsansatz" -->

---

## Entwicklung seit 2020

<!-- oder "Fortschritt"? -->

**Verstetigung** in anderen Projektkontexten

<!-- Verstetigung der Projektidee durch andere Förderinstrumente -->

- SI: Retrodigitalisierung und Präsentation auf Basis von Kitodo
- SLUB: Beteiligung bei…
   + Entwicklung [Kitodo](https://www.kitodo.org/) und [DFG-Viewer](http://dfg-viewer.de/)
   + DFG-Förderinitiative [OCR-D](https://ocr-d.de)
   + DDB [Zeitungsportal](https://pro.deutsche-digitale-bibliothek.de/deutsches-zeitungsportal)

<!-- Machbarkeit im Gesamtsystem -->

**Einsetzbarkeit** im produktiven Betrieb mit komplexem Workflow
<!-- Reading Order zu Blockreihenfolge, Images zu Scans, LogicStruc = Struktur (manu oder auto), DFG-Viewer zu KITODO.PRES / DFG-Viewer, OCRD zu OCR-D, PROZESSOR zu docstruct, PAGEXML zu PAGE, TEI-XML zu TEI -->

![](https://i.imgur.com/VyNdEKM.png)

---

## Was macht eine hochqualitative Texterkennung aus?

- *gute Segmentierung*: Ist der Text richtig lokalisiert worden?  
  (kein Text verloren, kein Nicht-Text verwechselt)
   + scheinbare/fehlende Wörter oder Zeilen
   + überlappende/abgeschnittene Zeichen
- *gute OCR*: Sind die Zeichen an sich richtig erkannt worden?
- *gute Strukturerkennung*: Sind die Blöcke und Zeilen in der richtigen Reihenfolge? Wurden Überschriften markiert? Wurden Kapitel/Artikel separiert?
- *weitere Analyse*: Schriftauszeichnung, Textnormalisierung


<!-- → **OCR-Workflow** -->

<!-- 2. Kasten zu "Zeilensegmentierung", 3. Kasten zu "Struktur + Reihenfolge", Artikelerkennung zu "Artikelseparierung" 

außerdem: 2. Kasten vor dem 1. Kasten

-->

![](https://i.imgur.com/6sjl9Yo.png)


<!-- Ende WB -->

---

class: part-slide
count: false

# Maschinelles Lernen am Beispiel der automatischen Texterkennung

---

# Kurze Einführung OCR

.cols[
.sixty[
- Bilderfassung ≠ Texterfassung
- **O**ptical **C**haracter **R**ecognition: Automatische Erfassung von Text in Bildern
- ursprünglich begrenzt auf Zeichenerkennung
- heute häufig Synonym für den gesamten Texterfassungsprozess
  + Bildvorverarbeitung
  + Layoutanalyse (OLR)
  + Zeilenerkennung
  + ...
]
.fourty[
<center><img src="https://upload.wikimedia.org/wikipedia/commons/9/9f/Codex_Manesse_127r.jpg" /></center>
]
]

---

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_raw.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_raw.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_opt.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
- Layoutanalyse
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_opt.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
- Layoutanalyse
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_struct.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
- Layoutanalyse
    * **strukturierende** Elemente
        + Absätze
        + Überschriften
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_struct.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
- Layoutanalyse
    * **strukturierende** Elemente
        + Absätze
        + Überschriften
    * **textflussunterbrechende** Elemente
        + Seitenzahlen
        + Kolumnentitel
        + Abbildungsunterschriften
        + Marginalien etc.
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_struct.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
- Layoutanalyse
    * **strukturierende** Elemente
        + Absätze
        + Überschriften
    * **textflussunterbrechende** Elemente
        + Seitenzahlen
        + Kolumnentitel
        + Abbildungsunterschriften
        + Marginalien etc.
    * **nichttextuelle** Elemente
        + Abbildungen
        + Tabellen etc.
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_struct.svg" />
</p>
]
]

---

count: false

# Komponenten eines einfachen OCR-Workflows

.cols[
.fifty[
- Bildvorverarbeitung
- Layoutanalyse
    * **strukturierende** Elemente
        + Absätze
        + Überschriften
    * **textflussunterbrechende** Elemente
        + Seitenzahlen
        + Kolumnentitel
        + Abbildungsunterschriften
        + Marginalien etc.
    * **nichttextuelle** Elemente
        + Abbildungen
        + Tabellen etc.
- Texterkennung
]
.fourty[
<p style="margin-top:-80px">
<img src="img/grenzboten_text.svg" />
</p>
]
]

---

# Texterkennung: Zeichenorientierte Ansätze

.cols[
.seventy[
- Erkennung erfolgt *glyphenweise*
  - **Mustervergleich**: Vergleich der Zeichenbilder zu in einem „Setzkasten“ gespeicherten Glyphen **Pixel für Pixel**
  - **Merkmalsvergleich**: Zerlegung der Glyphen in vordefinierte, bedeutungstragende **Eigenschaften** wie *Einfärbung*, *Kurven*, *Linien* etc. und Vergleich zu Referenzmaterialien
]
.fourty[
<center><img src="img/char.svg" width="300px" /></center>
]
]

---

count: false

# Texterkennung: Zeichenorientierte Ansätze

.cols[
.seventy[
- Erkennung erfolgt *glyphenweise*
  - **Mustervergleich**: Vergleich der Zeichenbilder zu in einem „Setzkasten“ gespeicherten Glyphen **Pixel für Pixel**
  - **Merkmalsvergleich**: Zerlegung der Glyphen in vordefinierte, bedeutungstragende **Eigenschaften** wie *Einfärbung*, *Kurven*, *Linien* etc. und Vergleich zu Referenzmaterialien
]
.fourty[
<center><img src="img/char.svg" width="300px" /></center>
]
]
- *regelbasiertes Vorgehen*
    + **direkte** Abbildung von Referenzmaterial
    + Modellierung von Expertenwissen
- Zerlegung der Seite in *Zeilen* und *Zeichen* notwendig

---

# Texterkennung: Zeilenorientierte Ansätze

- Erkennung erfolgt *zeilenweise*
  1. **Skalierung:** einheitliche Höhe für alle Zeilen
  2. **Merkmalsextraktion**: Raster mit festgelegter Anzahl (horizontaler) Zeilen und variabler Anzahl (vertikaler) Spalten → Zeilen als Sequenzen binärwertiger Vektoren fixer Länge
<center><img src="img/grid.svg" width="800px"/></center>
- kontextsensitive Erkennung über *Übergangswahrscheinlichkeiten* der Vektoren
- Zerlegung der Seite in *Zeilen* notwendig
- Vorgehen robuster gegenüber Varianz durch Artefakte als zeichenorientierte Ansätze
- `Tesseract` (ab Version 4), `OCRopus`, `kraken`, `Calamari`
  + Einsatz *neuronaler Netze* für die Sequenzklassifikation

---

# Texterkennung: Zeilenorientierte Ansätze

- zentrales Verfahren des maschinellen Lernens (cf. e.g. [Xing et al. 2010](https://www.cs.sfu.ca/~jpei/publications/Sequence%20Classification.pdf))
- basierend auf dem **Satz von Bayes**: `\(P(C|E) = \frac{P(E|C)\cdot P(C)}{P(E)}\)`
- Rezept
    + Man nehme
        * eine **sehr große** Liste **manuell annotierter** Daten und
        * einen **Trainingsalgorithmus**,
    + modelliere eine **`n:n`-Beziehung** zwischen Eingabe und Ausgabe,
        * e.g., jedes Eingabeelement (Buchstabe) wird auf eine Klasse abgebildet
    + induziere ein **statistisches Modell**,
    + und evaluiere dessen Qualität anhand von **Evaluationsdaten**

---

# Texterkennung: Zeilenorientierte Ansätze

- Übertragung auf OCR
    + Daten
        * https://htr-united.github.io/
        * manuell transkribierte Textzeilen
    + Kodierung `\(f: \mathbb{N}^{10}\rightarrow\mathbb{B}\)` 
      $$
      f(x[n]) = \begin{cases} 1 & \text{Pixel in Zelle $(x,n)$ schwarz} \\\\
      0 & \, \text{sonst}\end{cases}
      $$ 
    + Training
        * Zählen von Sequenzen aus Vektor-Buchstabenteil-Paaren
        * Repräsentation als OCR-Modell
        * Tesseract: [tesstrain](https://github.com/tesseract-ocr/tesstrain)
.cols[
.fifty[
```
  0123456789
0 1111111111
2 0000110000 
```
]
.fifty[
<center>
<img src="img/hi.png" style="width:150px"/>
</center>
]
]

---

## Maßnahmen zur Verbesserung der Textqualität für Obersorbisch

| | OLR | OCR | AS | |
| --- | --- | --- | --- | --- |
| Bereitstellung von Daten |  | ✅ |  | SI |
| Entwicklung von Werkzeugen | ✅ | ✅ | ✅ | SLUB / OCR-D |
| Entwicklung von Modellen |  | ✅ |  | SI / SLUB |
| Erarbeitung von Workflows | ✅ | ✅ | ✅ | SI / SLUB |

OLR: Optische Layouterkennung (Segmentierung)
OCR: Optische Zeichenerkennung
AS: Artikelseparierung (Strukturerkennung)

---

## Vorgehen bei Segmentierung

- Nutzung der Prozessoren aus OCR-D (hier [`eynollah`](https://github.com/qurator-spk/eynollah) und [`ocrd_segment`](https://github.com/OCR-D/ocrd_segment))
- Erkennung von:
  + Seitenrändern
  + Linien und Ornamentierung
  + Blocksegmentierung und Lesereihenfolge
  + Zeilensegmentierung
- Adäquate Evaluierung: für Aussage über Gesamtqualität der Texterkennung ist **Anteil des Segmentierungsfehlers** mit zu betrachten!

---

## Vorgehen bei Zeichenerkennung

- Nutzung der Werkzeuge und Workflows von OCR-D
- Nutzung von Multi-OCR-Alignierung zur weiteren Verbesserung der OCR-Qualität  
  (z.B. Diplopie-Problem bei Tesseract)
- [Training von eigenen Modellen für Obersorbisch](https://github.com/bertsky/hsbcala) (Fraktur + Antiqua),  
  aufbauend auf Community-Modellen (Tesseract / Calamari OCR)
- Erstellung von GT-Material (eigenes Repository für `hsb`)
    - [Transkription mit Aletheia](https://i.imgur.com/2kSDu1y.jpg)
    - [Transkription mit Larex](http://ocr.slub-dresden.de/Larex)
- iteratives Vorgehen Prozessierung – GT-Erstellung – Training  
  &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; ⬑──────────────────┘

---

## Iteratives Vorgehen

  1. Verbesserung der OCR-D-Werkzeuge und Workflows  
     (z.B. Binarisierung SBB)
  2. Nutzung existierender Modelle für die OCR
  3. Transkription von GT-Material
     (Level 2 nach [Richtlinien OCR-D / DFG](https://ocr-d.de/en/gt-guidelines/trans/))
     - neue Seiten
     - Finden und Beseitigen von Transkriptionsfehlern 
  4. Neutrainieren der OCR-Modelle, 
  5. Wiederholung und stetige Evaluierung an ausgewähltem GT-Material

<!-- Vorgehen iterativ: GT-Erzeugung auf Basis von Trainingsmodellen vorangegangener GT-Erzeugung -->

---

## Training und Evaluierung

<!-- Messungen -->

- Umfang der GT-Daten
  - Fraktur: &gt; 16.000 Zeilen (1843-1911)
  - Antiqua: &gt; 16.000 Zeilen (1880-1934, 1950-)
- [Training von Modellen](https://github.com/bertsky/hsbcala) für Tesseract / Calamari …
- Zeichenfehlerraten (CER) auf Test-GT:

|CER OCR|Abbyy Srv14* | Tesseract | hsb (Tess) | hsb (Cala) | hsb (multi) 
| ---------- | ---------- | -------- | ------------- |-------- |-------- |
|Fraktur**  | 14,72% | 9,01% |0.56% | 0.45%  | 0.37% |
|Antiqua   |  ***  | 2.17%   |  0.89%  | 0.52%    | 0.48% |


`*` Abbyy repräsentiert `ſ` als `s` (ca. 50-80% Fehleranteil)
`**` v.a. Überpunkt vs. Akut
`***` Stichproben mit Abbyy: bei Korrektur von ĕ (e breve) nach ě (e caron): < 1%


<!-- eventuell zweite Folie nur für Antiqua! -->
<!-- Ende RS-->

---

## Herausforderungen bei GT-Erstellung

- Lücken in Transkriptionsrichtlinien  
  z.B. **"** vs. **“** oder **—** vs. **–** oder **⸗** vs. **-** <!-- Zeichensetzung, auch Leerzeichen! -->
- zu wenige Beispiele für große Fonts und für spezifische Zeichen
- Wandel historischer Schreibweisen  
  z.B. am Übergang von Überpunkt zu Akut – Erkennung ob 
    - "Druckschwäche": 
      ![](https://i.imgur.com/I1lloVk.png =500x)
    - "gewollt" oder "beschränkter Drucksatz":
  ![](https://i.imgur.com/uH5DbMC.png =300x) ![](https://i.imgur.com/1Y3o6Ig.png =300x)

---

## Strukturerkennung – warum? 

**Ziel ist Artikelseparierung**
- Erstellung einer qual. hochwertigen Präsentation
- Artikelextraktion (in TEI) für Textkorpora
- siehe [Masterplan Zeitungsdigitalisierung](https://zeitschriftendatenbank.de//fileadmin/user_upload/ZDB/z/Masterplan.pdf), Stufe 3a Artikelseparierung

<!-- und wie machen wir das? -->

**Unser Workflow:**

<!-- und jetzt sind wir endlich hier hinten -->

![](https://i.imgur.com/pdnExJN.png)

<!-- Ende WB -->

---

## Strukturerkennung – was?

<!-- Basis ist Blockreihenfolge aus OCR-D  -->

- Seitenstruktur (Segmentierung + Reihenfolge): PAGE oder ALTO
- Dokumentstruktur (Titel, Kapitel, Abschnitt, Legende, Seitenzahl, Artikel):  
  Repräsentation…
  + nach **DFG-Anwendungsprofil** für METS/ALTO:  
    `mets:div/@LABEL` + `mets:structLink` (mit ALTO-fileGrp)  
    → ganze Seiten <!-- oft auch: max. 1 Eintrag pro Seite -->
  + nach **Europeana-Profil** für METS/ALTO:  
    `mets:div/mets:fptr` (ALTO-fileID) `./mets:area` (ALTO-IDREF)  
    → 1..n Segmente unterhalb+oberhalb von Seiten  

Anwendungsbeispiel: [Serbske Nowiny 23.3.1878 (DFG-Viewer)](http://digital.serbski-institut.de/ska-sn23031878_3u4)

---

## Strukturerkennung – wie?

<div class="col-container">
    <div class="col80">
        
- automatische Strukturerkennung:
  + [regelbasiert](https://github.com/OCR-D/ocrd_segment):  
    vorherige seitenweise Textblock-Lesereihenfolge + heuristische (visuell-textuelle) Artikelseparierung
  + [datengetrieben](https://github.com/CITlabRostock/citlab-article-separation-new):  
    neuronale Netze mit visuell-textueller Eingabe
<!-- Ende RS -->
- Unterstützung durch Präsentation: 
   + Kitodo/DFG-Viewer: bisher nur `mets:structLink`
   + [TEI-Konvertierung](https://github.com/slub/mets-mods2tei): bisher nur `mets:structLink`
   + kommerzielle Systeme: `mets:area` / beides
   + [DDB-Zeitungsportal](https://www.fiz-karlsruhe.de/de/forschung/ddb-zeitungsportal-v-20#projektdaten): noch offen 

    </div>
    <div class="col20">
    
    <img src="https://i.imgur.com/fG2Vvdf.jpg" width="200"/>
        
    (Bsp.: <a href="https://dokuwiki.digital-innsbruck.at/structify_archive">Structify</a>)

    </div>
</div>

---
##Volltext-Generierung bei Tageszeitung Nowa Doba (1947-1990) 
<div class="col-container">
    <div class="col80">
Nowa Doba
Workflow
![](https://hackmd.io/_uploads/S1J-bWky6.jpg)
Automatische Segmentierung
![](https://hackmd.io/_uploads/Hyzfb-kJp.jpg)
Automatische Reihenfolge Erkennung
![](https://hackmd.io/_uploads/SJ8yAg1yT.jpg)
Manuelle Korrektur der Reihenfolge
![](https://hackmd.io/_uploads/HkyxAekk6.jpg)
OCR und Post-OCR
![](https://hackmd.io/_uploads/H19l0ek1p.jpg)
Wörterbuch-Abgleich bei (manuell)
![](https://hackmd.io/_uploads/H1VveWy1p.jpg)
Automatische Überführung in TEI 1
![](https://hackmd.io/_uploads/HknPx-y16.jpg)
Manuelle Annotation nach TEI 2
![](https://hackmd.io/_uploads/S1Lv7-y16.jpg)
     
    </div>
</div>


---
## Fragen?

Vielen Dank für Ihre Aufmerksamkeit!

- wito.bejmak [[at]] serbski-institut.de
- robert.sachunsky [[at]] slub-dresden.de

https://hackmd.io/@bertsky/bibkon22-hsb-si-slub

---
---
# Many thanks for your attention!

<center>
<a href="https://wrznr.github.io/slide-template/">wrznr.github.io/slide-template</a>
</center>
