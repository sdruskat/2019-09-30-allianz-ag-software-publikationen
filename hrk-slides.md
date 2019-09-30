---
title:  'Software-Publikationen: <br/> Überblick, Herausforderungen, Bedarfe'
subtitle: 'Fachgespräch "Neue digitale Formate für die Forschung",<br/>Allianz-AG 8 "Wissenschaftspraxis",<br/>Bonn, Hochschulrektorenkonferenz, 2019-09-30'
author: 
    - '<em>Stephan Druskat</em> (Deutsches Zentrum für Luft- und Raumfahrt (DLR),<br/>Friedrich-Schiller-Universität Jena, Humboldt-Universität zu Berlin)<br/><img src="image/cc-by.png">'
theme: 'humboldt'
center: 'false'
slideNumber: 'true'
bibliography: 'literature.bib'
link-citations: no
revealjs-url: lib/revealjs/
mathjaxurl: 'lib/mathjax/MathJax.js'
aspectratio: 169
---

# Fachspezifika

## Linguistik - Formate

- **Papers, Monographien (inkl. z.B. Grammatiken & Wörterbücher), Konferenzbeiträge**

. . .

- Modelle [*d*]
- Datensätze (v.a. Korpora) aus analogen oder digitalen Quellen [*a/d*]
- Datenbanken (z.B. Treebanks, typologische Datenbanken) [*d*]
- Standards (z.B. Tagsets) [*a/d*]
- Software [*d*]
- technische Berichte (Annotationshandbücher, etc.) [*a/d*]
- Digitalisate (z.B. von Handschriften) [*d*]

allgemein nativ [*a*]nalog / nativ [*d*]igital

## Linguistik - Wahrnehmung und Nutzung digitaler Formate

- datengetriebene Teilbereiche (z.B. Korpuslinguistik, Computerlinguistik, Phonetik, moderne hist. Linguistik)
- Forschungsdaten sind zentral und werden auch so wahrgenommen
- Forschungssoftware ist zentral, wird aber nur teilweise so wahrgenommen (Computerlinguistik)

## Forschungssoftware - Qualitätssicherung

- analog zu Lebenswissenschaften
- softwaretechnische Qualitätssicherung: vs. Praxis (Fähigkeiten, Ressourcen, Anreize)
- wissenschaftliche Qualitätssicherung: nur über Metaformate (Papers)
- Validität sekundärer Qualitätssicherung?

## Forschungssoftware - Anerkennung und Gratifikation

::: {.center .large}
  
<br/><br/><br/>
Nein

:::

. . . 

::: {.center}

(bzw. kaum, v.a. sekundär via Paper)

:::

## Forschungssoftware - infrastrukturelle Unterstützung - Infrastrukturen

### z.B. CLARIN (ERIC)

- webbasierte Analysewerkzeuge: Nutzung?
- Virtual Language Observatory (Suchmaschine)

. . .

**Distribution (Publikation)? Vernetzung? Auswertung?**

## VLO

::: {.center}

<img src="image/annis.png" width="80%">

:::

## Forschungssoftware - infrastrukturelle Unterstützung - Infrastruktur

:::::::::::::: {.columns}
::: {.column width="75%"}

- Ausbildung?
- Karrierepfade?
- grundständige Finanzierung?
- softwarespezifische Infrastruktur (VCS, CI, etc.)?
- dedizierte Softwarerepositorien/-archive?
- (disziplinspezifische) Policies / Guidelines?
- zentrale Anlaufstellen?
- nicht-projektgebundene Softwaregruppen?

:::
::: {.column width="25%"}

- informell
- Nein
- kaum
- teilweise
- Nein/Zenodo
- Nein
- de-RSE
- kaum


:::

::::::::::::::




# Entwicklungs-, Steuerungs-, Reformbedarfe bzgl. Software-Publikationen

## State of the art

::: {.center}

<img src="image/zeller1.png" width="80%">

:::


## "Will an accepted paper increase the odds that people will use it?"

::: {.center}

<img src="image/zeller2.png" width="80%">

:::

## Publikationen

- "Document the details"
- "Link name to contribution"
- "Help advance careers"

## Was ist der Forschungsbeitrag?

- Paper?
- Service?
- Datenoutput?

. . .

- **Software!**
- "Document the details": Software ist "the details"
  - Code ist Dokumentation
  - (Softwaredokumentation ist Dokumentation)
- <span style="color: #009251;">**Bedarf$_1$: Kulturwandel**</span>

## Attribution

- "Link name to contribution"
- <span style="color: #009251;">**Bedarf$_2$: Metadaten**</span>
  - [Citation File Format (CFF)](https://citation-file-format.github.io) [@druskat_stephan_2018_1405679] - Autorenformat
  - [CodeMeta](https://codemeta.github.io) [@jonesCodeMetaExchangeSchema2017a] -<br/>Austauschformat
  - <span style="color: #009251;">Steuerungsbedarf:</span> Metadaten fordern
  - <span style="color: #009251;">Entwicklungsbedarf:</span> Metadaten in Publikationsplattformen integrieren

## Zitierung

- "Link name to contribution" + "Help advance careers"
- <span style="color: #009251;">**Bedarf$_3$: Zitierpraxis**</span>
  - neben allgemeinen - z.B. DFG Kodex 2019 [@deutscheforschungsgemeinschaftdfgLeitlinienZurSicherung2019] -
  spezifische Richtlinien und Policies für Herausgeber\*innen, Gutachter\*innen, Autor\*innen (derzeit entwickelt von [FORCE11 SCIWG](https://www.force11.org/group/software-citation-implementation-working-group) Guidance Task Force)
- <span style="color: #009251;">Steuerungsbedarf:</span> Evaluation inkl. Softwareveröffentlichungen
- Softwarezitierung hat zentrale Rolle für Reproduzierbarkeit
- <span style="color: #009251;">Entwicklungsbedarf:</span> Software muss eigene Referenzen zitieren (eigene Dissertation)

## Publikationsplattformen

:::::::::::::: {.columns}
::: {.column width="50%"}

- Journal of Open Source Software (JOSS) / Software Journals?
- Zenodo
  - DOI für Versionen
  - DOI für "Konzept"
  - Metadaten?
  - Peer Review?

:::
::: {.column width="50%"}

<img src="image/go.png">

:::
::::::::::::::

## Publikationsplattformen

- <span style="color: #009251;">**Bedarf$_4$: geeignete Publikationsplattformen, Auffindbarkeit**</span>
- <span style="color: #009251;">Entwicklungsbedarf:</span> wiss. Softwarearchiv mit PID, Versionen + Konzepten, (Zitations-)Metadaten; (Bibliotheken? NFDI?)
- <span style="color: #009251;">Entwicklungsbedarf:</span> Peer Review für Forschungssoftware; neue Rolle für Software Journals ohne Fließtextveröffentlichungen? 

## Karrierepfade

- "Help advance careers" - <span style="color: #009251;">**Bedarf$_5$: Karrierepfade**</span>
- Research Software Engineers analog zu wiss. Stellenbeschreibungen
- <span style="color: #009251;">Reformbedarf:</span> Grundlagen der Softwareentwicklung in Curricula
- <span style="color: #009251;">Reformbedarf:</span> Karrierepfade entwickeln und implementieren
- <span style="color: #009251;">Steuerungsbedarf:</span> (grundständige) Finanzierung softwarerelevanter Stellen, z.B. Grundsicherung durch Institutionen + Finanzierung durch Drittmittel
- <span style="color: #009251;">Steuerungsbedarf:</span> Einrichtung institutioneller RSE-Gruppen nach britischem Vorbild (?)

## Danke!

::: {.center}

### Was sind Ihre Fragen?

stephan.druskat@dlr.de  
Twitter: [\@stdruskat](http://twitter.com/stdruskat)  
ORCiD [0000-0003-4925-7248](https://orcid.org/0000-0003-4925-7248)  
vorstand@de-rse.org  
Folien: [doi:10.6084/m9.figshare.9918653](https://doi.org/10.6084/m9.figshare.9918653)

:::

# Appendix

## Referenzen 