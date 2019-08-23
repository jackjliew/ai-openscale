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

# Fehlerbehebung
{: #ts-trouble}

## Allgemeine Probleme für {{site.data.keyword.aios_full}}
{: #ts-trouble-common}

Die folgenden Probleme treten sowohl bei {{site.data.keyword.aios_full}} on Cloud als auch bei {{site.data.keyword.wos4d_full}} auf.

### Nutzdatenanalyse wird nicht korrekt angezeigt
{: #ts-trouble-common-payloadfileformat}

- Situation: Die folgende Fehlernachricht wird angezeigt:
  - Fehlercode: AIQDT0044E
  - Fehlertext: Nicht zulässiges Zeichen `"` im Spaltennamen `<Spaltenname>`

- Situation: Im Hinblick auf eine ordnungsgemäße Verarbeitung der Nutzdatenanalyse unterstützt {{site.data.keyword.aios_short}} keine Spaltennamen mit Anführungszeichen (") in den Nutzdaten. Dies betrifft sowohl Scoring-Nutzdaten als auch Feedbackdaten im CSV- und im JSON-Format.
- Lösung: Entfernen Sie die Anführungszeichen in den Spaltennamen der Datei mit den Nutzdaten.

## Für {{site.data.keyword.wos4d_full}} spezifische Probleme
{: #ts-trouble-icp}

Die folgenden Probleme sind spezifisch für {{site.data.keyword.wos4d_full}}:

## Service für Verzerrung und Fairness ist inaktiv
{: #ts-bfdown}

### Überblick
{: #ts-bfdov}

- Situation: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: etcd

### kubectl konfigurieren
{: #ts-bfdck}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-bfdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**2/2**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o <format>' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

    - Stellen Sie sicher, dass der Name des Image korrekt ist.
    - Haben Sie das Image in das Repository verschoben?
    - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Da dieser Pod über die drei Container 'aios-bias', 'ml-gateway-sidecar' und 'check-etcd-ready' verfügt, müssen Sie auch das Protokoll von 'ml-gateway-sidecar' und 'check-etcd-ready' überprüfen, wenn 'aios-bias' keine Probleme aufweist:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    In der Regel sollten die Protokolle Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus den Protokollen.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---
## {{site.data.keyword.aios_short}}-Service ist inaktiv
{: #ts-aiosdown}

### Überblick
{: #ts-odov}

- Situation: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: etcd

### kubectl konfigurieren
{: #ts-odkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole

    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-odvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

        Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

        - Fügen Sie weitere Knoten zum Cluster hinzu.

        - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
        ```bash
      kubectl -n [namespace] delete pod [pod name]
        ```

        - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

        - Stellen Sie sicher, dass der Name des Image korrekt ist.
        - Haben Sie das Image in das Repository verschoben?
        - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---
## {{site.data.keyword.aios_short}}-Konfigurationsservice ist inaktiv
{: #ts-aiosconfigdown}

### Überblick
{: #ts-ocdov}

- Situation: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: etcd

### kubectl konfigurieren
{: #ts-ocdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-ocdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-configuration-554f548667-7l782` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-Dashboardservice ist inaktiv
{: #ts-aiosdashdown}

### Überblick
{: #ts-oddov}

- Situation: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: Nicht zutreffend

### kubectl konfigurieren
{: #ts-oddkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-oddvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---
## Data Mart-Service ist inaktiv
{: #ts-datamartdown}

### Überblick
{: #ts-dmdov}

- Situation: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: etcd

### kubectl konfigurieren
{: #ts-dmdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-dmdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## Erklärbarkeitsservice ist inaktiv
{: #ts-expdown}

### Überblick
{: #ts-esdov}

- Situation: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: etcd

### kubectl konfigurieren
{: #ts-esdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-esdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**2/2**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Da dieser Pod über die drei Container 'explainability-service', 'ml-gateway-sidecar' und 'check-etcd-ready' verfügt, müssen Sie auch das Protokoll von 'ml-gateway-sidecar' und 'check-etcd-ready' überprüfen, wenn 'explainability-service' keine Probleme aufweist:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      In der Regel sollten die Protokolle Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus den Protokollen.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-Feedback-Service ist inaktiv
{: #ts-aiosfeedbackdown}

### Überblick
{: #ts-fsdov}

- Situation: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: etcd

### kubectl konfigurieren
{: #ts-fsdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-fsdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**2/2**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Da dieser Pod über die drei Container 'aios-feedback', 'ml-gateway-sidecar' und 'check-etcd-ready' verfügt, müssen Sie auch das Protokoll von 'ml-gateway-sidecar' und 'check-etcd-ready' überprüfen, wenn 'aios-feedback' keine Probleme aufweist:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      In der Regel sollten die Protokolle Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus den Protokollen.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-Erkennungsservice ist inaktiv
{: #ts-aiosdiscdown}

### Überblick
{: #ts-dsdov}

- Situation: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: Nicht zutreffend

### kubectl konfigurieren
{: #ts-dsdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Option 2: Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-dsdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-nginx-Service ist inaktiv
{: #ts-aiosnginxdown}

### Überblick
{: #ts-nsdov}

- Situation: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: Nicht zutreffend

### kubectl konfigurieren
{: #ts-nsdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-nsdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-API-Service für Nutzdatenprotokollierung ist inaktiv
{: #ts-aiospayloadapidown}

### Überblick
{: #ts-pladov}

- Situation: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine Nutzdaten von externen Services (Azur, Amazon, etc) in Service schreiben und verfügen somit nicht über aktuelle Daten für Analyse.
- Überwachungssystem:
- Abhängigkeiten: IBM Event Stream

### kubectl konfigurieren
{: #ts-pladkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-pladvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o <format>' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-Service für Nutzdatenprotokollierung ist inaktiv
{: #ts-aiospayloaddown}

### Überblick
{: #ts-plsdov}

- Situation: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine Nutzdaten von externen Services (Azur, Amazon, etc) in Service schreiben und verfügen somit nicht über aktuelle Daten für Analyse.
- Überwachungssystem:
- Abhängigkeiten: IBM Event Stream

### kubectl konfigurieren
{: #ts-plsdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-plsdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running  ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         6h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o <format>' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-Zeitplanungsservice ist inaktiv
{: #ts-aiosscheddown}

### Überblick
{: #ts-ssdov}

- Situation: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: Nicht zutreffend

### kubectl konfigurieren
{: #ts-ssdkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-ssdvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## {{site.data.keyword.aios_short}}-Redis-Service ist inaktiv
{: #ts-aiosredisdown}

### Überblick
{: #ts-redov}

- Situation: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: Nicht zutreffend

### kubectl konfigurieren
{: #ts-redkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-redvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    aios-redis-sentinel-6d5bffbcd8-hjvgk                          1/1       Running    0          14m
    aios-redis-sentinel-6d5bffbcd8-j4htd                          1/1       Running    0          14m
    aios-redis-sentinel-6d5bffbcd8-w4vcb                          1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-h4nfh                            1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-k9ggw                            1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-nlrr4                            1/1       Running    0          14m
    ```

    Stellen Sie sicher, dass der Status **Aktiv** (Running) lautet und der Pod vollständig bereit ist (**1/1**).  In den folgenden Beispielen wird `aios-redis-server-6f4c55fd75-nlrr4` als Pod verwendet.

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o <format>' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## etcd-Service ist inaktiv
{: #ts-etcddown}

### Überblick
{: #ts-etcov}

- Situation: etcd_micro_service_is_down:
- Auswirkung auf den Kunden: Kunden können keine der Funktionen wie etwa zum Konfigurieren neuer Instanzen, Analysieren von Anforderungen, Speichern von Nutzdaten usw. nutzen.
- Überwachungssystem:
- Abhängigkeiten: Keine

### kubectl konfigurieren
{: #ts-etckc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Schritte zur Verifizierung/Wiederherstellung
{: #ts-etcvr}

1.  Überprüfen Sie den Status des Pods mit den folgenden Befehlen:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    NAME                                         READY     STATUS    RESTARTS   AGE
    etcd-0                                       1/1       Running             3          8d
    etcd-1                                       1/1       Running             0          8d
    etcd-2                                       1/1       Running             0          8d
    ```

    Stellen Sie sicher, dass drei etcd-Pods vorhanden sind, ihr Status **Running** ist und sie vollständig bereit sind (**1/1**).

1.  Beschreiben Sie den Pod, falls er nicht aktiv ist:

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    Nach der Ausführung dieses Befehls werden die Details des Pods angezeigt.  So werden Fehler auch dann angegeben, wenn der Pod nicht aktiv ist.  Für Ihren Pod können die folgenden Fälle zutreffen, wenn er nicht aktiv ist:

    - **Pod verbleibt im Status 'Anstehend'**

      Wenn der Pod im Status **Anstehend** verbleibt, bedeutet dies, dass er nicht für einen Knoten terminiert werden kann.  Im Allgemeinen wird diese Terminierung dadurch verhindert, dass Ressourcen eines bestimmten Typs nicht in ausreichender Menge verfügbar sind.  Führen Sie den vorherigen Befehl aus, um weitere Informationen zu erhalten. Vom Scheduler sollten Nachrichten vorliegen, aus denen hervorgeht, warum der Pod nicht terminiert werden kann. Es kann sein, dass im Cluster nicht ausreichend CPU-Ressourcen oder Hauptspeicherressourcen vorhanden sind. In diesem Fall haben Sie mehrere Möglichkeiten:

      - Fügen Sie weitere Knoten zum Cluster hinzu.

      - Beenden Sie nicht benötigte Pods, um Ressourcen für anstehende Pods freizugeben.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Stellen Sie sicher, dass der Pod nicht größer als die Knoten ist. Beispiel: Wenn alle Knoten die CPU-Kapazität 1 aufweisen, kann ein Pod mit der Anforderung einer CPU-Kapazität von 1,1 nicht terminiert werden.

      Sie können die Knotenkapazitäten mit dem Befehl 'kubectl get nodes -o `<format>`' überprüfen. Nachfolgend werden einige Beispielbefehlszeilen aufgeführt, bei deren Ausführung nur die erforderlichen Informationen extrahiert werden:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Pod verbleibt im Status 'Wartend'**

      Wenn ein Pod im Status **Wartend** verbleibt, wurde er für einen Workerknoten terminiert, kann aber auf dieser Maschine nicht ausgeführt werden. Auch in diesem Fall müssten die Informationen, die nach Absetzen des Befehls 'kubectl describe ...' ausgegeben werden, hilfreich sein. Die häufigste Ursache für das Verbleiben eines Pods im Status **Wartend** ist ein Fehler beim Extrahieren des Image. Hierbei müssen drei Punkte überprüft werden:

      - Stellen Sie sicher, dass der Name des Image korrekt ist.
      - Haben Sie das Image in das Repository verschoben?
      - Führen Sie eine manuelle `Docker-Pull-Operation` zum Extrahieren des Image im Cluster aus, um zu überprüfen, ob das Image extrahiert werden kann.

    - **Pod fällt aus oder ist in keinem ordnungsgemäßen Zustand**

      Überprüfen Sie zunächst die Protokolle des aktuellen Containers:
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      Wenn der Container vorher ausgefallen ist, können Sie mithilfe des folgenden Befehls auf das Absturzprotokoll des vorherigen Containers zugreifen:
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      In der Regel sollte das Protokoll Informationen darüber enthalten, warum der Pod nicht erfolgreich gestartet wurde.  Beheben Sie das Problem basierend auf den Informationen aus dem Protokoll.  Wenn keine dieser Methoden funktioniert, fahren Sie mit den Eskalationsschritten fort.

---

## Dashboard mit Ereignisstrom erstellen
{: #ts-createdashes}

### Überblick
{: #ts-dshov}

- In diesem Dokument wird beschrieben, wie ein neues Dashboard zum Überwachen von {{site.data.keyword.aios_full}}-Services erstellt wird.

### kubectl konfigurieren
{: #ts-dshkc}

Es gibt zwei Möglichkeiten, den kubectl-Client zu konfigurieren.

1.  Mithilfe des cloudctl-Tools

    Wenn cloudctl auf dem Laptop verfügbar ist, führen Sie den folgenden Befehl aus, um kubectl zu konfigurieren:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    Ersetzen Sie `${username}`, `${password}` und `${ICP Host}` jeweils durch den entsprechenden Wert.  Beispiel:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  Mithilfe der kubectl-Konfiguration in der {{site.data.keyword.icpfull}}-Konsole
    - Melden Sie sich am {{site.data.keyword.icpfull}}-Cluster unter `https://${ICP Host}:8443` an.
    - Wählen Sie das **runde Personensymbol** und danach **Client konfigurieren** aus.
    - Klicken Sie auf das Symbol **In Zwischenablage kopieren**, um die Konfigurationsinformationen in die Zwischenablage zu kopieren.
    - Ändern Sie bei Bedarf den Namensbereich von `aiopenscale` in `es`.
    - Fügen Sie die Konfigurationsdaten in die Befehlszeile ein und drücken Sie die **Eingabetaste**.

### Ereignisstrom anzeigen
{: #ts-dshve}

Der Ereignisstrom besteht aus mehreren Services.  Details zu jedem Service finden Sie im jeweiligen Unterordner.

  ```bash
  $ kubectl get pods -n eventstream
  NAME                                                  READY     STATUS              RESTARTS   AGE
  es-ibm-es-access-controller-deploy-54cd9bc959-899s7   2/2       Running             0          20d
  es-ibm-es-access-controller-deploy-54cd9bc959-zcgx8   2/2       Running             0          16d
  es-ibm-es-kafka-sts-0                                 4/4       Running             15         17d
  es-ibm-es-kafka-sts-1                                 4/4       Running             264        15d
  es-ibm-es-kafka-sts-2                                 4/4       Running             370        22d
  es-ibm-es-proxy-deploy-5866fbd8cb-jk6rd               1/1       Running             0          9d
  es-ibm-es-proxy-deploy-5866fbd8cb-rjx5q               1/1       Running             0          9d
  es-ibm-es-rest-deploy-585df7f77c-j2d5k                3/3       Running             0          22d
  es-ibm-es-ui-deploy-6f59c7764c-7tlzn                  3/3       Running             55         16d
  es-ibm-es-zookeeper-sts-0                             1/1       Running             0          17d
  es-ibm-es-zookeeper-sts-1                             1/1       Running            ai-open-scale-ibm-aios-scheduling  | 1 | Scheduling service         15d
  es-ibm-es-zookeeper-sts-2                             1/1       Running   488        9d
  ```

---

## {{site.data.keyword.aios_short}}-Überwachung verwenden
{: #ts-aiosusemonitor}

### Überblick
{: #ts-omov}

- In diesem Dokument wird beschrieben, wie ein neues Dashboard zum Überwachen von {{site.data.keyword.aios_full}}-Services erstellt wird.

### Dashboard einrichten
{: #ts-omsd}

- Beziehen Sie die Datei 'aios-dashboard.json' aus 'ibm-aiopenscale-x86_64-1.0.0.tar.gz'.  Diese Datei befindet sich im Verzeichnis `utils`.
- Melden Sie sich am ICP-Cluster unter `https://${ICP Host}:8443` an.
- Wählen Sie `Menü` > `Plattform` > `Überwachung`aus.
- Klicken Sie auf das Symbol `Home`.
- Klicken Sie auf das Menüelement `Dashboard importieren`.
- Klicken Sie auf die Schaltfläche `JSON-Datei hochladen` und zeigen Sie auf die Datei 'aios-dashboard.json'.
- Wählen Sie `prometheus` für das Prometheus-Eingabefeld aus.

### Dashboard anzeigen
{: #ts-omvd}

Das Dashboard besteht aus den folgenden Zeilen:

- Gesamte Clusternutzung

  In dieser Zeile wird die clusterweite CPU-, Speicher- und Dateisystemnutzung angezeigt. Die Tachometer zeigen an, ob sich der Cluster in einem einwandfreiem Zustand befindet. Falls die Tachometer anzeigen, dass sich der Cluster nicht in einwandfreiem Zustand befindet, fügen Sie weitere Cluster zum Knoten hinzu oder beenden Sie nicht benötigte Pods, um Platz für andere Bereitstellungen zu schaffen.

- Verfügbarkeit nach Service

  In dieser Zeile wird die Verfügbarkeit für jeden einzelnen Service angezeigt.  Die Eingangsanzeigen zeigen die Gesamtzahl der bereiten Container an.  Wenn der Tachometer einen Wert von 100 % anzeigt, befindet sich {{site.data.keyword.aios_short}} in einwandfreiem Zustand.  Andernfalls können Sie anhand der Tabelle überprüfen, welcher Service inaktiv ist, um diesen Service mit entsprechenden Maßnahmen schließlich wieder zu aktivieren.  Wenn ein Container nicht erfolgreich gestartet wurde, gibt es als Unterstützung für die Diagnose noch weitere {{site.data.keyword.aios_short}}-Runbooks.  Den Eingangsanzeigen folgen die Anzeigen für einzelne Services. In den verschiedenen Zeilen wird die Anzahl der bereiten Container und die Anzahl der angeforderten Container angezeigt.

- CPU nach Service

  Diese Zeile zeigt die CPU-Auslastung für jeden Service an und enthält die Anzahl der CPU-Kerne, die jeder Container verwendet, sowie die maximale Anzahl von CPU-Kernen, die jeder Container verwenden kann.  Falls diese Werte zu nahe beieinander liegen, prüfen Sie, warum der Container zu viel CPU-Ressourcen verbraucht.  Bei Bedarf können Sie den Grenzwert für die CPU für diesen Container durch eine Bearbeitung der Bereitstellung und Aktualisierung des CPU-Grenzwerts erhöhen:
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Beispiel:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Hauptspeicher nach Service

  Diese Zeile zeigt die Hauptspeichernutzung für jeden Service an und enthält die Menge an Hauptspeicher, die jeder Container verwendet, sowie die maximale Menge an Hauptspeicher, die jeder Container verwenden kann.  Falls diese Werte zu nahe beieinander liegen, prüfen Sie, warum der Container zu viel Hauptspeicher verbraucht.  Bei Bedarf können Sie den Hauptspeicher für diesen Container durch eine Bearbeitung der Bereitstellung und Aktualisierung des Hauptspeichergrenzwerts erhöhen:
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Beispiel:
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Dateisystem nach Service

  In dieser Zeile wird die Dateisystemnutzung für jeden einzelnen Service angezeigt.  Falls das Überwachungsprogramm anzeigt, dass die Dateisystemnutzung kontinuierlich ansteigt, sollten Sie den Container überprüfen, um festzustellen, warum die Nutzung durch das Dateisystem zunimmt.  Bei Bedarf können Sie Kontakt zum zuvor genannten Slack-Kanal aufnehmen, um weitere Hilfe zu erhalten.

- Images und Versionen

  In dieser Zeile werden alle Images und Versionen aufgelistet, die für {{site.data.keyword.aios_full}} verwendet werden.
