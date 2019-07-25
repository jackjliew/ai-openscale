---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Microsoft Azure studio, ml, machine learning, services, studio

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

# Microsoft Azure ML Studio-Instanz angeben
{: #connect-azure}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Microsoft Azure ML Studio-Instanz an. In der Azure ML Studio-Instanz werden die AI-Modelle und -Bereitstellungen gespeichert.
{: shortdesc}

Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Microsoft Azure-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-azbind).

## Verbindung zu Azure ML Studio-Instanz herstellen
{: #ca-connect}

{{site.data.keyword.aios_short}} stellt eine Verbindung zu AI-Modellen und -Bereitstellungen in einer Azure ML Studio-Instanz her.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** auf **Machine Learning-Anbieter**.

    ![Die Anzeige für die Auswahl des Machine Learning-Anbieters mit Kacheln für die unterstützten Machine Learning-Engines wird angezeigt.](images/wos-machine-learning-providers-selection.png)

1.  Klicken Sie auf die Kachel **Microsoft Azure ML Studio**.

    ![Azure ML Studio-Berechtigungsnachweise eingeben](images/connect-azure-cred.png)

1.  Geben Sie Ihre Berechtigungsnachweise ein und speichern Sie sie:

    - Client-ID: Der tatsächliche Zeichenfolgewert Ihrer Client-ID, der Ihre Identität nachweist und Ihre Azure Studio-Aufrufe authentifiziert und autorisiert.
    - Geheimer Clientschlüssel: Der tatsächliche Zeichenfolgewert Ihres geheimen Clientschlüssels, der Ihre Identität nachweist und Ihre Azure Studio-Aufrufe authentifiziert und autorisiert.
    - Tenant: Ihre Tenant-ID entspricht Ihrem Unternehmen und stellt eine dedizierte Azure AD-Instanz dar. Ermitteln Sie die Tenant-ID, indem Sie den Mauszeiger über Ihrem Kontonamen bewegen, um die Verzeichnis-/Tenant-ID zu erhalten, oder wählen Sie Azure Active Directory > Eigenschaften > Verzeichnis-ID im Azure-Portal aus.
    - Abonnement-ID: Abonnementberechtigungsnachweise, die Ihr Microsoft Azure-Abonnement eindeutig kennzeichnen. Die Abonnement-ID ist ein Bestandteil der URI für die einzelnen Serviceaufrufe.

    Anweisungen dazu, wie Sie Ihre Berechtigungsnachweise für Microsoft Azure beziehen, finden Sie in der zugehörigen Dokumentation unter [How to: Use the portal to create an Azure AD application and service principal that can access resources](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-create-service-principal-portal){: external}.
    {: note}

1.  In {{site.data.keyword.aios_short}} sind die bereitgestellten Modelle aufgelistet. Wählen Sie die Modelle aus, die Sie überwachen möchten, und klicken Sie auf **Konfigurieren**.

Sie haben erfolgreich Bereitstellungen ausgewählt.

### Weitere Schritte
{: #ca-next}

Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
