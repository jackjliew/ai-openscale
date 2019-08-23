---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: machine learning engines, frameworks, Microsoft Azure, Amazone SageMaker, custom ML engine 

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

# Mecanismo de aprendizado de máquina customizado
{: #fmrk-workaround-customengine}

Um mecanismo de aprendizado de máquina customizado fornece os recursos de infraestrutura e de hosting para modelos de aprendizado de máquina e aplicativos da web. Os mecanismos de aprendizado de máquina customizados que são suportados pelo {{site.data.keyword.aios_short}} devem se adequar aos requisitos a seguir:

- Exponha dois tipos de terminais da API de REST:

   * terminal de descoberta (lista de implementações e detalhes de GET)
   * terminais de pontuação (pontuação on-line e em tempo real)

- Todos os terminais precisam ser compatíveis com a especificação swagger a ser suportada.

- A carga útil de entrada e a saída para a implementação ou da implementação devem ser compatíveis com o formato de arquivo JSON que está descrito na especificação.

Neste estágio, somente os formatos `BasicAuth` ou `none` são suportados
{: Note}

O exemplo a seguir mostra a especificação de terminais da API de REST:

![A especificação de terminais da API de REST é exibida por meio do documento do swagger](images/wosdeployments.png)


O exemplo a seguir mostra o formato para uma carga útil de entrada:

![O exemplo de carga útil de entrada é mostrado](images/wosinputdata.png)


## Quando um mecanismo de aprendizado de máquina customizado é a melhor opção para mim?
{: #fmrk-workaround-enging-choice}

Um mecanismo de aprendizado de máquina customizado é a melhor opção quando as situações a seguir são verdadeiras:

- Você não está usando nenhum produto pronto para utilização para atender a seus modelos de aprendizado de máquina. Você acabou de desenvolver seu próprio sistema para fazer isso. Não há e não haverá nenhum suporte direto no {{site.data.keyword.aios_short}} para isso.
- O mecanismo de entrega que você está usando por meio de um fornecedor de terceiros ainda não é suportado pelo {{site.data.keyword.aios_short}}. Nesse caso, considere o desenvolvimento de um mecanismo de aprendizado de máquina customizado como um wrapper para suas implementações originais ou nativas.

## Próximos passos
{: #fmrk-workaround-nxt-steps-over}

Implemente sua própria solução usando um destes [Exemplos de aprendizado de máquina customizado](/docs/services/ai-openscale?topic=ai-openscale-fmrk-workaround-cstmmlsengex).
