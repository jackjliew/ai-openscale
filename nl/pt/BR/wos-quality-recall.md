---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds

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

# Rechamada
{: #quality_recall}

A Rechamada fornece a proporção de predições corretas em classe positiva.
{: shortdesc}

## Visão rápida da Rechamada
{: #quality_recall-glance}

- **Descrição**: proporção de predições corretas na classe positiva
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: matriz de confusão

## Interpretando a exibição da métrica de rechamada
{: #quality_recall-display}

![o gráfico de Rechamada é exibido.](images/quality-recall.png)

### Pontuação de justiça
{: #quality_recall-display-fairness-score}

Para a métrica de rechamada, a pontuação de justiça a seguir é exibida. 

![a porcentagem da pontuação de rechamada é exibida.](images/wos-quality-recall-score.png)

### Planejamento
{: #quality_recall-display-schedule}

A área de janela **Planejamento** mostra os horários da **Última avaliação** e da **Próxima avaliação**. As métricas de qualidade são avaliadas a cada hora. É possível forçar a avaliação clicando em **Verificar qualidade agora**. Também é possível incluir feedback clicando em **Incluir dados de feedback**.

![a área de janela Planejamento é exibida, que mostra os horários da última e da próxima avaliação](images/wos-quality-schedule.png)


### Recomendação
{: #quality_recall-display-recommendations}

Para ajudá-lo a interpretar o gráfico, a área de janela **Recomendação** exibe quais tendências indicam a melhoria ou o comprometimento da eficácia do modelo.

![a área de janela Recomendação é exibida.](images/wos-quality-positive-recommendation.png)




## Fazer os cálculos
{: #quality_recall-math}

A rechamada (R) é definida como o número de positivos verdadeiros (Tp) sobre o número de positivos verdadeiros mais o número de falsos negativos (Fn).

```
                       número de positivos verdadeiros Rechamada = ______________________________________________________

           (número de positivos verdadeiros + número de falsos negativos)
```
