---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Perda logarítmica ![tag beta](images/beta.png)
{: #quality_log_loss}

A Perda logarítmica fornece a média das probabilidades da classe de destino dos logaritmos (confiança). Também é conhecida como probabilidade de log esperada e é uma medida efetiva de desempenho do modelo.
{: shortdesc}

## Visão rápida da Perda logarítmica
{: #quality_log_loss-glance}

- **Descrição**: média de probabilidades da classe de destino de logaritmos (confiança). Ela também é conhecida como log da verossimilhança esperada.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**:
   - **Tendência ascendente**: uma tendência ascendente indica que a métrica está melhorando. Isso significa que o novo treinamento dos modelos é efetivo.
   - **Tendência de queda**: uma tendência de queda indica que a métrica
está se deteriorando. Os dados de feedback estão se tornando significativamente diferentes dos dados de treinamento.
   - **Variação errática ou irregular**: uma variação errática ou irregular indica que os dados de feedback não são consistentes entre as avaliações. Aumente o tamanho mínimo da
amostra para o monitor de Qualidade.
- **Tipo de problema**: classificação binária e classificação multiclasse
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: nenhum

## Interpretando a exibição
{: #quality_log_loss-display}

![A Perda logarítmica é exibida](images/quality-log-loss.png)

## Faça as contas
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
