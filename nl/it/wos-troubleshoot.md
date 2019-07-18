---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


keywords: troubleshooting, bias

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

# Risoluzione dei problemi
{: #ts-trouble}

## Problemi comuni per {{site.data.keyword.aios_full}}
{: #ts-trouble-common}

Le seguenti problematiche sono comuni sia a {{site.data.keyword.aios_full}} on Cloud che a {{site.data.keyword.wos4d_full}}.

### L'analytics del payload non viene visualizzata correttamente
{: #ts-trouble-common-payloadfileformat}

- Situazione: viene visualizzato il seguente messaggio di errore:
  - codice di errore: AIQDT0044E
  - testo dell'errore: carattere non consentito `"` nel nome colonna `<column name>`

- Situazione: per una corretta elaborazione dell'analytics del payload, {{site.data.keyword.aios_short}} non supporta i nomi di colonna con virgolette (") nel payload. Ciò influisce sui dati di feedback e payload di calcolo del punteggio nei formati CSV e JSON.
- Soluzione: rimuovere le virgolette (") dai nomi colonna del file del payload.

## Problemi specifici di {{site.data.keyword.wos4d_full}}
{: #ts-trouble-icp}

Le seguenti problematiche sono specifiche per {{site.data.keyword.wos4d_full}}:

## Il servizio distorsione/correttezza è inattivo
{: #ts-bfdown}

### Panoramica
{: #ts-bfdov}

- Situazione: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: etcd

### Configurare kubectl
{: #ts-bfdck}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-bfdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NOME                                                           PRONTO    STATO          RIAVVII   DURATA
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       In esecuzione  0         2h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **2/2**.  Verrà utilizzato `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o <format>. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

    - Assicurarsi di avere il nome dell'immagine corretta.
    - Assicurarsi di aver immesso l'immagine nel repository.
    - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Poiché questo pod ha 3 contenitori, aios-bias, ml-gateway-sidecar e check-etcd-ready, è opportuno consultare anche il log di ml-gateway-sidecar e check-etcd-ready se aios-bias non ha problemi:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    In generale, i log contengono informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni dei log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---
## Il servizio {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosdown}

### Panoramica
{: #ts-odov}

- Situazione: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload . . .
- Sistema di monitoraggio:
- Dipendenze: etcd

### Configurare kubectl
{: #ts-odkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}

    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-odvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NOME                                                           PRONTO    STATO         RIAVVII   DURATA
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       In esecuzione 1         6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

        Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

        - Aggiungere altri nodi al cluster.

        - Terminare i pod non necessari per fare spazio per i pod in sospeso.
        ```bash
      kubectl -n [namespace] delete pod [nome pod]
        ```

        - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

        - Assicurarsi di avere il nome dell'immagine corretta.
        - Assicurarsi di aver immesso l'immagine nel repository.
        - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---
## Il servizio di configurazione {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosconfigdown}

### Panoramica
{: #ts-ocdov}

- Situazione: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: etcd

### Configurare kubectl
{: #ts-ocdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
  ```

  Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-ocdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NOME                                                     PRONTO    STATO         RIAVVII    DURATA
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       In esecuzione 1          6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-configuration-554f548667-7l782` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio dashboard {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosdashdown}

### Panoramica
{: #ts-oddov}

- Situazione: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: N/A

### Configurare kubectl
{: #ts-oddkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-oddvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NOME                                                           PRONTO    STATO       RIAVVII    DURATA
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       In esecuzione 0          4h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---
## Il servizio Data Mart è disattivo
{: #ts-datamartdown}

### Panoramica
{: #ts-dmdov}

- Situazione: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: etcd

### Configurare kubectl
{: #ts-dmdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-dmdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NOME                                                        PRONTO    STATO         RIAVVII   DURATA
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb             1/1       In esecuzione 1         6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio Esplicabilità è inattivo
{: #ts-expdown}

### Panoramica
{: #ts-esdov}

- Situazione: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: etcd

### Configurare kubectl
{: #ts-esdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-esdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NOME                                                           PRONTO    STATO         RIAVVII    DURATA
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984          2/2       In esecuzione 0          4h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **2/2**.  Verrà utilizzato `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Poiché questo pod ha 3 contenitori, explainability-service, ml-gateway-sidecar e check-etcd-ready, è opportuno consultare anche il log di ml-gateway-sidecar e check-etcd-ready se explainability-service non ha problemi:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      In generale, i log contengono informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni dei log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio feedback {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosfeedbackdown}

### Panoramica
{: #ts-fsdov}

- Situazione: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: etcd

### Configurare kubectl
{: #ts-fsdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-fsdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NOME                                                        PRONTO    STATO         RIAVVII   DURATA
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f             2/2       In esecuzione 1         6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **2/2**.  Verrà utilizzato `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Poiché questo pod ha 3 contenitori, aios-feedback, ml-gateway-sidecar e check-etcd-ready, è opportuno consultare anche il log di ml-gateway-sidecar e check-etcd-ready se aios-feedback non ha problemi:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      In generale, i log contengono informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni dei log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio di rilevamento {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosdiscdown}

### Panoramica
{: #ts-dsdov}

- Situazione: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: N/A

### Configurare kubectl
{: #ts-dsdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Opzione 2: Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-dsdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NOME                                                            PRONTO    STATO         RIAVVII   DURATA
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt    1/1       In esecuzione 1         6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio nginx {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosnginxdown}

### Panoramica
{: #ts-nsdov}

- Situazione: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: N/A

### Configurare kubectl
{: #ts-nsdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-nsdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NOME                                                      PRONTO    STATO         RIAVVII    DURATA
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5             1/1       In esecuzione 0          4h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio API di registrazione payload {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiospayloadapidown}

### Panoramica
{: #ts-pladov}

- Situazione: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- Impatto sul cliente: i clienti non possono scrivere il payload sul nostro servizio da servizi esterni (Azur, Amazon, altri), pertanto i clienti non hanno dati correnti per l'analisi.
- Sistema di monitoraggio:
- Dipendenze: IBM Event Stream

### Configurare kubectl
{: #ts-pladkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-pladvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NOME                                                           PRONTO    STATO         RIAVVII   DURATA
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       In esecuzione 1         6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o <format>. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio di registrazione payload {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiospayloaddown}

### Panoramica
{: #ts-plsdov}

- Situazione: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- Impatto sul cliente: i clienti non possono scrivere il payload sul nostro servizio da servizi esterni (Azur, Amazon, altri), pertanto i clienti non hanno dati correnti per l'analisi.
- Sistema di monitoraggio:
- Dipendenze: IBM Event Stream

### Configurare kubectl
{: #ts-plsdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP`}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-plsdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NOME                                                           PRONTO    STATO          RIAVVII    DURATA
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       In esecuzione   1          6h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o <format>. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio di pianificazione {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosscheddown}

### Panoramica
{: #ts-ssdov}

- Situazione: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: N/A

### Configurare kubectl
{: #ts-ssdkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${ICP Host}`:8443
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-ssdvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NOME                                                      PRONTO    STATO         RIAVVII    DURATA
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww        1/1       In esecuzione 0          2h
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio redis {{site.data.keyword.aios_short}} è disattivo
{: #ts-aiosredisdown}

### Panoramica
{: #ts-redov}

- Situazione: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: N/A

### Configurare kubectl
{: #ts-redkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-redvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    NOME                                                          PRONTO    STATO        RIAVVII  DURATA
    aios-redis-sentinel-6d5bffbcd8-hjvgk                          1/1       In esecuzione  0      14m
    aios-redis-sentinel-6d5bffbcd8-j4htd                          1/1       In esecuzione  0      14m
    aios-redis-sentinel-6d5bffbcd8-w4vcb                          1/1       In esecuzione  0      14m
    aios-redis-server-6f4c55fd75-h4nfh                            1/1       In esecuzione  0      14m
    aios-redis-server-6f4c55fd75-k9ggw                            1/1       In esecuzione  0      14m
    aios-redis-server-6f4c55fd75-nlrr4                            1/1       In esecuzione  0      14m
    ```

    Assicurarsi che lo stato sia **In esecuzione** e che sia completamente pronto **1/1**.  Verrà utilizzato `aios-redis-server-6f4c55fd75-nlrr4` come pod per i seguenti esempi.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o <format>. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Il servizio etcd è disattivo
{: #ts-etcddown}

### Panoramica
{: #ts-etcov}

- Situazione: etcd_micro_service_is_down:
- Impatto sul cliente: i clienti non possono utilizzare funzionalità come la configurazione di nuove istanze, l'analisi delle richieste, l'archiviazione del payload...
- Sistema di monitoraggio:
- Dipendenze: Nessuna

### Configurare kubectl
{: #ts-etckc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n aiopenscale
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Passi di verifica/ripristino
{: #ts-etcvr}

1.  Controllare lo stato del pod con i seguenti comandi:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    NOME                                         PRONTO    STATO               RIAVVII    DURATA
    etcd-0                                       1/1       In esecuzione       3          8g
    etcd-1                                       1/1       In esecuzione       0          8g
    etcd-2                                       1/1       In esecuzione       0          8g
    ```

    Assicurarsi che ci siano tre pod etcd, che il loro stato sia **In  esecuzione** e siano completamente pronti **1/1**.

1.  Descrivere il pod se il pod non è in fase di esecuzione:

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    Questo comando visualizzerà i dettagli relativi al pod.  Indica anche gli errori se il pod non è in fase di esecuzione.  Il pod potrebbe incontrare i seguenti problemi quando non è in fase di esecuzione:

    - **Il pod rimane in sospeso**

      Se il pod rimane **In sospeso**, significa che non può essere pianificato su un nodo.  Generalmente questo si verifica perché non ci sono risorse sufficienti di un certo tipo e ciò impedisce la pianificazione.  Eseguire il comando precedente per ottenere ulteriori informazioni. Ci dovrebbero essere messaggi dal programma di pianificazione sul perché non è possibile pianificare il pod. Potrebbe essersi esaurita la fornitura di CPU o memoria nel cluster. In questo caso è possibile tentare diverse azioni:

      - Aggiungere altri nodi al cluster.

      - Terminare i pod non necessari per fare spazio per i pod in sospeso.
      ```bash
      kubectl -n [namespace] delete pod [nome pod]
      ```

      - Verificare che il pod non sia più grande dei nodi. Ad esempio, se tutti i nodi hanno una capacità di cpu:1, un pod con una richiesta di cpu: 1.1 non sarà mai pianificato.

      È possibile verificare le capacità del nodo con il comando kubectl get nodes -o `<format>`. Ecco alcuni comandi di esempio per estrarre solo le informazioni necessarie:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Il pod rimane In attesa**

      Se un pod è bloccato nello stato **In attesa**, è stato pianificato su un nodo di lavoro, ma non può essere eseguito su quella macchina. Di nuovo, le informazioni da kubectl describe ... dovrebbe essere informative. La causa più comune dei pod **In attesa** è un errore di pull
dell'immagine. Ci sono tre cose da controllare:

      - Assicurarsi di avere il nome dell'immagine corretta.
      - Assicurarsi di aver immesso l'immagine nel repository.
      - Eseguire un `docker pull` manuale per estrarre l'immagine sul cluster per vedere se l'immagine può essere estratta.

    - **Il pod è in crash o altrimenti malfunzionante**

      Innanzitutto, controllare i log del contenitore corrente:
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      Se si è verificato un crash del contenitore in precedenza, è possibile accedere al log del crash del contenitore precedente con:
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      In generale, il log contiene informazioni sul perché il pod non si è avviato correttamente.  Correggere il problema in base alle informazioni del log.  Se nessuno di questi approcci funziona, continuare con i passi di escalation

---

## Creare un dashboard con event_stream
{: #ts-createdashes}

### Panoramica
{: #ts-dshov}

- Questo documento descrive come creare un nuovo dashboard per monitorare i servizi {{site.data.keyword.aios_full}}.

### Configurare kubectl
{: #ts-dshkc}

Ci sono due modi per configurare il client kubectl.

1.  Utilizzando lo strumento cloudctl

    Se cloudctl è disponibile sul laptop, eseguire il seguente comando per configurare kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${host ICP}:8443` -n es
    ```
    Sostituire `${username}`,  `${password}`, `${host ICP}` con i valori reali.  Ad esempio:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  Utilizzando la configurazione kubectl dalla console {{site.data.keyword.icpfull}}
    - Accedere al cluster {{site.data.keyword.icpfull}} `https://${host ICP}:8443`
    - Selezionare l'icona **persona nel cerchio** > **Configura client**
    - Fare clic sull'icona **Copia negli appunti** per copiare le informazioni di configurazione negli appunti
    - Modificare il namespace da `aiopenscale` a `es`, se necessario.
    - Incollare le informazioni di configurazione nella riga comandi e premere **Invio**.

### Visualizzazione il flusso di eventi
{: #ts-dshve}

Il flusso di eventi è composto da diversi servizi.  Vedere la sottocartella per i dettagli su ogni servizio.

  ```bash
  $ kubectl get pods -n eventstream
  NOME                                                  PRONTO    STATO              RIAVVII     DURATA
  es-ibm-es-access-controller-deploy-54cd9bc959-899s7   2/2       In esecuzione       0          20g
  es-ibm-es-access-controller-deploy-54cd9bc959-zcgx8   2/2       In esecuzione       0          16g
  es-ibm-es-kafka-sts-0                                 4/4       In esecuzione       15         17g
  es-ibm-es-kafka-sts-1                                 4/4       In esecuzione       264        15g
  es-ibm-es-kafka-sts-2                                 4/4       In esecuzione       370        22g
  es-ibm-es-proxy-deploy-5866fbd8cb-jk6rd               1/1       In esecuzione       0          9g
  es-ibm-es-proxy-deploy-5866fbd8cb-rjx5q               1/1       In esecuzione       0          9g
  es-ibm-es-rest-deploy-585df7f77c-j2d5k                3/3       In esecuzione       0          22g
  es-ibm-es-ui-deploy-6f59c7764c-7tlzn                  3/3       In esecuzione       55         16g
  es-ibm-es-zookeeper-sts-0                             1/1       In esecuzione       0          17g
  es-ibm-es-zookeeper-sts-1                             1/1       In esecuzione       1          15g
  es-ibm-es-zookeeper-sts-2                             1/1       In esecuzione       488        9g
  ```

---

## Utilizzo del monitoraggio {{site.data.keyword.aios_short}}
{: #ts-aiosusemonitor}

### Panoramica
{: #ts-omov}

- Questo documento descrive come creare un nuovo dashboard per monitorare i servizi {{site.data.keyword.aios_full}}.

### Configurazione del dashboard
{: #ts-omsd}

- Ottenere il file aios-dashboard.json da ibm-aiopenscale-x86_64-1.0.0.tar.gz.  Questo file può essere trovato dalla directory `utils`.
- Accedere al cluster ICP `https://${host ICP}:8443`
- Selezionare `Menu` > `Piattaforma` > `Monitoraggio`
- Fare clic sull'icona `Home`
- Fare clic sulla voce di menu `Importa dashboard`
- Fare clic sul pulsante `Carica file .json` e puntare al proprio aios-dashboard.json
- Selezionare `prometheus` per il campo di input prometheus

### Visualizzazione del dashboard
{: #ts-omvd}

Il dashboard è costituito dalle seguenti righe:

- Utilizzo totale cluster

  Questa riga mostra l'utilizzo CPU a livello di cluster, l'utilizzo della memoria e l'utilizzo del file system. I contatori mostrano se il cluster è in buono stato. Se non appare in buono stato, aggiungere più nodi al cluster o terminare i pod non necessari per fare spazio per altre distribuzioni.

- Disponibilità per servizio

  Questa riga mostra la disponibilità per ogni servizio.  I pannelli iniziali mostrano i contenitori totali pronti.  Se il contatore viene visualizzato al 100%,  {{site.data.keyword.aios_short}} è in buono stato.  Altrimenti, vedere la tabella per scoprire quale servizio è inattivo e intraprendere l'azione opportuna per riattivarlo.  Ci sono altri runbook {{site.data.keyword.aios_short}} che aiutano a diagnosticare il motivo per cui un contenitore non si è avviato correttamente.  Dopo i pannelli iniziali ci sono i pannelli per i singoli servizi. Linee diverse mostrano il numero di contenitori pronti e che sono richiesti.

- CPU per servizio

  Questa riga mostra l'utilizzo di CPU per ogni servizio e include il numero di core CPU che ogni contenitore utilizza e il numero limite di core CPU che ogni contenitore può utilizzare.  Se questi valori sono troppo vicini, controllare il motivo per cui il contenitore consuma troppa risorsa cpu.  Se necessario, è possibile aumentare il limite di cpu per quel contenitore modificando la distribuzione e aggiornando il limite di cpu:
  ```bash
  kubectl -n aiopenscale edit deployment ${nome distribuzione}
  ```

  Esempio:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Memoria per servizio

  Questa riga mostra l'utilizzo di memoria per ogni servizio e include la memoria che ogni contenitore utilizza e la memoria che ogni contenitore può utilizzare.  Se questi valori sono troppo vicini, controllare il motivo per cui il contenitore consuma troppa memoria.  Se necessario, è possibile aumentare la memoria per quel contenitore modificando la distribuzione e aggiornando il limite di memoria:
  ```bash
  kubectl -n aiopenscale edit deployment ${nome distribuzione}
  ```

  Esempio:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Filesystem per servizio

  Questa riga mostra l'utilizzo del filesystem per ogni servizio.  Se il monitor mostra l'uso del file system costantemente in aumento, ispezionare il contenitore per capire perché l'utilizzo del filesystem continua ad aumentare.  Se necessario, è possibile contattare il precedente canale Slack per ulteriore aiuto.

- Immagini e versioni

  Questa riga elenca tutte le immagini e le versioni utilizzate per {{site.data.keyword.aios_full}}.
