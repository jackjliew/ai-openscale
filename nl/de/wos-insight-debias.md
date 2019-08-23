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

# Optionen für die Verzerrungsbereinigung
{: #it-dbo}

{{site.data.keyword.aios_short}} verwendet zwei Typen von Verzerrungsbereinigung: passive und aktive Bereinigung. Bei der passiven Verzerrungsbereinigung erfahren Sie, welche Verzerrung vorlag, während die aktive Verzerrungsbereinigung durch eine Echtzeitänderung des Modells für die aktuelle Anwendung verhindert, dass sich die Verzerrung fortsetzt.

- *Passive Verzerrungsbereinigung* - Passive Verzerrungsbereinigung wird von OpenScale automatisch jede Stunde ausgeführt. Diese Bereinigung wird als passiv bezeichnet, da sie ohne Benutzereingriff erfolgt. Im Rahmen der Verzerrungsprüfung führt {{site.data.keyword.aios_short}} auch eine Verzerrungsbereinigung der Daten durch, indem das Verhalten des Modells analysiert und die Daten ermittelt werden, bei denen das Modell eine Verzerrung aufweist.

  {{site.data.keyword.aios_short}} erstellt dann ein Machine Learning-Modell, um vorherzusagen, ob das Modell an einem bestimmten neuen Datenpunkt wahrscheinlich auf verzerrte Weise reagieren wird. Anschließend analysiert {{site.data.keyword.aios_short}} die Daten, die vom Modell empfangen werden, stündlich und sucht die Datenpunkte, an denen {{site.data.keyword.aios_short}} meint, ein verzerrtes Verhalten feststellen zu können. Für derartige Datenpunkte wird der Wert des Attributs 'Fairness' durch Perturbation (Störung) von 'Minderheit' in 'Mehrheit' geändert und die durch Perturbation gestörten Daten werden zur Vorhersage an das ursprüngliche Modell gesendet. Diese Vorhersage des Originalmodells wird als verzerrungsbereinigte Ausgabe verwendet.

  {{site.data.keyword.aios_short}} führt diese Verzerrungsbereinigung stündlich für alle Daten durch, die in der letzten Stunde vom Modell empfangen wurden. Es berechnet auch die Fairness für die verzerrungsbereinigte Ausgabe und zeigt sie auf der Registerkarte **Verzerrungsbereinigtes Modell** an.

- *Aktive Verzerrungsbereinigung* - Die aktive Verzerrungsbereinigung stellt eine Möglichkeit dar, verzerrungsbereinigte Ergebnisse über den REST-API-Endpunkt anzufordern und in Ihre Anwendung aufzunehmen. Sie weisen {{site.data.keyword.aios_short}} aktiv an, eine Verzerrungsbereinigung durchzuführen und das Modell zu ändern, damit Sie Ihre Anwendung ohne Verzerrung ausführen können. Bei der aktiven Verzerrungsbereinigung können Sie von Ihrer Anwendung aus einen REST-API-Endpunkt für Verzerrungsbereinigung einsetzen. Dieser REST-API-Endpunkt ruft Ihr Modell intern auf und prüft dessen Verhalten.

  Wenn {{site.data.keyword.aios_short}} erkennt, dass das Modell ein verzerrtes Verhalten aufweist, verändert es die Daten wie zuvor erwähnt durch Perturbation und sendet sie dann an das ursprüngliche Modell zurück. Die Ausgabe des ursprünglichen Modells für die durch Perturbation gestörten Daten wird als die verzerrungsbereinigte Vorhersage zurückgegeben. Wenn {{site.data.keyword.aios_short}} feststellt, dass das ursprüngliche Modell nicht verzerrt handelt, gibt {{site.data.keyword.aios_short}} die Vorhersage des ursprünglichen Modells als verzerrungsbereinigte Vorhersage zurück. Durch die Verwendung dieses REST-API-Endpunkts können Sie also sicherstellen, dass Ihre Anwendung keine Entscheidungen trifft, die auf einer verzerrten Ausgabe Ihrer Modelle basieren.

Wählen Sie den Link **Verzerrungsbereinigten Scoring-Endpunkt anzeigen** aus, um Ihren verzerrungsbereinigten REST-API-Endpunkt zu ermitteln.

![Darstellung der Detailanzeige von 'Verzerrungsbereinigter API-Endpunkt', mit cURL-Beispiel, das im Feld mit dem Code-Snippet angezeigt wird](images/insight-debias-api.png)

## Weitere Schritte
{: #it-dbo-nextsteps}

- Zur Minderung der Verzerrung, nachdem diese festgestellt wurde, müssen Sie eine neue Version des Modells erstellen, durch die das Problem behoben wird. {{site.data.keyword.aios_short}} speichert verzerrte Datensätze in der Liste mit manuellen Kennzeichnungen. Diese verzerrten Datensätze müssen manuell gekennzeichnet werden; danach muss das Modell mithilfe dieser zusätzlichen Daten erneut trainiert werden, um eine neue Version des Modells zu erstellen, die unverzerrt ist.


