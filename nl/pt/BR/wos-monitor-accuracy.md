---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: accuracy, 

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

# Configurando o monitor Qualidade (Precisão)
{: #acc-monitor}

O monitor Qualidade (anteriormente conhecido como monitor Precisão) permite que você saiba quão bem seu modelo prevê resultados.
{: shortdesc}

## Etapas de configuração
{: #acc-config}

Na guia **Qualidade**, em **O que é o monitor Qualidade?**, clique em **Iniciar** para começar o processo de configuração.

![A página O que é o monitor Qualidade? é mostrada e explica que o monitor de qualidade avalia quão bem seu modelo prevê resultados precisos](images/wos-quality-what-is.png)

Defina as configurações a seguir nas páginas sucessivas da guia de configuração Precisão:

-  Configure o limite de alerta de precisão. Selecione um valor que represente um nível de precisão aceitável. Por exemplo, se estiver usando o **Modelo de risco de crédito alemão** para o tutorial interativo, configure o alerta como **90%**.

    A Precisão é um valor sintetizado de métricas relevantes de ciência de dados associadas a cada tipo de modelo específico. A pontuação é uma medida normalizada para permitir que você compare com facilidade a precisão em diferentes tipos de modelo. Em situações típicas, uma pontuação de precisão de 80 é suficiente. Para o tutorial, para gerar mais dados, recomendamos 90.
    {: note}

-  Configure os tamanhos de amostra mínimos e máximos. O tamanho mínimo impede a medição de Precisão até que um número mínimo de registros esteja disponível no conjunto de dados de avaliação; isso assegura que o tamanho da amostra não seja muito pequeno para distorcer os resultados. O tamanho máximo da amostra ajuda a gerenciar melhor o tempo e o esforço que leva para avaliar o conjunto de dados; somente os registros mais recentes serão avaliados se esse tamanho for excedido. Por exemplo, se estiver usando o **Modelo de risco de crédito alemão** para o tutorial interativo, configure o tamanho mínimo da amostra como **100** e o tamanho máximo da amostra como **10000**.


Um resumo de suas seleções é apresentado para revisão. Se você desejar mudar alguma coisa, clique no link **Editar** para essa seção. Caso contrário, clique em **Salvar** para concluir sua configuração.

### Próximos passos
{: #acc-next}

Para continuar configurando monitores, clique na guia **Justiça** e em **Começar**. Para obter mais informações, consulte [Configurando o monitor de justiça](/docs/services/ai-openscale?topic=ai-openscale-mf-monitor).
