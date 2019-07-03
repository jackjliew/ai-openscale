---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: fairness, fairness monitor, payload, perturbation, training data, debiased

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

# Construtor de gráfico ![tag beta](images/beta.png)
{: #chart_builder}

Use o construtor de gráfico do {{site.data.keyword.aios_short}} para criar visualizações customizadas para que seja possível entender melhor predições do modelo e entradas no tempo de execução. O construtor de gráfico fornece a capacidade de visualizar a saída da predição do modelo com relação aos recursos ou aos intervalos de dados que um negócio considera importante. Ele ajuda a descobrir novas tendências nos dados que podem levar as equipes de negócios e de ciência de dados a considerarem mudanças no modelo de IA.
{: shortdesc}

Por exemplo, se você está familiarizado com nosso modelo de risco de crédito por meio dos tutoriais, pode ver a divisão em classes preditas para diferentes intervalos do atributo Credit History. 

   ![um gráfico que mostra o recurso predição para sexo pelo recurso idade](images/by_custom_chart.png)
      
   Também é possível ver o grau de confiança do modelo ao predizer esses intervalos do Credit History. É possível analisar a carga útil de pontuação que é enviada para sua implementação no intervalo de dados selecionado por gráfico customizado (selecionando entre recursos, classes de predição e confiança).


   ![um gráfico que mostra o recurso predição para sexo pelo recurso idade](images/by_custom_chart002.png)
   
