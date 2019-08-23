---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Erklärung eines kategorialen Modells
{: #ie-class}

Dieses Beispiel für Erklärbarkeit bezieht sich auf ein binäres Klassifizierungsmodell, das Versicherungsansprüche freigibt oder ablehnt. Sie können die Faktoren sehen, die in diesem Fall positiv oder negativ zum Endergebnis `ABGELEHNT` beigetragen haben.
{: shortdesc}

Das Merkmal *ALTER POLICE* mit dem Wert `<ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceyear` übte den größten Einfluss auf die Entscheidung des Modells zugunsten von ABGELEHNT als Ergebnis aus. Die anderen Merkmale, die zu diesem Ergebnis beigetragen haben, waren *SCHADENSHÄUFIGKEIT* (`Hoch`) und *ALTER* (`18`), wobei *FAHRZEUGWERT* (`$50,000`) nur einen geringfügigen Einfluss hatte.

![Darstellung der Erklärbarkeit bei binärer Klassifizierung mit Details zu abgelehnten und bewilligten Ansprüchen](images/insight-explain-binary.png)

Die Diagramme sind zwar nützlich zur Darstellung der wichtigsten Faktoren bei der Bestimmung des Ergebnisses einer Transaktion, doch Klassifizierungsmodelle können auch erweiterte Erklärungen enthalten, die in den Abschnitten `Mindeständerungen für Ergebnis 'Genehmigt'` und `Mindeständerungen für dieses Ergebnis` detailliert beschrieben sind.

Erweiterte Erklärungen stehen nicht für Regressions- oder Imagemodelle und Modelle für unstrukturierten Text zur Verfügung.
{: note}

`Mindeständerungen für Ergebnis 'Genehmigt'` besagt, dass sich die Vorhersage des Modells ändern würde, wenn die Werte der Merkmale in die in diesem Abschnitt aufgeführten Werte geändert würden.

`Mindeständerungen für dieses Ergebnis` besagt hingegen, dass sich die Vorhersage des Modells nicht ändern würde, selbst wenn die Werte der Merkmale in die in diesem Abschnitt aufgeführten Werte geändert würden.

Diese beiden Werte geben Auskunft über das Verhalten des Modells im Umkreis des Datenpunktes mit, für den die Erklärung generiert wird.

![Details zur Erklärbarkeit bei binärer Klassifizierung mit minimalen Änderungen, die nötig wären, um andere Ergebnisse zu erhalten](images/insight-explain-binary2.png)
