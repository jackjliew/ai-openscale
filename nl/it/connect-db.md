---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-09"

keywords: databases, connections, scoring, requests

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

# Specifica di un database
{: #connect-db}

Specificare un database per l'utilizzo da parte dell'istanza {{site.data.keyword.aios_short}}.
{: shortdesc}

## Connessione al database
{: #cdb-connect}

{{site.data.keyword.aios_short}} utilizza un database per memorizzare il payload, il feedback e i dati di misurazione. Oltre a selezionare un database, è possibile selezionare anche uno schema per il database - uno schema è una determinata raccolta di tabelle nel database.

1.  Scegliere un database. Esistono due opzioni: il database del piano Lite gratuito o un database esistente o nuovo.

    ![Selezionare il database](images/gs-config-database.png)

    Se si dispone di un account {{site.data.keyword.cloud_notm}} a pagamento, è possibile fornire un servizio `Databases for PostgreSQL` o `Db2 Warehouse` per sfruttare tutti i vantaggi dell'integrazione con Watson Studio e i servizi di continuous learning. Se si sceglie di non fornire un servizio a pagamento, è possibile utilizzare lo storage interno PostgreSQL gratuito con {{site.data.keyword.aios_short}}, ma non sarà possibile configurare il continuous learning per il modello. {: note}

### Database del piano Lite gratuito
{: #cdb-lite}

**NOTA**: il database gratuito del piano Lite ha alcune limitazioni importanti:

- Il database gratuito del piano Lite è ospitato e non è accessibile direttamente.
- {{site.data.keyword.aios_full}} avrà accesso completo al database e quindi avrà accesso completo ai dati.
- Il database gratuito del piano Lite non è conforme con il GDPR. Se il proprio modello elabora informazioni personali identificabili (o PII-personally-identifiable information), non è possibile utilizzare il database gratuito del piano Lite. È necessario acquistare un nuovo database, o utilizzare un database esistente che sia conforme alle regole del GDPR. Consultare [Sicurezza delle informazioni](/docs/services/ai-openscale?topic=ai-openscale-is-ov) per acquisire ulteriori informazioni.

Per procedere con l'utilizzo del database gratuito del piano Lite, selezionare semplicemente quella opzione, quindi rivedere i dati di riepilogo e fare clic su **Salva**.

  ![Selezionare il database](images/gs-config-database2.png)

### Database esistente o nuovo
{: #cdb-exn}

1.  Se è stata selezionata l'opzione "Utilizza il database esistente o acquistane uno nuovo", {{site.data.keyword.aios_short}} controlla l'account {{site.data.keyword.Bluemix_notm}} per individuare eventuali database esistenti.

1.  Selezionare il proprio tipo di database esistente (Compose per Postgres, Database per Postgres o Db2), quindi un database dal menu a discesa **Database** e quindi uno **Schema**:

    {{site.data.keyword.aios_short}} utilizza un database PostgreSQL o Db2 per memorizzare l'output della distribuzione dei modelli e i dati del nuovo training. I piani DB2 Lite non sono attualmente supportati. {: note}

    ![Selezionare il database](images/gs-config-database3.png)

1.  È anche possibile fare clic su **Seleziona un percorso differente** per specificare una ubicazione database al di fuori del proprio account {{site.data.keyword.Bluemix_notm}}.

    {{site.data.keyword.aios_short}} utilizza un database PostgreSQL o Db2 per memorizzare l'output della distribuzione dei modelli e i dati del nuovo training. I piani DB2 Lite non sono attualmente supportati. {: note}

    - Selezionare il **Tipo di database** (`Compose per PostgreSQL`, `Database per PostgreSQL` o `Db2`), quindi fornire le informazioni di connessione:

        - Per un database `Compose per PostgreSQL`, indicare le seguenti informazioni:

            - Nome host o indirizzo IP
            - Porta
            - Database (nome)
            - Nome utente
            - Password

            ![Specificare l'ubicazione db Compose per Postgres](images/db-config-cpostgres.png)

        - Per un database `Database per PostgreSQL`, indicare le seguenti informazioni:

            - Nome host o indirizzo IP
            - Porta SSL
            - Certificato con codifica Base-64
            - Database (nome)
            - Nome utente
            - Password

            ![Specificare l'ubicazione db Database per Postgres](images/db-config-dpostgres.png)

        - Per un database `Db2`, indicare le seguenti informazioni:

            - Nome host o indirizzo IP
            - Porta SSL
            - Database (nome)
            - Nome utente
            - Password

            ![Specificare l'ubicazione Db2 ](images/db-config-db2.png)

    - Una volta che si è connessi correttamente, è possibile selezionare uno schema.

      Il nome schema deve essere fornito esplicitamente se si fornisce un'istanza Db2 con accesso limitato, cosa che non consente che il nome schema sia generato automaticamente. Questo si applica al piano Entry Db2 Warehouse.       {: important}

      ![Selezionare lo schema](images/gs-config-database5.png)

1.  Fare clic su **Avanti** per esaminare i dati di riepilogo, quindi fare clic su **Salva**.

## Invio di una richiesta di calcolo del punteggio
{: #cdb-score}

Per configurare i monitor, {{site.data.keyword.aios_short}} richiede l'invio di una richiesta di calcolo del punteggio, per poter iniziare a registrare i dati che verranno monitorati. 

Il punteggio dei modelli distribuiti in Watson Machine Learning viene automaticamente calcolato da {{site.data.keyword.aios_short}}. Se si dispone solo di modelli distribuiti in Watson Machine Learning, non verrà visualizzata questa schermata.
{: note:}

Selezionare una distribuzione, in questo caso "Frode Detector", quindi utilizzare i frammenti di codice `cURL` o `Python` forniti per registrare i dati di richiesta e risposta di distribuzione del modello. Per maggiori dettagli, consultare [Registrazione payload per istanze di servizio non Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect). 

I campi e i valori nei frammenti di codice devono essere sostituiti con i propri valori reali, in quanto quelli forniti sono solo esempi.
{: important}

![Selezionare il database](images/config-send-scoring.png)

Una volta eseguita la registrazione del payload, verrà visualizzato un segno di spunta nella colonna "Pronto a monitorare" per la distribuzione selezionata. Fare clic su **Configura monitor** per continuare.

## Passi successivi
{: #cdb-next}

{{site.data.keyword.aios_short}} ora è pronto per poter [configurare i monitor per le distribuzioni](/docs/services/ai-openscale?topic=ai-openscale-mo-config).