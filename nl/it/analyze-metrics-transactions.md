---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Analisi delle metriche e delle transazioni ![tag beta](images/beta.png)
{: #anlz_metrics}

È possibile utilizzare {{site.data.keyword.aios_full}} per analizzare le metriche e le transazioni tramite varie modalità.
{: shortdesc}

## Metriche di correttezza
{: #anlz_metrics_fairness}

Utilizzare il monitoraggio della correttezza per determinare se i risultati prodotti dal modello sono corretti o meno per il gruppo monitorato. Quando il monitoraggio della correttezza è abilitato, genera una serie di metriche ogni ora per impostazione predefinita. È possibile generare queste metriche on-demand facendo clic sul pulsante **Controlla qualità ora** o utilizzando il client Python.

Le metriche di correttezza sono calcolate in base alle seguenti informazioni:

- calcolo del punteggio dei dati del payload.

Al fine di un corretto monitoraggio, ogni richiesta di calcolo del punteggio dovrebbe essere registrata anche in {{site.data.keyword.aios_short}}. La registrazione dei dati di payload è automatizzata per i motori {{site.data.keyword.pm_full}}.

Per altri motori di machine learning, i dati del payload possono essere forniti utilizzando il client Python o l'API REST.

Per i motori di machine learning diversi da {{site.data.keyword.pm_full}}, il monitoraggio della correttezza crea ulteriori richieste di calcolo del punteggio sulla distribuzione monitorata.
{: note}

È possibile esaminare tutti i valori di metrica nel tempo sul dashboard {{site.data.keyword.aios_short}}:

![grafico delle metriche di correttezza che mostra la deviazione al di sotto della soglia](images/fairness_metrics_001.png)

È possibile esaminare i dettagli correlati, ad esempio risultati favorevoli e sfavorevoli:

![dettagli correttezza](images/fairness_metrics_002.png)

È possibile visualizzare transazioni dettagliate:

![un grafico della correttezza che mostra un elenco di transazioni](images/fairness_metrics_003.png)

È possibile visualizzare l'endpoint di calcolo del punteggio senza distorsione consigliato:

![dettagli dell'endpoint di calcolo del punteggio senza distorsione](images/fairness_metrics_004.png)

### Metriche di correttezza supportate
{: #anlz_metrics_supfairmets}

Le seguenti metriche di correttezza sono supportate da {{site.data.keyword.aios_short}}:

#### Correttezza per un gruppo
{: #anlz_metrics_supfairmets_group}

- **Descrizione**: la propensione del modello ad offrire risultati favorevoli ad un gruppo rispetto a un altro.
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**: l'endpoint di calcolo del punteggio senza distorsione che è possibile utilizzare nell'applicazione aziendale per ricevere risposte senza distorsione dal modello distribuito.
- **Tipo di problema**: tutti
- **Tipo di dati**: strutturati
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: sì

### Dettagli di correttezza supportati
{: #anlz_metrics_supfairdets}

I seguenti dettagli delle metriche di correttezza sono supportati da {{site.data.keyword.aios_short}}:

- Le percentuali di risultati favorevoli per ciascuno dei gruppi
- Le medie di correttezza per tutti i gruppi di correttezza

  Rapporto impatto eterogeneo = (% di risultati favorevoli nel gruppo monitorato) / (% di risultati favorevoli nel gruppo di riferimento)

- Distribuzione dei dati per ciascuno dei gruppi monitorati
- Distribuzione dei dati del payload


<!---
BTW, I propose to use screenshots with data from FastPath.
Source monitored group or referenced group
Source of bias is also in fairness metrics
--->


## Metriche di qualità
{: #anlz_metrics_quality}

Utilizzare il monitoraggio della qualità per determinare la precisione con cui il modello predice i risultati. Quando il monitoraggio della qualità è abilitato, genera una serie di metriche ogni ora per impostazione predefinita. È possibile generare queste metriche on-demand facendo clic sul pulsante **Controlla qualità ora** o utilizzando il client Python.

Le metriche di qualità sono calcolate in base alle seguenti informazioni:

- dati di feedback etichettati manualmente,
- risposte della distribuzione monitorata per questi dati.

Per un corretto monitoraggio, i dati di feedback devono essere registrati in {{site.data.keyword.aios_short}} su base regolare. I dati di feedback possono essere forniti utilizzando l'opzione "Aggiungi dati di feedback" o utilizzando il client Python o l'API REST.

Per i motori di machine learning diversi da {{site.data.keyword.aios_short}}, il monitoraggio della qualità crea ulteriori richieste di calcolo del punteggio sulla distribuzione monitorata.
{: note}

È possibile esaminare tutti i valori di metrica nel tempo sul dashboard {{site.data.keyword.aios_short}}:

![grafico delle metriche di qualità che mostra la deviazione dell'area sotto la curva di ROC](images/quality_metrics_001.png)


Per esaminare i dettagli correlati, ad esempio la matrice di confusione per la classificazione binaria e multi-classe, disponibile per alcune metriche, fare clic sul grafico.

![tabella dei dettagli delle metriche di qualità](images/quality_metrics_002.png)

### Metriche di qualità supportate
{: #anlz_metrics_supqualdets}

Le seguenti metriche di qualità sono supportate da {{site.data.keyword.aios_short}}:

#### Area sotto la curva ROC
{: #anlz_metrics_supqualdets_roc}

- **Descrizione**: l'rea sotto la curva della percentuale di richiami e falsi positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Area sotto la curva PR
{: #anlz_metrics_supqualdets_pr}

- **Descrizione**: l'area sotto la curva di precisione e richiamo
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Varianza spiegata dalla proporzione
{: #anlz_metrics_supqualdets_var}

- **Descrizione**: la varianza spiegata dalla proporzione rappresenta il rapporto tra varianza spiegata e varianza obiettivo. La varianza spiegata indica la differenza tra varianza obiettivo e varianza dell'errore di previsione.
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

#### Errore assoluto medio
{: #anlz_metrics_supqualdets_abserror}

- **Descrizione**: la media della differenza assoluta tra previsione del modello e valore obiettivo
- **Soglie predefinite**: limite superiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

#### Errore quadratico medio
{: #anlz_metrics_supqualdets_squerror}

- **Descrizione**: la media della differenza quadratica tra previsione del modello e valore obiettivo
- **Soglie predefinite**: limite superiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

#### R quadro
{: #anlz_metrics_supqualdets_r_squared}

- **Descrizione**: il rapporto di differenza tra la varianza obiettivo e la varianza dell'errore di previsione rispetto alla varianza obiettivo
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

#### Radice dell'errore quadratico medio
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Descrizione**: la radice quadrata della media della differenza quadratica tra previsione del modello e valore obiettivo
- **Soglie predefinite**: limite superiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: regressione
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

#### Accuratezza
{: #anlz_metrics_supqualdets_acc}

- **Descrizione**: la proporzione di previsioni corrette
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipi di problema**: classificazione binaria e classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Tasso ponderato di veri positivi (wTPR - Weighted True Positive Rate)
{: #anlz_metrics_supqualdets_wtpr}

- **Descrizione**: la media ponderata della classe TPR con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Tasso di veri positivi (TPR - True positive rate)
{: #anlz_metrics_supqualdets_tpr}

- **Descrizione**: la proporzione delle previsioni corrette nelle previsioni della classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Tasso ponderato di falsi positivi (wFPR - Weighted False Positive Rate)
{: #anlz_metrics_supqualdets_wfpr_weighted}

- **Descrizione**: la media ponderata della classe FPR con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Tasso di falsi positivi (FPR - False positive rate)
{: #anlz_metrics_supqualdets_fpr_false}

- **Descrizione**: la proporzione di previsioni errate nella classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Richiamo ponderato
{: #anlz_metrics_supqualdets_weighted_recall}

- **Descrizione**: la media ponderata del richiamo con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Richiamo
{: #anlz_metrics_supqualdets_recall}

- **Descrizione**: la proporzione di previsioni corrette nella classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Precisione ponderata
{: #anlz_metrics_supqualdets_wgth_prec}

- **Descrizione**: la media ponderata della precisione con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Precisione
{: #anlz_metrics_supqualdets_precision}

- **Descrizione**: la proporzione delle previsioni corrette nelle previsioni della classe dei positivi
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Misura F1 ponderata
{: #anlz_metrics_supqualdets_wght_f1-measure}

- **Descrizione**: la media ponderata della misura F1 con pesi uguali alla probabilità della classe
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Misura F1
{: #anlz_metrics_supqualdets_f1-measr}

- **Descrizione**: la media armonica di precisione e richiamo
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipo di problema**: classificazione binaria
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: matrice di confusione

#### Perdita logaritmica
{: #anlz_metrics_supqualdets_log_loss}

- **Descrizione**: la media delle probabilità della classe obiettivo dei logaritmi (confidenza). È nota anche come Probabilità log prevista.
- **Soglie predefinite**: limite inferiore = 80%
- **Raccomandazione predefinita**:
   - **Andamento crescente**: un andamento crescente indica che la metrica sta migliorando. Ciò significa che il nuovo training del modello è efficace.
   - **Andamento decrescente**: un andamento decrescente indica che la metrica sta peggiorando. I dati di feedback stanno riportando differenze significative rispetto ai dati di training.
   - **Variazione anomala o irregolare**: una variazione anomala o irregolare indica che i dati di feedback non sono congruenti tra le valutazioni. Incrementare la dimensione minima del campione per il monitor Qualità.
- **Tipi di problema**: classificazione binaria e classificazione multi-classe
- **Valori del grafico**: ultimo valore nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

### Dettagli di qualità supportati
{: #anlz_metrics_supqualdets_suppr_dets}

I seguenti dettagli delle metriche di qualità sono supportati da {{site.data.keyword.aios_short}}:

#### Matrice di confusione
{: #anlz_metrics_supqualdets_confusion}

La matrice di confusione consente di comprendere per quale dei dati di feedback la risposta della distribuzione monitorata è corretta e per la quale non lo è.

## Metriche delle prestazioni
{: #anlz_metrics_performance}

Utilizzare il monitoraggio delle prestazioni per conoscere la velocità dei record di dati elaborati dalla distribuzione. È possibile abilitare il monitoraggio delle prestazioni quando si seleziona la distribuzione che deve essere tracciata e monitorata da {{site.data.keyword.aios_short}}.

Le metriche di prestazione sono calcolate in base alle seguenti informazioni:

- calcolo del punteggio dei dati del payload

Al fine di un corretto monitoraggio, ogni richiesta di calcolo del punteggio dovrebbe essere registrata anche in {{site.data.keyword.aios_short}}. La registrazione dei dati di payload è automatizzata per i motori {{site.data.keyword.pm_full}}. Per altri motori di machine learning, i dati del payload possono essere forniti utilizzando il client Python o l'API REST. Il monitoraggio delle prestazioni non crea ulteriori richieste di calcolo del punteggio sulla distribuzione monitorata.

È possibile esaminare i valori delle metriche di prestazione nel tempo sul dashboard {{site.data.keyword.aios_short}}:

![grafico prestazioni](images/performance_metrics_001.png)

### Metriche delle prestazioni supportate
{: #anlz_metrics_performance_supp_quality_mets}

Le seguenti metriche delle prestazioni sono supportate da {{site.data.keyword.aios_short}}:

#### Velocità di trasmissione dei dati
{: #anlz_metrics_performance_supp_quality_mets_through}

- **Descrizione**: la media delle richieste di calcolo del punteggio al minuto in un periodo di tempo specifico
- **Soglie predefinite**: non applicabile
- **Raccomandazione predefinita**: non applicabile
- **Tipo di problema**: tutti
- **Valori del grafico**: valore medio nel periodo di tempo
- **Dettagli di metriche disponibili**: nessuno

## Analytics dei dati di payload
{: #anlz_metrics_payload}

È possibile analizzare il payload del calcolo del punteggio che viene inviato alla propria distribuzione nell'intervallo di dati selezionato tramite uno dei seguenti metodi:

- Riesaminando le classi di previsione e la distribuzione della confidenza in ogni classe
   
   ![un grafico che associa la previsione per distribuzione di confidenza](images/by_confidence.png)
   
- Tramite grafico personalizzato (selezionando tra le funzioni, le classi di previsione e la confidenza)
   
   ![un grafico che mostra la funzione previsione per il genere in base alla funzione età](images/by_custom_chart.png)

