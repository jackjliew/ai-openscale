---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: supported frameworks, models, model types, limitations, limits

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
{:external: target="_blank" .external}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# Bekannte Probleme und Einschränkungen für {{site.data.keyword.aios_short}}
{: #rn-12ki}

In der folgenden Liste werden die bekannten Probleme und Einschränkungen für {{site.data.keyword.aios_full}} und {{site.data.keyword.wos4dfull}} aufgeführt.
{: shortdesc}

<p>&nbsp;</p>

## Einschränkungen
{: #wos-limitations}

- {{site.data.keyword.aios_short}} unterstützt die Verwendung mehrerer Machine Learning-Engines, sofern Sie die zusätzlichen Engines über das Python-SDK konfigurieren.

- Das aktuelle Release unterstützt nur eine Datenbank, eine {{site.data.keyword.pm_full}}-Instanz und eine Instanz von {{site.data.keyword.aios_short}}.

- Die Datenbank und die {{site.data.keyword.pm_full}}-Instanz müssen in demselben {{site.data.keyword.cloud_notm}}-Konto bereitgestellt werden.

- Für den kostenlosen Lite-Plan gelten die folgenden monatlichen Grenzwerte:

    - Überwachung von zwei bereitgestellten Modellen
    - Erklärung von 20 Transaktionen
    - 50.000 Datensätze für Nutzdaten (kumulativ)
    - 50.000 Rückmeldedatensätze (kumulativ)

- {{site.data.keyword.aios_short}} verwendet eine PostgreSQL- oder Db2-Datenbank zum Speichern modellbezogener Daten (Rückmeldedaten, Scoring-Nutzdaten) und berechneter Metriken. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt.

- Für Lizenzen gilt ein Grenzwert von 20 bereitgestellten Modellen pro Instanz von {{site.data.keyword.aios_short}}.

- Für {{site.data.keyword.pm_full}} kann die Scoring-Eingabe für Imageklassifizierungsmodelle, die zur Nutzdatenprotokollierung gesendet werden, eine Größe von 1 MB nicht überschreiten. Um Probleme aufgrund von Zeitlimitüberschreitungen zu vermeiden, dürfen Images nicht mehr als 125 x 125 Pixel aufweisen und sie müssen nacheinander gesendet werden, damit die Erklärung für das zweite Image angefordert wird, nachdem die erste abgeschlossen ist.

- Die Datenbank für den kostenlosen Lite-Plan ist nicht DSGVO-konform. Wenn in Ihrem Modell personenbezogene Daten verarbeitet werden, dann müssen Sie eine neue Datenbank kaufen oder eine bereits vorhandene Datenbank verwenden, die DSGVO-konform ist. 

- Die Erklärbarkeit wird bei Modellen mit unstrukturiertem Text nicht für fortlaufende Scriptsprachen wie Japanisch, Chinesisch und Koreanisch, bei denen keine Leerzeichen oder Punktuationszeichen zum Trennen von Wörtern verwendet werden, unterstützt.



<p>&nbsp;</p>

## Gängige Probleme
{: #wos-common-issues}

Die folgenden Probleme treten sowohl bei {{site.data.keyword.aios_full}} unter {{site.data.keyword.Bluemix}} als auch bei {{site.data.keyword.wos4d_full}} auf.

<p>&nbsp;</p>

### Fehler bei der Driftkonfiguration verhindern die Konfiguration der Driftüberwachung
{: #wos-common-issues-mismatchdatatype}

Die hohe Flexibilität der Modellkonfigurationsanzeige kann zu Problemen bei der späteren Überwachungskonfiguration führen, z. B. bei der Konfiguration der Drifterkennungsüberwachung. Da Sie die Datentypen auswählen können, müssen Sie sicherstellen, dass Ihre Auswahl dem Wesen des Modells entspricht. Eine Fehlernachricht mit dem folgenden Inhalt kann auftreten, wenn für die Vorhersagespalte nicht der richtige Typ ausgewählt wurde:

```
"error": AIQDS2003E",
"message": "Die Modellvorhersagen '[0. 1.]' unterscheiden sich von Klassennamen in Trainingsdaten '[ 'No' 'Yes'] ' für das Abonnement < <Nummer > > in Datamart < <Datamart-ID> > und Servicebindung < <Bindungs-ID> >.
```

Ursache sind in der Regel die folgenden Fälle:

- Die Kennzeichnung für `class` weist den Typ 'String' auf und die Modellierungsrolle (`modeling_role`) für Vorhersage (**prediction**) ist der Spalte für **Vorhersage** als Datentyp 'double' zugeordnet, da dies der Definition des Ausgabedatenschemas entspricht.
- Sie wählen die Spalte für **Vorhersage** des Datentyps 'Double' in der Benutzerschnittstelle aus, der keine Einschränkungen aufweist.


### Nutzdatenformate
{: #wos-common-issues-payloadformat}

Im Hinblick auf eine ordnungsgemäße Verarbeitung der Nutzdatenanalyse werden von {{site.data.keyword.aios_short}} keine Spaltennamen mit Anführungszeichen (") in den Nutzdaten unterstützt. Dies betrifft sowohl Scoring-Nutzdaten als auch Feedbackdaten im CSV- und im JSON-Format.

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- Von den beiden Arten von Azure Machine Learning-Web-Services wird von {{site.data.keyword.aios_short}} nur der Typ `Neu` unterstützt. Der Typ `Klassisch` wird nicht unterstützt.

- __*Standardeingabename muss verwendet werden*__: Im Azure-Web-Service lautet der Standardeingabename `"input1"`. Dieses Feld ist gegenwärtig für {{site.data.keyword.aios_short}} bevollmächtigt und wenn es fehlt, funktioniert {{site.data.keyword.aios_short}} nicht.

  Wenn Ihr Azure-Web-Service nicht den Standardnamen verwendet, ändern Sie den Namen für das Eingabefeld in `"input1"`, dann funktioniert der Code.

- Wenn an Microsoft Azure ML Studio gerichtete Aufrufe zur Auflistung der Machine Learning-Modelle zur Folge haben, dass die Antwort das Zeitlimit überschreitet, wenn zum Beispiel eine große Anzahl von Web-Services vorhanden ist, so müssen Sie einen höheren Wert für das Zeitlimit festlegen. Wenn Sie zum Beispiel die HAProxy-Lastausgleichsfunktion verwenden, ist es möglicherweise erforderlich, dieses Problem durch Absetzen der folgenden Befehle zu umgehen:

   - Melden Sie sich am Knoten für die Lastausgleichsfunktion an und aktualisieren Sie `/etc/haproxy/haproxy.cfg`, um den Zeitlimitwert für den Client und den Server von `1m` auf `5m` hochzusetzen:

       ```bash
       timeout client           5m
       timeout server           5m
      ```

   - Führen Sie `systemctl restart haproxy` aus, um die HAProxy-Lastausgleichsfunktion erneut zu starten.

Wenn Sie eine andere Lastausgleichsfunktion als HAProxy verwenden, müssen Sie die Zeitlimitwerte gegebenenfalls auf ähnliche Weise anpassen.
      {: note}

- Von den beiden Arten von Azure Machine Learning-Web-Services wird von {{site.data.keyword.aios_short}} nur der Typ `Neu` unterstützt. Der Typ `Klassisch` wird nicht unterstützt.

- Im Azure-Web-Service lautet der Standardeingabename `"input1"`. Dieses Feld ist gegenwärtig für {{site.data.keyword.aios_short}} bevollmächtigt und wenn es fehlt, schlägt die Genauigkeitsüberwachung fehl.

   Wenn Ihr Azure-Web-Service nicht den Standardnamen verwendet, ändern Sie den Namen für das Eingabefeld in `"input1"`.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*BlazingText-Algorithmus wird nicht unterstützt*__: Das Format der Eingabenutzdaten für den Amazon SageMaker BlazingText-Algorithmus wird in der aktuellen Version von {{site.data.keyword.aios_short}} nicht unterstützt.

<p>&nbsp;</p>


### Instanz des angepassten Machine Learning-Service
{: #wos-common-issues-custom}

- Beim [Python-Modul](/docs/services/ai-openscale?topic=ai-openscale-as-module) funktioniert derzeit die Erklärbarkeit für die angepasste Serviceinstanz nicht. Das liegt daran, dass die angepasste Serviceinstanz eine numerische Vorhersage in den Antwortdaten erfordert, die nicht im Modulscript enthalten ist.

<p>&nbsp;</p>


- **Code-Snippets ungültig**

    - Die für die Überwachungskonfiguration bereitgestellten Code-Snippets sind ungültig, und zwar sowohl das für cURL als auch das für Python. Die korrekten Code-Snippets sind hier bereitgestellt:

      *Protokollierung von Nutzdaten*

      ```cURL
      # ICP-Zugriffstoken durch Übergeben eines ICP-Benutzernamens als $USERNAME und ICP-Kennwort und eines ICP-Kennworts als $PASSWORD in der nachfolgenden Anforderung generieren

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # Die vorherige CURL-Anforderung gibt unter "accessToken" ein Authentifizierungstoken zurück, das Sie in der folgenden Anforderung zur Nutzdatenprotokollierung als {icp_token} verwenden
      # AUFGABE: Manuelles Definieren und Übergeben von:
      # Anforderung - Eingabe für den Scoring-Endpunkt in von {{site.data.keyword.aios_short}} unterstütztem Format - Beispielfelder und -werte durch die jeweils zutreffenden Werte ersetzen
      # Antwort - Ausgabe des bewerteten Modells in von {{site.data.keyword.aios_short}} unterstütztem Format - Beispielfelder und -werte durch die jeweils zutreffenden Werte ersetzen
      # - $SCORING_ID - ID der Scoring-Transaktion
      # - $SCORING_TIME - Verstrichene Zeit in Millisekunden (ms), die für die Vorhersage (zur Leistungsüberwachung) aufgewendet wurde

      SCORING_PAYLOAD='[{
        "scoring_id": "$SCORING_ID",
        "response_time": "$SCORING_TIME",
        "request": {
          "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K"],
          "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026]]
      },
      "response": {
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "probability", "prediction", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, [0.82, 0.07, 0.0, 0.05, 0.03], 0.0, "drugY"]]
        },
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}",
        "deployment_id": "{{deployment_id}}"
      }]'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/scoring_payloads -d "$SCORING_PAYLOAD" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

      *Protokollierung von Rückmeldedaten*

      ```cURL
      # ICP-Zugriffstoken durch Übergeben eines ICP-Benutzernamens als $USERNAME und ICP-Kennwort und eines ICP-Kennworts als $PASSWORD in der nachfolgenden Anforderung generieren

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # Die vorherige CURL-Anforderung gibt unter "accessToken" ein Authentifizierungstoken zurück, das Sie in der folgenden Anforderung zur Nutzdatenprotokollierung als {icp_token} verwenden
      # AUFGABE: Manuelles Definieren und Übergeben von:
      # Felder - Liste von Feldnamen - Beispielwerte durch die jeweils zutreffenden Werte ersetzen
      # Werte - Datensätze der Rückmeldungsdaten - Beispielwerte durch die jeweils zutreffenden Werte ersetzen
      # - $SCORING_ID - ID der Scoring-Transaktion
      # - $SCORING_TIME - Verstrichene Zeit in Millisekunden (ms), die für die Vorhersage (zur Leistungsüberwachung) aufgewendet wurde

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - Das für den verzerrungsbereinigten Endpunkt bereitgestellte Java-Code-Snippet ist ungültig. Das korrekte Code-Snippet wird hier bereitgestellt:

      *Verzerrungsbereinigter Endpunkt*

      ```java
      /**
      Zur Laufzeit müssen Sie die Platzhalter durch die folgenden Werte ersetzen:

      <HOSTNAME> - Hostname, z. B. aiopenscale.test.cloud.ibm.com
      <PORT> - Server-Port
      <DATA_MART_ID> - DataMart-ID
      <SERVICE_BINDING_ID> - ID der Servicebindung
      <ASSET_ID> - Asset-ID oder Modell-ID
      <DEPLOYMENT_ID> - ID der Bereitstellung
      <TOKEN> - Trägertoken

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      String bearerToken = "Bearer <TOKEN>";
      String URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      String payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


## Bekannte Probleme für {{site.data.keyword.wos4d_notm}}
{: #rn-16April2019ki}

Die folgenden Probleme sind spezifisch für {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>

### Microsoft Azure Machine Learning Service
{: #icp4d-azure-service-status403}

Bei der Ausführung von {{site.data.keyword.wos4d_full}} treten möglicherweise Probleme auf, bei denen {{site.data.keyword.aios_short}} nicht in der Lage ist, mit Azure Machine Learning Service zu kommunizieren, wenn Implementierungs-Scoring-Endpunkte aufzurufen sind. Sicherheitstools, die Ihre Unternehmenssicherheitsrichtlinien umsetzen, z. B. Symantec Blue Coat, können diesen Zugriff verhindern.

Wenn Fehler auftreten, die darauf hinweisen, dass das Scoring für Azure Machine Learning Service nicht erreicht wird, z. B. der HTTP-Statuscode 403, überprüfen Sie Ihre Unternehmenssicherheitsrichtlinien und stellen Sie sicher, dass die Scoring-URL ordnungsgemäß mit den verwendeten Tools erneut kategorisiert wird, soweit erforderlich, damit {{site.data.keyword.aios_short}} ordnungsgemäß auf die Scoring-Endpunkte zugreifen kann.

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services (C&DS)
{: #rn-16April2019ki-icp-spss}

- **Eingeschränkte Unterstützung der Erklärbarkeit**

   - Die Erklärbarkeit wird für binäre Modelle und für solche SPSS-Modelle mit mehreren Klassen unterstützt, die Wahrscheinlichkeiten für alle Klassen zurückgeben. 
   - Die Erklärbarkeit wird nicht für solche SPSS-Modelle mit mehreren Klassen unterstützt, die nur die Wahrscheinlichkeit für die sich durchsetzende Klasse zurückgeben.



<p>&nbsp;</p>




- **IBM SPSS Collaboration and Deployment Services (C&DS) erfordert (nur Binärtyp) die Durchführung einer zusätzlichen Nutzdatenanforderung**

    - Für binäre Abonnements von IBM SPSS Collaboration & Deployment Services müssen Sie eine weitere [(Scoring-)Anforderung zur Nutzdatenprotokollierung](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring) stellen, nachdem Sie die [Überwachungen für eine Bereitstellung vorbereitet](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config) haben oder nachdem alle Überwachungen konfiguriert worden sind. So wird sichergestellt, dass später die [Erklärbarkeit](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov) korrekt ist.

<p>&nbsp;</p>


- Anzahl der korrigierten Datensätze bei **IBM SPSS C&DS (nur Binärtyp) ist möglicherweise falsch**

    - Für binäre Abonnements von IBM SPSS Collaboration & Deployment Services ist die Anzahl für *Korrigierte Datensätze* möglicherweise nicht korrekt, wenn die Anzeige unter Verwendung der Schaltfläche **Transaktionen anzeigen** erfolgt.

<p>&nbsp;</p>

### Metriken
{: #rn-16April2019ki-icp-metrics}

- **{{site.data.keyword.pm_full}}-Leistungsmetriken werden nicht erfasst**

    - In einer Cloud Pak for Data-Umgebung werden keine {{site.data.keyword.pm_full}}-Leistungsmetriken erfasst.

<p>&nbsp;</p>

- **Einschränkungen bei der Unterstützung der Erklärbarkeit**

    - Schließen Sie beim Erstellen Ihrer Modelle nicht die Zielspalte (Kennzeichnung) aus der Eingabeanforderung ins Scoring ein. Wenn für das Modell die Einbindung der Zielspalte in die Eingabeanforderung erforderlich ist, funktionieren Verzerrungsprüfung, Verzerrungsbereinigung und Erklärbarkeit nicht.


<p>&nbsp;</p>


### Python-Funktionen
{: #rn-16April2019ki-icp-python}

- **Python-Funktionen nicht unterstützt**

    - Verzerrungsprüfung, Verzerrungsbereinigung und Erklärbarkeit werden in den aktuellen Releases nicht als Python-Funktionen unterstützt.

<p>&nbsp;</p>


### Installation und Konfiguration
{: #rn-16April2019ki-icp-install}


- **Deinstallationsscript löscht Kafka-Abschnitte nicht**

    - Bei der Ausführung des Deinstallationsscripts werden die {{site.data.keyword.aios_short}} Kafka-Topics, die bei der Installation in EventStream erstellt wurden, nicht entfernt.

<p>&nbsp;</p>

### Datenbanken
{: #rn-16April2019ki-icp-dbs}

- **Begrenzt Zeilenlänge bei Verwendung von Db2 Warehouse**

    - Für Db2 Warehouse gilt eine Zeilenbegrenzung von 1 MB. Wenn mehrere (d. h. mehr als 30) Textspalten (mit 32000 Byte pro VARCHAR) vorhanden sind, wird dieser Grenzwert überschritten. Diese Einschränkung macht sich bei Verwendung von Amazon SageMaker am stärksten bemerkbar, denn im nativen SageMaker-Format liegen alle Spalten in Zeichenfolgeformat vor.

       Da {{site.data.keyword.aios_short}} den Standardtabellenbereich zum Erstellen von Datenbankobjekten verwendet, hängen die tatsächlichen Grenzwerte von der Konfiguration Ihrer Datenbank ab. Zusätzliche Informationen zu dieser Einschränkungen enthält die [Dokumentation zu Db2 im IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html).





## Browserunterstützung
{: #abt-browser}

Für die Tools des {{site.data.keyword.aios_short}}-Service ist dieselbe Browsersoftware erforderlich wie für {{site.data.keyword.cloud_notm}}. Genaueres hierzu enthält der Abschnitt {{site.data.keyword.cloud_notm}} [Voraussetzungen](/docs/overview?topic=overview-prereqs-platform#browsers).

<p>&nbsp;</p>


## Python-Client
{: #abt-python}

Der [Python-Client für {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} ist eine Python-Bibliothek, die es Ihnen ermöglicht, direkt mit dem {{site.data.keyword.aios_short}}-Service zu arbeiten. Sie können den Python-Client anstelle der {{site.data.keyword.aios_short}}-Clientbenutzerschnittstelle verwenden, um die Datamart-Datenbank direkt zu konfigurieren, die Maschine Learning-Engine zu binden sowie Bereitstellungen auszuwählen und zu überwachen. Beispiele, in denen der Python-Client auf diese Weise verwendet wird, enthalten die [{{site.data.keyword.aios_short}}-Beispielnotebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>
## Weitere Schritte
{: #abt-next}

- Machen Sie Ihre [ersten Schritte](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started) mit dem Service.
- [](https://test.cloud.ibm.com/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- Sichten Sie das [Referenzmaterial für die API](https://{DomainName}/apidocs/ai-openscale){: external}.

Haben Sie immer noch offene Fragen? 

- [Neuerungen in {{site.data.keyword.wos4dfull}}](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [IBM kontaktieren](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
