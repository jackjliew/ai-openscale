---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased, Logarithmic loss

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

# Perda logarítmica
{: #quality_log_loss}

A Perda logarítmica fornece a média das probabilidades da classe de destino dos logaritmos (confiança). Também é conhecida como probabilidade de log esperada e é uma medida efetiva de desempenho do modelo.
{: shortdesc}

## Visão rápida da Perda logarítmica
{: #quality_log_loss-glance}

- **Descrição**: média dos logaritmos das probabilidades de classe de destino (confiança). Ela também é conhecida como Log da verossimilhança esperada.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Tendência de queda**: uma tendência de queda indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária e classificação de várias classes
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Interpretando a exibição
{: #quality_log_loss-display}

![A Perda logarítmica é exibida](images/quality-log-loss.png)

### Pontuação de justiça
{: #quality_log_loss-display-fairness-score}

Para a métrica de perda logarítmica, a pontuação de justiça a seguir é exibida. 

![a porcentagem da pontuação de rechamada é exibida.](images/wos-quality-logloss-score.png)

### Planejamento
{: #quality_log_loss-display-schedule}

A área de janela **Planejamento** mostra os horários da **Última avaliação** e da **Próxima avaliação**. As métricas de qualidade são avaliadas a cada hora. É possível forçar a avaliação clicando em **Verificar qualidade agora**. Também é possível incluir feedback clicando em **Incluir dados de feedback**.

![a área de janela Planejamento é exibida, que mostra os horários da última e da próxima avaliação](images/wos-quality-schedule.png)


### Recomendação
{: #quality_log_loss-display-recommendations}

Para ajudá-lo a interpretar o gráfico, a área de janela **Recomendação** exibe quais tendências indicam a melhoria ou o comprometimento da eficácia do modelo.

![a área de janela Recomendação é exibida.](images/wos-quality-negative-recommendation.png)



## Fazer os cálculos
{: #quality_log_loss-math}

Para um modelo binário, a Perda logarítmica é calculada usando a fórmula a seguir:

```
-(y log(p) + (1-y)log(1-p))
```

em que p = rótulo verdadeiro e y = probabilidade predita

Para um modelo de várias classes, a Perda logarítmica é calculada usando a fórmula a seguir:

```
  M
-SUM Yo,c log(Po,c)
 c=1 
```

em que M > 2, p = rótulo verdadeiro e y = probabilidade predita
