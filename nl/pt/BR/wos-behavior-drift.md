---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: drift, behavior, metrics

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

# Magnitude de desvio ![beta tag](images/beta.png)
{: #behavior-drift-ovr}

Ao longo do tempo, a importância e o impacto de determinados recursos em um modelo mudam. Isso afeta os aplicativos associados e os resultados dos negócios. Por meio da detecção de desvio, o {{site.data.keyword.aios_short}} fornece uma maneira de rastrear as métricas do modelo, o desempenho do modelo e a maneira com que os pesos do recurso mudam ao longo do tempo. À medida que os dados mudam, a capacidade do seu modelo de fazer predições precisas pode ser prejudicada. A magnitude de desvio é a extensão da degradação do desempenho preditivo ao longo do tempo. Use as informações sobre o desvio para tomar uma ação corretiva.
{: shortdesc}

## Entendendo a detecção de desvio
{: #behavior-drift-understand}

Desvio é a degradação do desempenho preditivo ao longo do tempo devido ao contexto oculto. À medida que seus dados mudam com o tempo, a capacidade do seu modelo de fazer previsões precisas pode ser prejudicada. O {{site.data.keyword.aios_short}} detecta e destaca o desvio para que seja possível tomar uma ação corretiva.

### Como ele funciona
{: #behavior-drift-works}

O {{site.data.keyword.aios_short}} analisa todas as transações para localizar aquelas que contribuem para o desvio. Em seguida, ele agrupa os registros com base nos valores de atributos que eram significativos na contribuição para o desvio.

### Fazer os cálculos
{: #behavior-drift-math}

A cada três horas, o {{site.data.keyword.aios_short}} calcula o desvio analisando os mesmos dados de treinamento que já foram analisados por seu modelo preditivo. Em seguida, ele compara os resultados com as predições do modelo. Onde houver mudanças ou discrepâncias, o {{site.data.keyword.aios_short}} calculará a extensão do desvio e, com base no limite configurado, alertará para a ocorrência. 


### Visualização de desvio
{: #behavior-drift-display}

A visualização de desvio inclui dados estatísticos gráficos e numéricos:

![gráfico de métricas de justiça mostrando o desvio inferior ao limite configurado](images/drift-example.png)

Ao clicar no gráfico, é possível exibir transações específicas que contribuem para o desvio. As principais razões para o desvio detectado são exibidas e inclui uma descrição de língua natural da observação, bem como uma lista de valores inesperados.

![gráfico de métricas de justiça mostrando o desvio inferior ao limite configurado](images/drift-detection-example.png)

Transações de desvio estão disponíveis na tela de detalhes da transação, na qual é possível clicar em **Explicar** para entender como uma transação específica entrou na categoria de desvio:

![gráfico de métricas de justiça mostrando o desvio inferior ao limite configurado](images/drift-detection-transactions.png)


## Próximos passos

- Para obter informações sobre como configurar a detecção de desvio, consulte [Configurando o monitor de detecção de desvio](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-config).
- Para minimizar o desvio, depois de ele ter sido detectado pelo Watson OpenScale, deve-se criar uma nova versão do modelo que corrija o problema. Um bom lugar para começar são os pontos de dados destacados como motivos para o desvio. Introduza os novos dados no modelo preditivo depois de rotular manualmente as transações com desvio e usá-las para treinar novamente o modelo.


