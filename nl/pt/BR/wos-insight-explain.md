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

# Explicando transações
{: #ie-ov}

Para cada implementação, é possível ver dados de explicabilidade para transações específicas. As transações aparecem apenas quando há dados para suportar os monitores e se baseiam nos limites definidos, no tempo planejado para a execução dos monitores e na disponibilidade de dados de carga útil do {{site.data.keyword.pm_full}}.
{: shortdesc}

## Visualizando explicações por ID de transação
{: #ie-view}

1. Clique em um bloco de implementação.
2. Clique na guia **Explicar uma transação** (![guia Explicar uma transação](images/insight-transact-tab.png)) do navegador.
3. Digite um ID de transação.

Sempre que os dados são enviados ao modelo para pontuação, ele define um ID de transação no cabeçalho de HTTP configurando o campo `X-Global-Transaction-Id`. Esse ID de transação é armazenado na tabela de carga útil. Para localizar uma explicação do comportamento do modelo para uma pontuação específica, especifique o ID de transação associado a essa solicitação de pontuação. Observe que esse comportamento se aplica somente a transações do {{site.data.keyword.pm_full}} e não é aplicável a transações não WML.
{: note}

## Localizando um ID de transação em {{site.data.keyword.aios_short}}
{: #ie-find}

1.  No gráfico de horário para sua implementação, deslize o marcador no gráfico e clique no link **Visualizar detalhes** para [visualizar dados para uma hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Clique no botão **Visualizar transações** para [visualizar a lista de IDs de transação](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copie um dos IDs de transação da lista, cole-o na caixa de procura na página **Explicar uma transação** e pressione Enter.

    A lista de IDs de transação também tem a opção de simplesmente clicar no link **Explicar** na coluna Ação para qualquer ID de transação, que abrirá essa transação na guia Explicabilidade.
    {: note}

  Consulte as seções a seguir para obter exemplos de explicações para diferentes tipos de modelos.

  ![ID de transação de explicabilidade](images/insight-explain-trans-id.png)

## Encontrando explicações através dos detalhes do gráfico
{: #ie-view-ui}

Como existem explicações para as métricas de justiça e desvio, é possível clicar nos gráficos para obter uma visão detalhada do conjunto de dados e, em seguida, clicar no botão **Visualizar transações** para obter as métricas de justiça ou clicar em um bloco de transação de desvio para ver as explicações da transação.

- Para um dos atributos de justiça, como sexo ou idade, clique no atributo, no gráfico e, em seguida, no botão **Visualizar transações**.
- Para o monitor de desvio, clique em **Magnitude de desvio**, no gráfico e, em seguida, em um bloco para ver as transações associadas a esse grupo de desvio específico.

## Próximos passos
{: #ie-trans-id-next}

- [Explicando modelos categóricos](/docs/services/ai-openscale?topic=ai-openscale-ie-class)
- [Explicando modelos de imagem](/docs/services/ai-openscale?topic=ai-openscale-ie-image)
- [Explicando modelos de texto não estruturado](/docs/services/ai-openscale?topic=ai-openscale-ie-unstruct)
- [Explicações contrastantes](/docs/services/ai-openscale?topic=ai-openscale-ie-pp-pn)
