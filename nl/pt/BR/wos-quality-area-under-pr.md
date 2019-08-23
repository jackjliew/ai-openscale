---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: metrics, monitoring, custom metrics, thresholds, Area under PR

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

# Área sob PR
{: #quality-area-pr}

A Área sob Rechamada de precisão fornece a área sob a curva de precisão e rechamada, que pode ser útil quando as classes são particularmente desequilibradas.
{: shortdesc}

## Visão rápida da Área sob PR
{: #quality-area-pr-glance}

- **Descrição**: área sob a curva de precisão e rechamada
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

## Interpretando a exibição
{: #quality-area-pr-display}

![A Área sob PR é mostrada com tendência de métrica descendente](images/quality-area-under-pr.png)

### Pontuação de justiça
{: #quality-area-pr-display-fairness-score}

Para a métrica Área sob PR, a pontuação de justiça a seguir é exibida. 

![a porcentagem de pontuação da Área sob PR é exibida.](images/wos-quality-area-pr-score.png)

### Planejamento
{: #quality-area-pr-display-schedule}

A área de janela **Planejamento** mostra os horários da **Última avaliação** e da **Próxima avaliação**. As métricas de qualidade são avaliadas a cada hora. É possível forçar a avaliação clicando em **Verificar qualidade agora**. Também é possível incluir feedback clicando em **Incluir dados de feedback**.

![a área de janela Planejamento é exibida, que mostra os horários da última e da próxima avaliação](images/wos-quality-schedule.png)


### Recomendação
{: #quality-area-pr-display-recommendations}

Para ajudá-lo a interpretar o gráfico, a área de janela **Recomendação** exibe quais tendências indicam a melhoria ou o comprometimento da eficácia do modelo.

![a área de janela Recomendação é exibida.](images/wos-quality-positive-recommendation.png)




## Fazer os cálculos
{: #quality-area-pr-math}

A Área sob Rechamada de precisão fornece o total para `Precision + Recall`.

A precisão (P) é definida como o número de positivos verdadeiros (Tp) sobre o número de positivos verdadeiros mais o número de falsos positivos (Fp).

```
               número de positivos verdadeiros
Precisão =   ______________________________________________________

              (número de positivos verdadeiros + número de falsos positivos)
```

A rechamada (R) é definida como o número de positivos verdadeiros (Tp) sobre o número de positivos verdadeiros mais o número de falsos negativos (Fn).

```
            número de positivos verdadeiros Rechamada = ______________________________________________________

           (número de positivos verdadeiros + número de falsos negativos)
```
