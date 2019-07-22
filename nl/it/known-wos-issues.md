---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Problemi noti e limitazioni per {{site.data.keyword.aios_short}}
{: #rn-12ki}

Il seguente elenco contiene i problemi e le limitazioni noti per {{site.data.keyword.aios_full}}.
{: shortdesc}

<p>&nbsp;</p>

## Limitazioni
{: #wos-limitations}

- {{site.data.keyword.aios_short}} supporta più motori di machine learning, a condizione di configurare gli ulteriori motori tramite l'SDK Python.

- La release corrente supporta solo un database, un'istanza di {{site.data.keyword.pm_full}} e un'istanza di {{site.data.keyword.aios_short}}

- Il database e l'istanza {{site.data.keyword.pm_full}} devono essere distribuiti nello stesso account {{site.data.keyword.cloud_notm}}.

- Il piano Lite (gratuito) ha i seguenti limiti mensili:

    - Due modelli distribuiti monitorati
    - 20 transazioni spiegate
    - 50.000 record di payload (cumulativi)
    - 50.000 record di feedback (cumulativi)

- {{site.data.keyword.aios_short}} utilizza un database PostgreSQL o Db2 per memorizzare i dati relativi al modello (dati di feedback, payload di calcolo del punteggio) e le metriche calcolate. I piani DB2 Lite non sono attualmente supportati.

- Esiste un limite di licenza di 20 modelli distribuiti per istanza di {{site.data.keyword.aios_short}}.

- Per {{site.data.keyword.pm_full}}, l'input di calcolo del punteggio per i modelli di classificazione dell'immagine inviati per la registrazione del payload non può superare 1 MB. Per evitare problemi di timeout, le immagini non devono superare 125 x 125 pixel e devono essere inviate in sequenza in modo che la spiegazione per la seconda immagine sia richiesta quando la prima è completata.

- Il database gratuito del piano Lite non è conforme al GDPR. Se il modello elabora PII (personally identifiable information - informazioni per l'identificazione personale), sarà necessario acquistare un nuovo database oppure utilizzare un database esistente, che sia conforme alle normative del GDPR. 

- L'esplicabilità per i modelli di testo non strutturati non è supportata per linguaggi di script continui, come il giapponese, il cinese e il coreano, che non usano spazi o caratteri di punteggiatura per separare le parole.



<p>&nbsp;</p>

## Problemi comuni
{: #wos-common-issues}

Le seguenti problematiche sono comuni sia a {{site.data.keyword.aios_full}} su {{site.data.keyword.Bluemix}} che a {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>

### Formati payload
{: #wos-common-issues-payloadformat}

Per una corretta elaborazione dell'analytics del payload, {{site.data.keyword.aios_short}} non supporta i nomi di colonna con virgolette (") nel payload. Ciò influisce sui dati di feedback e payload di calcolo del punteggio nei formati CSV e JSON.

<p>&nbsp;</p>



### Microsoft Azure ML Studio
{: #wos-common-issues-msazure}

- Dei due tipi di servizi Web di Azure Machine Learning, solo il tipo `Nuovo` è supportato da {{site.data.keyword.aios_short}}. Il tipo `Classico` non è supportato.

- __*Deve essere utilizzato il nome di input predefinito*__: nel servizio Web Azure, il nome di input predefinito è `"input1"`. Attualmente questo campo è obbligatorio per {{site.data.keyword.aios_short}} e, se manca, {{site.data.keyword.aios_short}} non funzionerà.

  Se il servizio Web Azure non utilizza il nome predefinito, modificare il nome del campo di immissione in `"input1"`, così il codice funzionerà.

- Se le chiamate a Microsoft Azure ML Studio per elencare i modelli di machine learning provocano il timeout della risposta, ad esempio quando si hanno molti servizi web, è necessario aumentare i valori di timeout. Ad esempio, se si sta utilizzando il programma di bilanciamento del carico HAProxy, potrebbe essere necessario risolvere questo problema tramite i seguenti comandi:

   - L'accesso al nodo del programma di bilanciamento del carico e l'aggiornamento di `/etc/haproxy/haproxy.cfg` in modo da impostare il timeout del server e del client da `1m` a `5m`:

       ```bash
       timeout client           5m
          timeout server           5m
      ```

   - Eseguendo `systemctl restart haproxy` per riavviare il programma di bilanciamento del carico HAProxy.

Se si utilizza un programma di bilanciamento del carico diverso, non HAProxy, potrebbe essere necessario regolare i valori di timeout in modo simile.
      {: note}

- Dei due tipi di servizi Web di Azure Machine Learning, solo il tipo `Nuovo` è supportato da {{site.data.keyword.aios_short}}. Il tipo `Classico` non è supportato.

- Nel servizio Web Azure, il nome di input predefinito è `"input1"`. Attualmente questo campo è obbligatorio per {{site.data.keyword.aios_short}} e, se manca, il monitoraggio dell'accuratezza non riesce.

   Se il servizio Web Azure non utilizza il nome predefinito, modificare il nome del campo di immissione in `"input1"`.

<p>&nbsp;</p>


### Amazon SageMaker
{: #wos-common-issues-aws}

- __*L'algoritmo BlazingText non è supportato*__: il formato di payload di input dell'algoritmo Amazon SageMaker BlazingText non è supportato nella release corrente di {{site.data.keyword.aios_short}}.

<p>&nbsp;</p>


### Istanza del servizio di machine learning personalizzato
{: #wos-common-issues-custom}

- Il [modulo Python](/docs/services/ai-openscale?topic=ai-openscale-as-module) attualmente non dispone di una Esplicabilità funzionante per l'istanza del servizio personalizzata. Questo perché l'istanza del servizio personalizzata richiede una previsione numerica nei dati di risposta, che non è inclusa con lo script del modulo.

<p>&nbsp;</p>


- **Frammenti di codice non validi**

    - Sia i frammenti di codice cURL che Python forniti per la configurazione del monitor non sono validi. I frammenti di codice corretti sono forniti qui:

      *Registrazione payload*

      ```cURL
      # Generare un token di accesso ICP inoltrando un nome utente ICP come $USERNAME e la password ICP come $PASSWORD nella seguente richiesta

      curl -k -X GET \
      -user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # la precedente richiesta CURL restituirà un token auth in "accessToken", che dovrà essere utilizzato come {icp_token} nella seguente richiesta di registrazione payload
      # TODO: definire manualmente e inoltrare:
      # request - input all'endpoint di calcolo del punteggio in formato supportato da {{site.data.keyword.aios_short}} - sostituire campi e valori di esempio con quelli appropriati
      # response - output dal modello calcolato in formato supportato da {{site.data.keyword.aios_short}} - sostituire campi e valori di esempio con quelli appropriati
      # - $SCORING_ID - ID della transazione di calcolo del punteggio
      # - $SCORING_TIME - Tempo (ms) impiegato per effettuare la previsione (per il monitoraggio delle prestazioni)

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

      *Registrazione feedback*

      ```cURL
      # Generare un token di accesso ICP inoltrando un nome utente ICP come $USERNAME e la password ICP come $PASSWORD nella seguente richiesta

      curl -k -X GET \
      --user "$USERNAME:$PASSWORD" \
      "https://{{icp_hostname}:{{icp_port}}/v1/preauth/validateAuth"

      # la precedente richiesta CURL restituirà un token auth nella chiave "accessToken", che dovrà essere utilizzato come {icp_token} nella seguente richiesta di registrazione payload
      # TODO: definire manualmente e inoltrare:
      # fields - elencare i nomi campo - sostituire i valori di esempio con quelli appropriati
      # values - record dei dati di feedback - sostituire i valori di esempio con quelli appropriati
      # - $SCORING_ID - ID della transazione di calcolo del punteggio
      # - $SCORING_TIME - Tempo (ms) impiegato per effettuare la previsione (per il monitoraggio delle prestazioni)

      FEEDBACK_DATA='{
        "fields": ["AGE", "SEX", "BP", "CHOLESTEROL", "NA", "K", "DRUG"],
        "values": [[28, "F", "LOW", "HIGH", 0.61, 0.026, "drugB"]],
        "binding_id": "{{binding_id}}",
        "subscription_id": "{{subscription_id}}"
      }'

      curl -k -X POST https://{{icp_hostname}:{{icp_port}}/v1/data_marts/{{data_mart_id}}/feedback_payloads -d "$FEEDBACK_DATA" \
      --header 'Content-Type: application/json' --header 'Accept: application/json' --header "Authorization: Bearer $ICP_TOKEN"
      ```

    - Il frammento di codice Java fornito per l'endpoint di annullamento della distorsione non è valido. Il frammento di codice corretto è fornito qui:

      *Endpoint di annullamento distorsione*

      ```java
      /**
      Al runtime occorre sostituire i valori per:

      <HOSTNAME> - Nome host, ad es.: aiopenscale.test.cloud.ibm.com
      <PORT> - porta server
      <DATA_MART_ID> - ID DataMart
      <SERVICE_BINDING_ID> - ID bind servizio
      <ASSET_ID> - ID asset o modello
      <DEPLOYMENT_ID> - ID distribuzione
      <TOKEN> - token bearer

      */
      import org.apache.http.HttpVersion;
      import org.apache.http.client.fluent.Request;
      import org.apache.http.entity.ContentType;

      Stringa bearerToken = "Bearer <TOKEN>";
      Stringa URL = "https://<HOSTNAME>:<PORT>/v1/data_marts/<DATA_MART_ID>/service_bindings/<SERVICE_BINDING_ID>/subscriptions/<ASSET_ID>/deployments/<DEPLOYMENT_ID>/online";

      Stringa payload = "{ \"fields\": [ \"field1\", \"field2\", \"field3\" ], \"values\": [ [ \"field1Value1\", \"field2Value1\", \"field3Value1\" ], [ \"field1Value2\", \"field2Value2\", \"field3Value2\" ]] }";

      byte[] res = Request.Post(URL).addHeader("Authorization", bearerToken).useExpectContinue().version(HttpVersion.HTTP_1_1)
                .bodyString(payload, ContentType.APPLICATION_JSON).execute().returnContent().asBytes();
      ```

<p>&nbsp;</p>


## Problemi noti per {{site.data.keyword.wos4d_notm}}
{: #rn-16April2019ki}

Le seguenti problematiche sono specifiche per {{site.data.keyword.wos4d_full}}.

<p>&nbsp;</p>


### IBM SPSS Collaboration and Deployment Services (C&DS)
{: #rn-16April2019ki-icp-spss}

- **Limitazioni del supporto dell'esplicabilità**

   - L'esplicabilità è supportata per i modelli binari e per i modelli SPSS multiclasse che restituono le probabilità per tutte le classi. 
   - L'esplicabilità non è supportata per i modelli SPSS multiclasse che restituono solo la probabilità della classe vincente.


<p>&nbsp;</p>


- **L'ID di distribuzione non può contenere il carattere di sottolineatura (_) in IBM SPSS Collaboration and Deployment Services (C&DS)**

    - Rimuovere il carattere di sottolineatura (_) dall'`id_distribuzione` per una sottoscrizione.

<p>&nbsp;</p>




- **IBM SPSS Collaboration and Deployment Services (C&DS) (solo tipo binario) richiede che venga effettuata una richiesta di payload aggiuntivo**

    - Per le sottoscrizioni binarie di IBM SPSS Collaboration & Deployment Services, è necessario effettuare un'altra [richiesta di registrazione del payload (calcolo del punteggio)](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-cdb-connect#cdb-scoring) dopo la  [preparazione dei monitor per la distribuzione](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-mo-config#mo-config) o dopo la configurazione di tutti i monitor. Ciò garantisce che la [esplicabilità](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-ie-ov#ie-ov) sia accurata.

<p>&nbsp;</p>


- Il conteggio dei record corretti di **IBM SPSS C&DS (solo tipo binario) potrebbe essere sbagliato. **

    - Per le sottoscrizioni binarie di IBM SPSS Collaboration & Deployment Services, il conteggio *Record corretti* potrebbe non essere accurato quando visualizzato utilizzando il pulsante **Visualizza transazioni**.

<p>&nbsp;</p>

### Metriche
{: #rn-16April2019ki-icp-metrics}

- **Metriche delle prestazioni {{site.data.keyword.pm_full}} non raccolte**

    - In un ambiente Cloud Pak for Data, le metriche delle prestazioni da {{site.data.keyword.pm_full}} non vengono raccolte.

<p>&nbsp;</p>

- **Limitazioni del supporto dell'esplicabilità**

    - Quando si creano i modelli, non viene inclusa la colonna di destinazione (etichetta) dalla richiesta di input per il calcolo del punteggio. Se il modello richiede che la colonna di destinazione venga inclusa nella richiesta di input, il controllo della distorsione, l'annullamento della distorsione e l'esplicabilità non funzioneranno.


<p>&nbsp;</p>


### Funzioni Python
{: #rn-16April2019ki-icp-python}

- **Funzioni Python non supportate**

    - Il controllo della distorsione, l'annullamento della distorsione e l'esplicabilità non sono supportati per le funzioni Python, nella release corrente.

<p>&nbsp;</p>


### Installazione e configurazione
{: #rn-16April2019ki-icp-install}


- **Lo script di disinstallazione non elimina gli argomenti Kafka**

    - L'esecuzione dello script di disinstallazione non rimuove gli argomenti {{site.data.keyword.aios_short}} Kafka che sono stati creati in EventStream durante l'installazione.

<p>&nbsp;</p>

### Database
{: #rn-16April2019ki-icp-dbs}

- **Limitazione dimensione riga utilizzando Db2 Warehouse**

    - C'è un limite di dimensione riga di 1 MB per Db2 Warehouse. Quando sono presenti più colonne di testo (più di 30) (32000 byte per ogni VARCHAR), il limite viene superato. Questa limitazione è più evidente quando si utilizza Amazon SageMaker, poiché il formato nativo SageMaker ha tutte le colonne in formato stringa.

       Poiché {{site.data.keyword.aios_short}} utilizza il tablespace predefinito per la creazione degli oggetti database, i limiti effettivi dipendono dalla configurazione del database. Ulteriori informazioni su questa limitazione sono disponibili nella [documentazione di Db2 nell'IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/SSEPGG_11.1.0/com.ibm.db2.luw.sql.ref.doc/doc/r0001029.html).





## Supporto dei browser
{: #abt-browser}

Gli strumenti del servizio {{site.data.keyword.aios_short}} richiedono lo stesso livello di software browser richiesto da {{site.data.keyword.cloud_notm}}. Per i dettagli, consultare l'argomento Prerequisiti {{site.data.keyword.cloud_notm}} [](/docs/overview?topic=overview-prereqs-platform#browsers).

<p>&nbsp;</p>


## Client Python
{: #abt-python}

Il [client {{site.data.keyword.aios_short}} Python](http://ai-openscale-python-client.mybluemix.net/){: external} è una libreria Python che consente di lavorare direttamente con il servizio {{site.data.keyword.aios_short}}. È possibile utilizzare il client Python, invece della IU del client  {{site.data.keyword.aios_short}}, per configurare direttamente il database datamart, collegare il motore di machine learning e selezionare e monitorare le distribuzioni. Per esempi di utilizzo del client Python a questo scopo, consultare i [notebook di esempio {{site.data.keyword.aios_short}}](https://github.com/pmservice/ai-openscale-tutorials/tree/master/notebooks).

<p>&nbsp;</p>
## Passi successivi
{: #abt-next}

- [Introduzione](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-gs-get-started) al servizio.
- Visualizzare il [materiale Riferimento API](https://{DomainName}/apidocs/ai-openscale){: external}.

Altre domande? 

- [Novità](/docs/services/ai-openscale-icp?topic=ai-openscale-icp-rn-relnotes)
- [Contatta IBM](https://www.ibm.com/account/reg/us-en/signup?formid=MAIL-watson){: external}.