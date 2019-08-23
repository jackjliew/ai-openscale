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

# Automatizando a criação de log de carga útil
{: #fmrk-workaround-pyld-lg}

A criação de log de carga útil automática existe entre o {{site.data.keyword.aios_full}} e o {{site.data.keyword.pm_full}} quando são provisionados na mesma conta do {{site.data.keyword.Bluemix_notm}}. Também é possível automatizar a criação de log de carga útil para outros provedores de aprendizado de máquina ou para uma instância do {{site.data.keyword.pm_full}} que não esteja na mesma conta usando um dos casos e opções a seguir:
{: shortdesc}

### Caso 1: manter o formato original de entrada e saída de pontuação (diferente daquele requerido pelo {{site.data.keyword.aios_short}})
{: #fmrk-workaround-case1}

Se seus aplicativos usarem um formato de carga útil original que não pode ser mudado, escolha uma das opções a seguir:

- Opção 1: o terminal de pontuação do mecanismo de aprendizado de máquina customizado deve aceitar os dois formatos de carga útil. 

   Dependendo do formato de carga útil: {{site.data.keyword.aios_short}} (como {{site.data.keyword.pm_full}}) ou um do usuário retornam a saída no formato correspondente. Se o formato for um do usuário, converta-o em um do {{site.data.keyword.aios_short}} e armazene como registro de carga útil na tabela de criação de log de carga útil. Se o formato de entrada de pontuação for um do {{site.data.keyword.aios_short}}, não armazene a carga útil (essa carga útil está vindo do {{site.data.keyword.aios_short}}, não do usuário).

   Para obter mais informações, consulte [Usando dois formatos de carga útil](#fmrk-workaround-notsuppt).

- Opção 2: se, por alguma razão, a integração dessa lógica em um único terminal da API de REST não for possível, será possível definir dois terminais. 

   Um é usado por seu aplicativo, no entanto, deve-se incluir a criação de log de carga útil e convertê-la no formato esperado. O segundo terminal é usado pelo {{site.data.keyword.aios_short}} para fazer cálculos necessários, como propensão e explicabilidade. Nenhuma criação de log de carga útil é necessária para esse terminal. Durante a configuração do {{site.data.keyword.aios_short}}, o segundo terminal deve ser apontado para um com formatos compatíveis.

   Para obter mais informações, consulte [Usando dois terminais](#fmrk-workaround-opt2-cs1).

- Opção 3: mova o módulo de criação de log de carga útil para o terminal original ou aplicativo de recebimento de dados. 

   Se o seu aplicativo suportar essa opção, somente um terminal no mecanismo de aprendizado de máquina customizado precisará ser desenvolvido: aquele para o {{site.data.keyword.aios_short}}.

### Caso 2: trabalhar com o formato de carga útil requerido pelo {{site.data.keyword.aios_short}}
{: #fmrk-workaround-case2}

Nesse caso, não há necessidade de fazer nenhuma conversão do formato do usuário (entrada/saída de pontuação) para aquele requerido pelo {{site.data.keyword.aios_short}}.

Como não desejamos que as solicitações de pontuação interna sejam registradas como carga útil do usuário (cálculos feitos pelo {{site.data.keyword.aios_short}}), deve-se desenvolver dois terminais ou codificar a lógica extra para um único terminal.

- Opção 1: dois terminais. É quase o mesmo que a opção 2 no Caso 1. A única diferença é que não há necessidade de fazer nenhuma conversão de formato, pois elas já estão alinhadas.

- Opção 2: terminal único. Há uma necessidade de detectar se a solicitação de pontuação está vindo do aplicativo do usuário. Isso pode ser alcançado enviando algumas informações extras na carga útil de pontuação (conhecido como metadados). Se esses metadados forem detectados, a carga útil deverá ser registrada.

## Usando dois formatos de carga útil
{: #fmrk-workaround-notsuppt}

Vamos supor que eu esteja usando a oferta XYZ para entregar meus modelos. XYZ não é suportado pelo {{site.data.keyword.aios_short}} neste estágio.

Tenho muitos aplicativos de recebimento de dados que consomem minhas implementações em XYZ e não posso mudar o formato de carga útil de pontuação. No entanto, eu posso modificar a lógica do terminal de pontuação.

### Etapas

1. Desenvolva um mecanismo de aprendizado de máquina customizado que agrupe a implementação XYZ.
2. Implemente o terminal de pontuação no mecanismo de aprendizado de máquina customizado para suportar os formatos de carga útil para ambos, XYZ e {{site.data.keyword.aios_short}}.
3. Inclua a lógica no terminal de pontuação em seu mecanismo de aprendizado de máquina customizado para detectar o formato da carga útil.
4. Se a carga útil estiver vindo de apps de recebimento de dados, converta-a no formato do {{site.data.keyword.aios_short}} e registre-a como registros de carga útil no {{site.data.keyword.aios_short}}.
5. Alterne os terminais de pontuação de apps de recebimento de dados para o novo que você criou.

Se a URL do terminal de pontuação precisar permanecer a mesma, use o redirecionamento de URL, que também é conhecido como um proxy.

## Usando dois terminais
{: #fmrk-workaround-opt2-cs1}

Se o formato de sua carga útil não pode ser mudado, por exemplo, se ele faz com que seus aplicativos de recebimento de dados falhem, deve-se usar terminais separados. Essa abordagem consiste nos componentes a seguir:

- terminal de pontuação (no formato do usuário) com o terminal de pontuação original usando o formato definido pelo usuário para entrada e saída
- mecanismo de ml customizado com terminal de perturbação (formato do {{site.data.keyword.aios_short}}) e terminal de descoberta. O terminal de perturbação agrupa o terminal de pontuação original e faz conversões do formato do {{site.data.keyword.aios_short}} para um do usuário e da saída do usuário para um do {{site.data.keyword.aios_short}}. Isso é necessário para o {{site.data.keyword.aios_short}} fazer uma solicitação de pontuação correta e entender a saída.
- wrapper de terminal de pontuação com recurso de criação de log de carga útil. Esse wrapper é consumido pelo aplicativo de recebimento de dados em vez do terminal de pontuação original. Sua lógica foi ampliada com o recurso de criação de log de carga útil. Cada vez que a solicitação de pontuação é executada, a entrada e a saída estão sendo convertidas para o formato do {{site.data.keyword.aios_short}} e registradas.

O fluxograma a seguir mostra a solução do mecanismo de aprendizado de máquina customizado na qual o mecanismo de aprendizado da máquina customizado manipula os terminais de perturbação e descoberta e os converte em seu formato:

![Especificação de terminais da API de REST](images/woscustommlworkflow.png)

### Etapas
{: #fmrk-workaround-smple-cd}

1. Use um bloco de notas para criar um terminal de pontuação para a implementação do modelo de risco de crédito (scikit-learn) no Microsoft Azure Machine Learning Service. Para obter mais informações, consulte [este bloco de notas de amostra](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20model%20with%20Azure%20ML%20Service%20and%20scikit-learn.ipynb).
2. Crie um mecanismo de aprendizado de máquina customizado e implemente-o no Microsoft Azure Cloud como um aplicativo Flask. Crie os terminais de perturbação e de descoberta. Para obter mais informações, consulte [estas instruções de implementação](https://github.com/pmservice/ai-openscale-tutorials/tree/master/applications/custom-ml-engine-azure).
3. Configure o {{site.data.keyword.aios_short}} para trabalhar com o mecanismo de aprendizado de máquina customizado. Para obter mais informações, consulte  [este bloco de notas de amostra](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/OpenScale%20and%20Custom%20ML%20Engine%20configuration.ipynb).
4. Crie um wrapper de terminal de pontuação que automatize a criação de log de carga útil no Microsoft Azure Machine Learning Service. Para obter mais informações, consulte [este bloco de notas de amostra](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/azure/Credit%20scoring%20endpoint%20wrapper%20with%20payload%20logging.ipynb).

Preste atenção especial nos itens a seguir:

- Credenciais: para tornar o tutorial mais fácil de ser seguido, as credenciais do {{site.data.keyword.aios_short}} são codificadas permanentemente dentro do código (wrapper de terminal de pontuação). Deve-se atualizar esses valores para suas credenciais reais.
- SDK do Python vs. API de REST: o tutorial usa o SDK do Python para registrar a carga útil. Também seria possível usar a API de REST para fazer isso, no entanto, deve-se gerar ou atualizar o token por conta própria. 
- {{site.data.keyword.cloud_notm}} vs. Cloud Pak for Data: se você estiver usando o {{site.data.keyword.wos4d_notm}}, as credenciais estarão em um formato diferente [aqui está o bloco de notas de amostra](https://github.com/pmservice/ai-openscale-tutorials/blob/master/notebooks/Watson%20OpenScale%20and%20Watson%20ML%20Engine%20-%20ICP.ipynb). A classe de cliente {{site.data.keyword.aios_short}} também é diferente. Ele usa a classe de cliente `APIClient4ICP`.
- Criação de log de carga útil como terminal/pacote separado — extração de criação de log de carga útil e métodos de conversão para pacote ou terminal separado. Dessa forma, ela poderá ser reutilizada se você desejar injetar lote de cargas úteis fora do wrapper de terminal de pontuação.

