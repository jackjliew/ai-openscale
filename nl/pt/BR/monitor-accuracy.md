---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

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

# Configurando o monitor de Precisão ou Qualidade
{: #acc-monitor}

O monitor de Qualidade (anteriormente conhecido como monitor de Precisão) permite que você saiba com que eficiência seu modelo prediz resultados.
{: shortdesc}

## Etapas de configuração
{: #acc-config}

Na guia **Precisão**, na página **O que é Precisão?**, clique em **Iniciar** para começar o processo de configuração.

![O Que É Precisão? página](images/accuracy-what-is.png)

Defina as configurações a seguir nas páginas sucessivas da guia de configuração Precisão:

-  Configure o limite de alerta de precisão. Selecione um valor que represente um nível de precisão aceitável.

    A Precisão é um valor sintetizado de métricas relevantes de ciência de dados associadas a cada tipo de modelo específico. A pontuação é uma medida normalizada para permitir que você compare com facilidade a precisão em diferentes tipos de modelo. Em situações típicas, uma pontuação de precisão de 80 é suficiente.
    {: note}

-  Configure os tamanhos de amostra mínimos e máximos. O tamanho mínimo impede a medição de Precisão até que um número mínimo de registros esteja disponível no conjunto de dados de avaliação; isso assegura que o tamanho da amostra não seja muito pequeno para distorcer os resultados. O tamanho máximo da amostra ajuda a gerenciar melhor o tempo e o esforço que leva para avaliar o conjunto de dados; somente os registros mais recentes serão avaliados se esse tamanho for excedido.


Um resumo de suas seleções é apresentado para revisão. Se você desejar mudar alguma coisa, clique no link **Editar** para essa seção. Caso contrário, clique em **Salvar** para concluir sua configuração.

### Próximos passos
{: #acc-next}

Na página **Configurar monitores**, é possível selecionar outra categoria de monitoramento.
