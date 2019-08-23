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

# Bekannte Probleme und Einschränkungen bei {{site.data.keyword.aios_short}} für {{site.data.keyword.cloud_notm}}
{: #rn-12ki}

In der folgenden Liste sind die für {{site.data.keyword.aios_full}} für {{site.data.keyword.Bluemix}} und {{site.data.keyword.wos4d_full}} sowie die für {{site.data.keyword.aios_full}} für {{site.data.keyword.Bluemix}} spezifischen bekannten Probleme und Einschränkungen aufgeführt.
{: shortdesc}

<p>&nbsp;</p>

## Gängige Probleme
{: #wos-common-issues}

Die folgenden Einschränkungen und bekannten Probleme gelten sowohl für {{site.data.keyword.aios_full}} unter {{site.data.keyword.Bluemix}} als auch für {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>


### Allgemeine Einschränkungen
{: #wos-limitations}

- Für {{site.data.keyword.pm_full}} darf die Scoring-Eingabe für Imageklassifizierungsmodelle, die zur Nutzdatenprotokollierung gesendet werden, ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling serviceMB nicht überschreiten. Um Probleme aufgrund von Zeitlimitüberschreitungen zu vermeiden, dürfen Images nicht mehr als 125 x 125 Pixel aufweisen und sie müssen nacheinander gesendet werden, damit die Erklärung für das zweite Image angefordert wird, nachdem die erste abgeschlossen ist.


- Die Erklärbarkeit wird bei Modellen mit unstrukturiertem Text nicht für fortlaufende Scriptsprachen wie Japanisch, Chinesisch und Koreanisch, bei denen keine Leerzeichen oder Punktuationszeichen zum Trennen von Wörtern verwendet werden, unterstützt.



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

Bei der Verarbeitung der Nutzdatenanalyse werden von {{site.data.keyword.aios_short}} keine Spaltennamen mit Anführungszeichen (") in den Nutzdaten unterstützt. Dies betrifft sowohl Scoring-Nutzdaten als auch Rückmeldedaten im CSV- und im JSON-Format.

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


### Browserunterstützung
{: #abt-browser}

Für die Tools des {{site.data.keyword.aios_short}}-Service ist dieselbe Browsersoftware erforderlich wie für {{site.data.keyword.cloud_notm}}. Genaueres hierzu enthält der Abschnitt {{site.data.keyword.cloud_notm}} [Voraussetzungen](/docs/overview?topic=overview-prereqs-platform#browsers).

<p>&nbsp;</p>


### Python-Client
{: #abt-python}

Der [Python-Client für {{site.data.keyword.aios_short}}](http://ai-openscale-python-client.mybluemix.net/){: external} ist eine Python-Bibliothek, die es Ihnen ermöglicht, direkt mit dem {{site.data.keyword.aios_short}}-Service zu arbeiten. Sie können den Python-Client anstelle der {{site.data.keyword.aios_short}}-Clientbenutzerschnittstelle verwenden, um die Datamart-Datenbank direkt zu konfigurieren, die Maschine Learning-Engine zu binden sowie Bereitstellungen auszuwählen und zu überwachen. Beispiele, in denen der Python-Client auf diese Weise verwendet wird, enthalten die [{{site.data.keyword.aios_short}}-Beispielnotebooks](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).


## Für {{site.data.keyword.aios_short}} spezifische Probleme
{: #cloud-issues}

Die folgende Einschränkung und die folgenden Probleme gelten für {{site.data.keyword.aios_short}} für {{site.data.keyword.Bluemix}}.

<p>&nbsp;</p>

### Einschränkungen
{: #cloud-limitations}

- Das aktuelle Release unterstützt nur eine Datenbank, eine {{site.data.keyword.pm_full}}-Instanz und eine Instanz von {{site.data.keyword.aios_short}}. 

- Die Datenbank und die {{site.data.keyword.pm_full}}-Instanz müssen in demselben {{site.data.keyword.cloud_notm}}-Konto bereitgestellt werden.

- {{site.data.keyword.aios_short}} verwendet eine PostgreSQL- oder Db2-Datenbank zum Speichern modellbezogener Daten (Rückmeldedaten, Scoring-Nutzdaten) und berechneter Metriken. Lite-Pläne mit Db2 werden gegenwärtig nicht unterstützt.

- Die Datenbank für den kostenlosen Lite-Plan ist nicht DSGVO-konform. Wenn in Ihrem Modell personenbezogene Daten verarbeitet werden, dann müssen Sie eine neue Datenbank kaufen oder eine bereits vorhandene Datenbank verwenden, die DSGVO-konform ist.



<p>&nbsp;</p>
## Weitere Schritte
{: #abt-next}

- [Einführung](/docs/services/ai-openscale?topic=ai-openscale-gettingstarted)
- Sichten Sie das [Referenzmaterial für die API](https://{DomainName}/apidocs/ai-openscale){: external}.
- [Neuerungen in {{site.data.keyword.aios_short}}](/docs/services/ai-openscale?topic=ai-openscale-rn-relnotes)
- [IBM kontaktieren](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.
