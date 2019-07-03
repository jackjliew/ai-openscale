---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Área sob PR ![tag beta](images/beta.png)
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


## Faça as contas
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
