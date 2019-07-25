---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:download: .download}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Fairness für eine Gruppe
{: #quality_group}

Die Fairness gibt als Gruppenmetrik die Neigung des Modells an, günstige Ergebnisse an andere Gruppe zu übergeben. Bei einer Gruppe kann es sich z. B. um eine Altersgruppe, eine dem Geschlecht nach gebildete Gruppe oder eine Ethnie handeln.
{: shortdesc}


## Fairness bei Gruppen - auf einen Blick
{: #quality_group-glance}

- **Beschreibung**: Die Neigung des Modells, günstige Ergebnisse für eine Gruppe gegenüber einer anderen Gruppe zu liefern.
- **Standardschwellenwerte**: Unterer Grenzwert = 80 %
- **Standardempfehlung**: Der verzerrungsbereinigte Scoring-Endpunkt, den Sie in Ihrer Geschäftsanwendung verwenden können, um verzerrungsbereinigte Antworten vom bereitgestellten Modell zu erhalten.
- **Problemtyp**: Alle
- **Datentyp**: Strukturiert
- **Diagrammwerte**: Letzter Wert im Zeitrahmen
- **Verfügbare Metrikdetails**: Ja

## Geschützte Attribute
{: #quality_group-atts}

{{site.data.keyword.aios_short}} erkennt automatisch, ob bekannte geschützte Attribute in einem Modell vorliegen. Werden derartige Attribute von {{site.data.keyword.aios_short}} erkannt, wird automatisch die Konfiguration einer Verzerrungsüberwachung für die einzelnen Attribute empfohlen, um sicherzustellen, dass die Verzerrung bei diesen möglicherweise schutzwürdigen Attributen in der Produktionsumgebung verfolgt wird. 

### Geschlecht (sex)
{: #quality_group-sex}

{{site.data.keyword.aios_short}} empfiehlt, im Attribut für **Geschlecht** die Werte für `Frau` (Woman) und `Nicht-binär` (Non-Binary) als zu überwachende Werte und `Mann` (Male) als Referenzwert für die Verzerrungsüberwachung zu konfigurieren. 

### Ethnizität (ethnicity)
{: #quality_group-ethnicity}

{{site.data.keyword.aios_short}} empfiehlt, im Attribut für **Ethnizität** den Wert für `weiß` (White-caucasian) als Referenzwert und andere Ethnien als zu überwachende Werte für die Verzerrungsüberwachung zu konfigurieren. 

### Familienstand (marital status)
{: #quality_group-marital}

{{site.data.keyword.aios_short}} empfiehlt, im Attribut für **Familienstand** den Wert für `verheiratet` (married) als Referenzwert und `ledig` (single) als zu überwachenden Wert für die Verzerrungsüberwachung zu konfigurieren. 

### Alter (age)
{: #quality_group-age}

{{site.data.keyword.aios_short}} empfiehlt, im Attribut für **Alter** die Verzerrungsüberwachung so zu konfigurieren, dass die verschiedenen Altersgruppen eine umsetzbare Verzerrungsbereinigung ermöglichen. 

### Postleitzahl (zip code)
{: #quality_group-zip}

{{site.data.keyword.aios_short}} empfiehlt, im Attribut für **Postleitzahl** die Verzerrungsüberwachung so zu konfigurieren, dass ein Scoring für die einzelnen Postleitzahlen durchgeführt wird.
