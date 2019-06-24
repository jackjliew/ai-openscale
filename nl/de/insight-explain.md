---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Transaktionen erklären
{: #ie-ov}

Für jede Bereitstellung können Sie Erklärungsdaten für bestimmte Transaktionen anzeigen.
{: shortdesc}

## Transaktionen erklären
{: #ie-view}

Wählen Sie in der Kachel für die ausgewählte Bereitstellung im Navigator die Registerkarte **Transaktion erklären** (![Registerkarte 'Transaktion erklären'](images/insight-transact-tab.png)) aus und geben Sie eine Transaktions-ID ein.

Wann immer Daten zwecks Scoring an das Modell gesendet werden, legt es eine Transaktions-ID im HTTP-Header fest, indem es das Feld `X-Global-Transaction-Id` entsprechend angibt. Diese Transaktions-ID wird in der Nutzdatentabelle gespeichert. Wenn Sie eine Erklärung des Modellverhaltens für ein bestimmtes Scoring suchen, geben Sie die Transaktions-ID an, die dieser Scoring-Anforderung zugeordnet ist. Beachten Sie bitte, dass dieses Verhalten nur Watson Machine Learning-Transaktionen (WML-Transaktionen) betrifft und nicht für andere Transaktionen (Nicht-WML-Transaktionen) gilt.
{: note}

### Transaktions-ID in {{site.data.keyword.aios_short}} suchen
{: #ie-find}

1.  Verschieben Sie die Markierung im Zeitdiagramm für Ihre Bereitstellung über das Diagramm und klicken Sie auf den Link **Details anzeigen**, um eine [Visualisierung von Daten eine bestimmte Uhrzeit](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet) anzuzeigen.
1.  Klicken Sie auf die Schaltfläche **Transaktionen anzeigen**, um die [Liste der Transaktions-IDs anzuzeigen](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Kopieren Sie eine der Transaktions-IDs aus der Liste, fügen Sie sie in das Suchfeld auf der Seite **Transaktion erklären** ein und drücken Sie die Eingabetaste.

    Die Liste der Transaktions-IDs bietet auch die Möglichkeit, für eine beliebige Transaktions-ID in der Spalte 'Aktion' einfach auf den Link **Erklären** zu klicken, woraufhin diese Transaktion in der Registerkarte 'Erklärbarkeit' geöffnet wird.
    {: note}

  Die den folgenden Abschnitten enthalten Beispiele für Erklärungen zu verschiedenen Modelltypen.

  ![Transaktions-ID für Erklärbarkeit](images/insight-explain-trans-id.png)

## Beispiel eines kategorialen Modells
{: #ie-class}

Dieses Beispiel für Erklärbarkeit bezieht sich auf ein binäres Klassifikationsmodell, das Versicherungsansprüche freigibt oder ablehnt. Sie können die Faktoren sehen, die in diesem Fall positiv oder negativ zum Endergebnis `ABGELEHNT` beigetragen haben.

Das Merkmal *ALTER POLICE* mit dem Wert `< 1 year` übte den größten Einfluss auf die Entscheidung des Modells zugunsten von ABGELEHNT als Ergebnis aus. Die anderen Merkmale, die zu diesem Ergebnis beigetragen haben, waren *SCHADENSHÄUFIGKEIT* (`Hoch`) und *ALTER* (`18`), wobei *FAHRZEUGWERT* (`$50,000`) nur einen geringfügigen Einfluss hatte.

![Erklärbarkeit bei binärer Klassifikation](images/insight-explain-binary.png)

Die Diagramme sind zwar nützlich zur Darstellung der wichtigsten Faktoren bei der Bestimmung des Ergebnisses einer Transaktion, doch Klassifikationsmodelle können auch erweiterte Erklärungen enthalten, die in den Abschnitten `Mindeständerungen für Ergebnis 'Genehmigt'` und `Mindeständerungen für dieses Ergebnis` detailliert beschrieben sind.

Erweiterte Erklärungen stehen nicht für Regressions- oder Imagemodelle und Modelle für unstrukturierten Text zur Verfügung.
{: note}

`Mindeständerungen für Ergebnis 'Genehmigt'` besagt, dass sich die Vorhersage des Modells ändern würde, wenn die Werte der Merkmale in die in diesem Abschnitt aufgeführten Werte geändert würden.

`Mindeständerungen für dieses Ergebnis` besagt hingegen, dass sich die Vorhersage des Modells nicht ändern würde, selbst wenn die Werte der Merkmale in die in diesem Abschnitt aufgeführten Werte geändert würden.

Diese beiden Werte geben Auskunft über das Verhalten des Modells im Umkreis des Datenpunktes mit, für den die Erklärung generiert wird.

![Erklärbarkeit bei binärer Klassifikation](images/insight-explain-binary2.png)

## Beispiel eines Imagemodells
{: #ie-image}

Als Beispiel der Erklärbarkeit bei einem Imageklassifikationsmodell können Sie sehen, welche Teile eines Images positiv zum vorhergesagten Ergebnis beigetragen haben und welche negativ. Im unten gezeigten Anschauungsbeispiel zeigt das rechte Image die Teile, die sich positiv auf die Vorhersage ausgewirkt haben, und das linke Image die Teile von Images, die sich negativ auf das Ergebnis ausgewirkt haben.

- Für {{site.data.keyword.pm_full}} können die Nutzdaten mit den durch Perturbation veränderten Images, die über das Machine Learning-Gateway gesendet werden, ein Volumen von 1 MB nicht überschreiten. Um Probleme aufgrund von Zeitlimitüberschreitungen zu vermeiden, dürfen Images nicht mehr als 125 x 125 Pixel aufweisen und sie müssen nacheinander gesendet werden, damit die Erklärung für das zweite Image angefordert wird, nachdem die erste abgeschlossen ist.
{: note}

![Erklärbarkeit bei Imageklassifikation](images/insight-explain-image.png)

## Beispiel eines Modells für unstrukturierten Text
{: #ie-unstruct}

Dieses Beispiel der Erklärbarkeit zeigt ein Klassifikationsmodell, das unstrukturierten Text auswertet. Die Erklärung zeigt die Schlüsselwörter an, die sowohl einen positiven als auch einen negativen Einfluss auf die Modellvorhersage hatten. Außerdem wird die Position der ermittelten Schlüsselwörter auch im Originaltext angezeigt, der dem Modell als Eingabe zugeführt wurde.

![Erklärbarkeit bei Imageklassifikation](images/insight-explain-text.png)
