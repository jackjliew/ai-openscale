---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: metrics, monitoring, custom metrics, thresholds, Fairness for a group, sex, age, race

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

# Justiça para um grupo
{: #quality_group}

A métrica Justiça para um grupo fornece a propensão do modelo de entregar resultados favoráveis para um grupo em vez de para outro. Um grupo pode ser qualquer grupo, tal como idade, sexo ou raça.
{: shortdesc}


## Visão rápida da Justiça para um grupo
{: #quality_group-glance}

- **Descrição**: a propensão dos modelos para entregar resultados favoráveis para um grupo e não a outro.
- **Limites padrão**: limite inferior = 80%
- **Recomendação padrão**: nó de terminal de pontuação sem propensão que você pode usar em seu aplicativo de negócios para receber respostas sem propensão de seu modelo implementado.
- **Tipo de problema**: todos
- **Tipo de dados**: estruturado
- **Valores de gráfico**: último valor no prazo
- **Detalhes de métricas disponíveis**: sim

## Atributos protegidos
{: #quality_group-atts}

O {{site.data.keyword.aios_short}} identifica automaticamente se algum atributo protegido conhecido está presente em um modelo. Quando o {{site.data.keyword.aios_short}} detecta esses atributos, ele recomenda automaticamente a configuração de monitores de propensão para cada atributo presente, a fim de assegurar que a propensão com relação a esses atributos potencialmente sigilosos seja rastreada na produção. 

### sexo
{: #quality_group-sex}

O {{site.data.keyword.aios_short}} recomenda que, dentro do atributo **Sex**, o monitor de propensão seja configurado de forma que `Woman` e `Non-Binary` sejam os valores monitorados e `Male` seja o valor de referência. 

### etnia
{: #quality_group-ethnicity}

O {{site.data.keyword.aios_short}} recomenda que, dentro do atributo **ethnicity**, o monitor de propensão seja configurado de forma que `White-caucasian` seja o valor de referência, enquanto outras etnias sejam os valores monitorados.

### estado civil
{: #quality_group-marital}

O {{site.data.keyword.aios_short}} recomenda que, dentro do atributo **marital status**, o monitor de propensão seja configurado de forma que `married` seja o valor de referência e `single` seja o valor monitorado.

### idade
{: #quality_group-age}

O {{site.data.keyword.aios_short}} recomenda que, dentro do atributo **age**, o monitor de propensão seja configurado de forma que o intervalo de idades produza uma remoção de propensão acionável.

### CEP
{: #quality_group-zip}

O {{site.data.keyword.aios_short}} recomenda que, dentro do atributo **zip code**, o monitor de propensão seja configurado de forma que os CEPs individuais sejam pontuados.
