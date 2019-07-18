---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# Specifica di un'istanza del servizio ML personalizzata
{: #co-connect}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza del servizio. L'istanza del servizio è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

## Connessione dell'istanza del servizio personalizzata
{: #co-config}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza del servizio. È possibile collegare un servizio personalizzato

1. Dalla scheda **Configura**, fare clic su **Provider di machine learning**.

   ![viene visualizzato il pannello per la selezione del provider del servizio di machine learning con i riquadri per i motori di machine learning supportati](images/wos-machine-learning-providers-selection.png)

2. Selezionare il riquadro **Ambiente personalizzato**.

   ![Selezionare personalizzato](images/ml-custom-provider.png)

3. Immettere un nome e una descrizione per il provider di machine learning personalizzato e fare clic su **Avanti**. 

4. Scegliere se connettersi alle distribuzioni [richiedendo un elenco](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-request-list) o [immettendo singoli endpoint di calcolo del punteggio](/docs/services/ai-openscale?topic=ai-openscale-co-connect#co-config-scoring-endpoints).

   ![Selezionare personalizzato](images/ml-custom-connect-deployments.png)
    
5. Fare clic su **Avanti**.

### Richiesta dell'elenco di distribuzioni
{: #co-config-request-list}

1. Se si seleziona il riquadro **Richiedi l'elenco di distribuzioni**, immettere le credenziali e l'endpoint API, quindi fare clic su **Salva**.

   ![Immettere le credenziali del servizio](images/connect-custom-cred.png)

2. Dopo aver salvato l'impostazione del machine learning, tornare al **Dashboard**, fare clic sulla scheda **Insight**, quindi fare clic sul pulsante **Aggiungi distribuzioni**.

3. Selezionare una distribuzione dall'elenco e fare clic su **Configura**.

Ora si è pronti a configurare i monitor.

### Fornitura di singoli endpoint di calcolo del punteggio
{: #co-config-scoring-endpoints}

1. Se si seleziona il riquadro **Immetti gli endpoint del punteggio individuali**, immettere le credenziali per l'endpoint API, quindi fare clic su **Salva**.

2. Dopo aver salvato l'impostazione del machine learning, tornare al **Dashboard**, fare clic sulla scheda **Insight**, quindi fare clic sul pulsante **Aggiungi distribuzioni**.

3. Fare clic sul pulsante **Aggiungi endpoint**. 

4. Dal menu a discesa, selezionare l'ambiente personalizzato, immettere il nome della distribuzione e l'endpoint API, quindi fare clic su **Salva**.

Ora si è pronti a configurare i monitor.

### Funzionamento
{: #co-works}

La seguente immagine mostra il supporto dell'ambiente personalizzato:

![Funzionamento della personalizzazione](images/custom-how-works.png)

È anche possibile fare riferimento ai seguenti link:

[API di registrazione payload {{site.data.keyword.aios_short}}](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: external}

[Custom deployment API](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: external}

[Python client binding SDK](http://ai-openscale-python-client.mybluemix.net/#bindings){: external}

[Utilizzo del motore di machine learning personalizzato](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: external}

[Python SDK for IBM Watson OpenScale](https://pypi.org/project/ibm-ai-openscale/){: external}

- **Criteri di input perché il modello supporti i monitor**

  Il modello deve assumere come input un vettore di funzione, che è essenzialmente una raccolta di campi indicati e i loro valori (i campi monitorati per la distorsione devono essere tra questi):

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position"
    ],
    "values": [
        [
            "john",
            33,
            "engineer"
        ],
        [
            "mike",
            23,
            "student"
        ]
    ]
  }
  ```

  In questo esempio, `“age”` potrebbe essere un campo che qualcuno sta valutando per la correttezza.

  Se l'input è un tensore o una matrice, trasformati dallo spazio della funzione di input (come spesso accade nel deep learning da testo o immagini), il modello non può essere gestito dalla piattaforma {{site.data.keyword.aios_short}} nella release corrente. Per estensione, i modelli di deep learning con input di testo o immagine non possono essere gestiti per la rilevazione e la mitigazione della distorsione.

  Inoltre, i dati di training devono essere caricati per supportare l'esplicabilità.

  Per l'esplicabilità sul testo, una delle funzioni deve essere il testo completo. L'esplicabilità sulle immagini per un modello personalizzato non è supportata nella release corrente.
  {: note}

- **Criteri di output perché il modello supporti i monitor**

  Il modello dovrebbe emettere il vettore della funzione di input insieme alle probabilità previsionali di varie classi in quel modello.

  ```bash
  {
    "fields": [
        "name",
        "age",
        "position",
        "prediction",
        "probability"
    ],
    "labels": [
        "personal",
        "camping"
    ],
    "values": [
        [
            "john",
            33,
            "engineer",
            "personal",
            [
                0.6744664422398081,
                0.3255335577601919
            ]
        ],
        [
            "mike",
            23,
            "student"
            "camping",
            [
                0.2794765664946941,
                0.7205234335053059
            ]
        ]
    ]
  }
  ```

  In questo esempio, `"personal”` e `“camping”` sono le possibili classi e i punteggi in ogni output di calcolo del punteggio sono assegnati a entrambe le classi. Se mancano le probabilità previsionali, il rilevamento della distorsione funzionerà, ma non funzionerà l'annullamento automatico della distorsione.

  L'output del calcolo del punteggio sopra riportato deve essere accessibile da un endpoint di calcolo del punteggio attivo che {{site.data.keyword.aios_short}} può richiamare su REST. Per AzureML, SageMaker e {{site.data.keyword.pm_full}}, {{site.data.keyword.aios_short}} connette direttamente agli endpoint di calcolo del punteggio nativi, pertanto non occorre implementare la specifica di punteggio.

### Passi successivi
{: #co-next}

{{site.data.keyword.aios_short}} ora è pronto per poter [configurare i monitor](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
