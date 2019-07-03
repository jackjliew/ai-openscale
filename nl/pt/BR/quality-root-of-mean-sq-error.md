---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Raiz do erro quadrático médio ![tag beta](images/beta.png)
{: #supqualdets_squ_errors_mean}

A visualização Raiz do erro quadrático médio (RMSE) mostra a diferença entre os valores preditos e observados em seu modelo.
{: shortdesc}

## Visão rápida da Raiz do erro quadrático médio
{: #anlz_metrics_supqualdets_squ_errors_mean}

- **Descrição**: raiz quadrada da média da diferença quadrática entre a predição do modelo e o valor de destino
- **Limites padrão**: limite superior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Tendência de queda**: uma tendência de queda indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Variação errática ou irregular**: uma variação errática ou irregular
indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: regressão
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Interpretando a exibição
{: #supqualdets_squ_errors_mean-display}

![o gráfico de Raiz do erro quadrático médio é exibido.](images/xxxx.png)

## Faça as contas
{: #supqualdets_squ_errors_mean-math}

A Raiz do erro quadrático médio é igual à Raiz quadrada da média de (previsões menos valores observados) ao quadrado.

```
          ___________________________________________________________
RMSE  =  √(previsões - valores observados)*(previsões - valores observados)
```
