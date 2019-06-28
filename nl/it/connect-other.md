---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning, services, ml, custom 

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

# Specifica di un'istanza del servizio ML personalizzata
{: #co-connect}

Il primo passo nello strumento {{site.data.keyword.aios_short}} è quello di specificare un'istanza del servizio. L'istanza del servizio è il luogo dove si memorizzano i modelli AI e le distribuzioni.
{: shortdesc}

## Connessione dell'istanza del servizio personalizzata
{: #co-config}

{{site.data.keyword.aios_short}} si collega ai modelli e alle distribuzioni AI in un'istanza del servizio.

1.  Dalla home page dello strumento {{site.data.keyword.aios_short}}, fare clic su **Inizia**.

    ![Home page](images/gs-config-start.png)

2.  Selezionare il riquadro **Personalizzato** e fare clic su **Avanti**.

    ![Selezionare personalizzato](images/connect-custom.png)

3.  Connettersi alle distribuzioni selezionando una delle opzioni:

    ![Selezionare personalizzato](images/connect-custom-deploy.png)

4.  Se è stato selezionato il riquadro "Immetti gli endpoint del punteggio individuali", immettere le credenziali:

    ![Immettere le credenziali del servizio](images/connect-custom-cred.png)

5.  Fare clic su **Avanti**.

    - Se è stato selezionato il riquadro "Immetti gli endpoint del punteggio individuali", è necessario fornire un nome di distribuzione e un endpoint:

      ![Immettere le credenziali del servizio](images/connect-custom-endpoint.png)

      Fare clic su **Avanti**.

    - Se è stato selezionato il riquadro "Richiedi un elenco di distribuzioni", è necessario fornire un nome host o un indirizzo IP e il numero porta:

      ![Immettere le credenziali del servizio](images/connect-custom-apiendpoint.png)

      Fare clic su **Avanti**.

      Quindi selezionare dall'elenco di distribuzioni:

      ![Immettere le credenziali del servizio](images/connect-custom-apiendpoint2.png)

6.  Esaminare le distribuzioni selezionate.

    ![Immettere le credenziali del servizio](images/connect-custom-deploy2.png)

7.  Fare clic su **Avanti**.

### Funzionamento
{: #co-works}

Questa immagine mostra il supporto dell'ambiente personalizzato:

![Funzionamento della personalizzazione](images/custom-how-works.png)

È anche possibile fare riferimento ai seguenti link:

[AIOS payload logging API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/ai-openscale#publish-scoring-payload){: new_window}

[Custom deployment API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://aiopenscale-custom-deployement-spec.mybluemix.net/){: new_window}

[Python client binding SDK ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://ai-openscale-python-client.mybluemix.net/#bindings){: new_window}

[Working with Custom machine Learning engine ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/AI%20OpenScale%20and%20Custom%20ML%20Engine.ipynb){: new_window}

[Python SDK for IBM Watson OpenScale ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://pypi.org/project/ibm-ai-openscale/){: new_window}

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

  L'output del calcolo del punteggio sopra riportato deve essere accessibile da un endpoint di calcolo del punteggio attivo che {{site.data.keyword.aios_short}} può richiamare su REST. Per AzureML, SageMaker e WML, {{site.data.keyword.aios_short}} connette direttamente agli endpoint di calcolo del punteggio nativi, pertanto non occorre implementare la specifica di punteggio

### Passi successivi
{: #co-next}

{{site.data.keyword.aios_short}} ora è pronto per poter  [specificare un database](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
