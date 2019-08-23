---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Spiegazione transazioni
{: #ie-ov}

Per ogni distribuzione, è possibile vedere i dati di esplicabilità per transazioni specifiche. Le transazioni vengono visualizzate solo quando ci sono i dati per supportare i monitor e si basano sulle soglie impostate, l'ora in cui  è pianificata l'esecuzione dei monitor e la disponibilità dei dati di payload da {{site.data.keyword.pm_full}}.
{: shortdesc}

## Visualizzazione delle spiegazioni per ID transazione
{: #ie-view}

1. Fare clic su un riquadro di distribuzione.
2. Fare clic sulla scheda **Spiega una transazione** (![scheda Spiega una transazione](images/insight-transact-tab.png)) nel navigator.
3. Immettere un ID transazione.

Ogni volta che i dati vengono inviati al modello per il calcolo del punteggio, imposta un ID transazione nell'intestazione HTTP impostando il campo `X-Global-Transaction-Id`. Questo ID di transazione viene memorizzato nella tabella payload. Per trovare una spiegazione del funzionamento del modello per un particolare calcolo del punteggio, specificare l'ID transazione associato alla richiesta di calcolo del punteggio. Si noti che questo comportamento si applica solo alle transazioni {{site.data.keyword.pm_full}} e non è applicabile alle transazioni non WML.
{: note}

## Ricerca di un ID transazione in {{site.data.keyword.aios_short}}
{: #ie-find}

1.  Dal grafico temporale per la propria distribuzione, scorrere il puntatore nel grafico e fare clic sul link **Visualizza dettagli** per [visualizzare i dati per un'ora specifica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Fare clic sul pulsante **Visualizza transazioni** per [visualizzare l'elenco di ID transazione](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copiare uno degli ID transazione dall'elenco, incollarlo nella casella di ricerca sulla pagina **Spiega una transazione** e premere Invio.

    L'elenco di ID transazione offre anche la possibilità di fare semplicemente clic sul link **Spiega** nella colonna Azione per qualsiasi ID di transazione, ciò aprirà quella transazione nella scheda Esplicabilità.
    {: note}

  Consultare le seguenti sezioni per esempi di spiegazioni per diversi tipi di modelli.

  ![Esplicabilità - ID transazione](images/insight-explain-trans-id.png)

## Ricerca di spiegazioni attraverso i dettagli del grafico
{: #ie-view-ui}

Poiché esistono spiegazioni per le metriche di correttezza e deviazione, è possibile fare clic sui grafici per ottenere una vista dettagliata del dataset e quindi fare clic sul pulsante **Visualizza transazioni** per le metriche di correttezza o fare clic su un riquadro di transazione di deviazione per visualizzare le spiegazioni delle transazioni.

- Per uno degli attributi di correttezza, come il sesso o l'età, fare clic sull'attributo, quindi sul grafico e quindi sul pulsante **Visualizza transazioni**.
- Per il monitor di deviazione, fare clic su **Entità deviazione**, fare clic sul grafico, quindi fare clic su un riquadro per visualizzare le transazioni associate a quel particolare gruppo di deviazione.

## Passi successivi
{: #ie-trans-id-next}

- [Spiegazione di modelli categoriali](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Spiegazione di modelli immagine](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Spiegazione di modelli di testo non strutturato](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Spiegazioni contrastanti](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
