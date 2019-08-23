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

# Kontrastierende Erklärungen verwenden relevante positive und relevante negative Werte.
{: #ie-pp-pn}

Bei kontrastiven Erklärungen zeigt {{site.data.keyword.aios_short}} immer relevante positive und relevante negative Werte an. 
{: shortdesc}

- Relevante positive Werte sind die Ergebnisse, die bei der Ermittlung eines Gegenstands oder Sachverhalts von entscheidender Bedeutung sind.
- Relevante negative Werte sind die Nicht-Ergebnisse, die durch ihre Abwesenheit von Bedeutung sind.

{{site.data.keyword.aios_short}} zeigt immer einen relevanten positiven Wert an, in einigen Fällen werden jedoch keine relativen negativen Werte angezeigt. In diesem Fall sind Werte für das jeweilige Merkmal entweder bereits gemittelt oder die Vorhersage hat sich durch das Entfernen von Werten vom Mittelwert nicht geändert.

Dies ist leichter zu verstehen, wenn man bedenkt, dass {{site.data.keyword.aios_short}} beim Berechnen des relativen negativen Werts die Werte aller Merkmale vom zugehörigen Mittelwert entfernt werden. Bei relevanten negativen Werten handelt es sich dabei um die Merkmalwerte, die am weitesten vom Mittelwert entfernt sind. Befinden sich die Werte eines Datenpunkts bereits auf dem Mittelwert oder ändert sich die Vorhersage auch nach dem Ändern des Werts in einen vom Mittelwert entfernten Wert nicht, gibt es keine relativen negativen Werte, die anzuzeigen sind. Im Hinblick auf relevante positive Werte findet {{site.data.keyword.aios_short}} die maximale Änderung bei den Merkmalwerten nahe dem Mittelwert, sodass sich die Vorhersage nicht ändert. Dies bedeutet in der Praxis, dass es fast immer einen relevanten positiven Wert gibt, der eine Transaktion erklärt.

