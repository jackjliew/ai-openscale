---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## IAM-Rollen und Aktionen (IAM = Identity and Access Management)

Der Zugriff auf {{site.data.keyword.aios_full}}-Serviceinstanzen für Benutzer in Ihrem Konto wird von {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM) gesteuert. Jedem Benutzer, der auf den {{site.data.keyword.aios_short}}-Service in Ihrem Account zugreift, muss eine Zugriffsrichtlinie mit einer definierten IAM-Rolle zugeordnet werden. Die Richtlinie bestimmt, welche Aktionen ein Benutzer im Kontext des ausgewählten Service oder der ausgewählten Instanz ausführen kann. Die zulässigen Aktionen werden durch den {{site.data.keyword.Bluemix_notm}}-Service angepasst und als Operationen definiert, die für den Service ausgeführt werden dürfen. Anschließend werden die Aktionen IAM-Benutzerrollen zugeordnet.

Richtlinien ermöglichen das Erteilen von Zugriffsberechtigungen auf verschiedenen Ebenen. Zu den Optionen gehören unter anderem die folgenden Ebenen: 

* Zugriff für alle Instanzen des Service in Ihrem Konto
* Zugriff auf eine einzelne Serviceinstanz in Ihrem Konto
* Zugriff auf eine bestimmte Ressource in einer Instanz

Nach dem Definieren des Geltungsbereichs der Zugriffsrichtlinie ordnen Sie eine Rolle zu, die die Zugriffsebene des Benutzers bestimmt. Die folgenden Tabellen enthalten Erläuterungen zu den Aktionen, die die einzelnen Rollen innerhalb des {{site.data.keyword.aios_short}}-Service ermöglichen.

Mit Plattformmanagementrollen können Benutzern unterschiedliche Berechtigungsstufen für die Ausführung von Plattformaktionen innerhalb des Kontos und für einen Service zugeordnet werden. Die für Katalogressourcen zugeordneten Plattformmanagementrollen ermöglichen Benutzern beispielsweise Aktionen wie das Erstellen, Löschen, Bearbeiten und Anzeigen von Serviceinstanzen auszuführen. Die Plattformmanagementrollen, die den Kontomanagementservices zugeordnet sind, ermöglichen es Benutzern, Aktionen wie das Einladen und Entfernen von Benutzern, das Arbeiten mit Ressourcengruppen und das Anzeigen von Abrechnungsinformationen auszuführen. Weitere Informationen zu den Kontomanagementservices finden Sie im Abschnitt [Zugriff auf Kontomanagementservices zuordnen](/docs/iam?topic=iam-account-services#account-services){: external}.

Wählen Sie beim Erstellen einer Richtlinie alle relevanten Rollen aus. Jede Rolle ermöglicht das Ausführen separater Aktionen und übernimmt keine Aktionen von Rollen mit niedrigeren Berechtigungsstufen.
{: tip}

Die folgende Tabelle enthält Beispiele für einige Plattformmanagementaktionen, die Benutzer im Kontext von Katalogressourcen und Ressourcengruppen ausführen können. In der Dokumentation zu den einzelnen Katalogangeboten wird erläutert, wie die Rollen im Kontext des jeweils verwendeten Service auf Benutzer angewendet werden.


|  | Einer oder alle IAM-fähigen Services | Ausgewählter Service in einer Ressourcengruppe | Ausgewählte Ressourcengruppe |
|:--------------|:------------|:-------------|:-------------|
| Anzeigeberechtigter | Instanzen, Aliasse, Bindungen und Berechtigungsnachweise anzeigen | Nur angegebene Instanzen in der Ressourcengruppe anzeigen | Ressourcengruppe anzeigen |
| Operator |  Instanzen anzeigen und Aliasse, Bindungen und Berechtigungsnachweise verwalten |  Nicht zutreffend | Nicht zutreffend |
| Bearbeiter |  Instanzen erstellen, löschen, bearbeiten und anzeigen. Aliasse, Bindungen und Berechtigungsnachweise verwalten | Ausschließlich angegebene Instanzen in der Ressourcengruppe erstellen, löschen, bearbeiten, aussetzen, wiederaufnehmen, anzeigen und binden | Namen der Ressourcengruppe anzeigen und bearbeiten |
| Administrator |  Alle Verwaltungsaktionen für Services | Alle Verwaltungsaktionen für die angegebenen Instanzen in der Ressourcengruppe | Zugriff auf die Ressourcengruppe anzeigen, bearbeiten und verwalten |
| Clusteradministrator (nur für {{site.data.keyword.wos4d_full}} vorgesehen) |  Vollständiger Zugriff auf die Plattform IBM Cloud Private | Vollständiger Zugriff auf die angegebenen Instanzen in der Ressourcengruppe | Die folgenden Aktionen können nur vom Clusteradministrator ausgeführt werden: Verbindung zu einem LDAP-Verzeichnis herstellen, Benutzer hinzufügen und IAM-Rollen zuordnen, Workloads, Infrastruktur und Anwendungen in allen Namensbereichen verwalten, Namensbereiche erstellen, Kontingente zuordnen, Sicherheitsrichtlinien für Pods hinzufügen, internes Helm-Repository hinzufügen, internes Helm-Repository löschen, Helm-Diagramme zum internen Helm-Repository hinzufügen, Helm-Diagramme im internen Helm-Repository entfernen und interne und externe Helm-Repositorys synchronisieren. |
{: row-headers}
{: class="comparison-table"}
{: caption="Tabelle 1. Beispiele für Plattformmanagementrollen und Aktionen für Services in einem Konto" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


Für Service-Zugriffsrollen, die Benutzern den Zugriff auf {{site.data.keyword.aios_short}} sowie den Aufruf der REST-API ermöglichen, greift {{site.data.keyword.aios_short}} auf die Plattformmanagementrollen in der vorherigen Tabelle zurück. Informationen zum Zuordnen von Benutzerrollen in der Benutzerschnittstelle finden Sie im Abschnitt [Zugriff auf Ressourcen verwalten](/docs/iam?topic=iam-iammanidaccser#iammanidaccser){: external}.

 
