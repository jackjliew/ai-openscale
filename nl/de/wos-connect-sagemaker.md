---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Amazon SageMaker ML-Serviceinstanz angeben
{: #csm-connect}

Als ersten Schritt im {{site.data.keyword.aios_short}}-Tool geben Sie eine Amazon SageMaker-Serviceinstanz an. In Ihrer Amazon SageMaker-Serviceinstanz speichern Sie Ihre AI-Modelle und -Bereitstellungen.
{: shortdesc}

Sie können Ihren Machine-Learning-Anbieter auch mithilfe des Python-SDK hinzufügen. Wenn Sie diesen Schritt programmgesteuert ausführen möchten, finden Sie weitere Informationen in [Bindung für Amazon SageMaker-Machine Learning-Engine erstellen](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Verbindung zur Amazon SageMaker-Serviceinstanz herstellen
{: #csm-config}

{{site.data.keyword.aios_short}} stellt die Verbindung zu AI-Modellen und Bereitstellungen in einer Amazon SageMaker-Serviceinstanz her.

1.  Klicken Sie auf der Registerkarte **Konfigurieren** auf **Machine Learning-Anbieter**. 

    ![Die Anzeige für die Auswahl des Machine Learning-Anbieters mit Kacheln für die unterstützten Machine Learning-Engines wird angezeigt.](images/wos-machine-learning-providers-selection.png)

1.  Klicken Sie auf die Kachel **Amazon SageMaker**. 

    ![Berechtigungsnachweise für Amazon SageMaker-Service eingeben](images/connect-sage-cred.png)

1.  Geben Sie Ihre Berechtigungsnachweise ein und speichern Sie sie: 

    - Zugriffsschlüssel-ID: Ihre AWS-Zugriffsschlüssel-ID, `aws_access_key_id`, die Sie identifiziert und Ihre AWS-Aufrufe authentifiziert und autorisiert. 
    - Geheimer Zugriffsschlüssel: Ihr geheimer AWS-Zugriffsschlüssel, `aws_secret_access_key`, der erforderlich ist, um Ihre Identität zu verifizieren und Ihre AWS-Aufrufe zu authentifizieren und zu autorisieren. 
    - Region: Geben Sie die Region ein, in der Ihre Zugriffsschlüssel-ID erstellt wurde. Schlüssel werden in der Region gespeichert und verwendet, in der sie erstellt wurden, und können nicht an eine andere Region übertragen werden. 

1.  In {{site.data.keyword.aios_short}} sind die bereitgestellten Modelle aufgelistet. Wählen Sie die Modelle aus, die Sie überwachen möchten. 

### Weitere Schritte
{: #csm-next}

Nun können Sie in {{site.data.keyword.aios_short}} die [Überwachungen konfigurieren](/docs/services/ai-openscale?topic=ai-openscale-mo-config). 
