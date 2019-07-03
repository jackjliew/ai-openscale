---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: identity and access management, authentication

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
{:table: .aria-labeledby="caption"}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:faq: data-hd-content-type='faq'}

# {{site.data.keyword.aios_short}} Identity and Access Management 
{: #iam-docs-template}

## Funções e ações do Identity and Access Management

O acesso às instâncias de serviço do {{site.data.keyword.aios_full}} para usuários em sua conta é controlado pelo {{site.data.keyword.Bluemix_notm}} Identity and Access Management (IAM). Deve-se designar uma política de acesso com uma função definida do IAM a cada usuário que acessa o serviço {{site.data.keyword.aios_short}} em sua conta. A política determina quais ações um usuário pode executar dentro do contexto do serviço ou da instância selecionada. As ações permitidas são customizadas e definidas pelo serviço {{site.data.keyword.Bluemix_notm}} como operações que têm permissão para execução no serviço. As ações são, então, mapeadas para funções de usuário do IAM.

As políticas permitem que o acesso seja concedido em níveis diferentes. Algumas das opções incluem o seguinte: 

* Acesso em todas as instâncias do serviço em sua conta
* Acesso a uma instância de serviço individual em sua conta
* Acesso a um recurso específico dentro de uma instância

Depois de definir o escopo da política de acesso, você designa uma função que determina o nível de acesso do usuário. Revise as tabelas a seguir que descrevem quais ações cada função permite no serviço {{site.data.keyword.aios_short}}.

A tabela a seguir detalha as ações que são mapeadas para funções de gerenciamento de plataforma. As funções de gerenciamento de plataforma permitem que os usuários executem tarefas em recursos de serviço no nível da plataforma, por exemplo, designar acesso de usuário ao serviço, criar ou excluir instâncias e ligar instâncias aos aplicativos.

| Função de gerenciamento da plataforma | Descrição de ações | Ações de exemplo                                                 |
|--------------------------|------------------------|-----------------------------------------------------------------|
| Visualizador             | Descrição            | <ul><li>Exemplo 1</li><li>Exemplo 2</li></ul>                   |
| Editor                   | Descrição            |<ul><li>Exemplo 1</li><li>Exemplo 2</li></ul>                    |
| Operador                 | Descrição            | <ul><li>Exemplo 1</li><li>Exemplo 2</li><li>Exemplo 3</li></ul> |
| Administrador            | Descrição            |<ul><li>Exemplo 1</li><li>Exemplo 2</li><li>Exemplo 3</li></ul>  |
{: caption="Tabela 1. Funções e ações do usuário do IAM" caption-side="top"}


A tabela a seguir detalha as ações que são mapeadas para funções de acesso de serviço. As funções de acesso de serviço permitem que os usuários acessem o {{site.data.keyword.aios_short}}, bem como a capacidade de chamar a API do {{site.data.keyword.aios_short}}.

| Função de acesso de serviço | Descrição de ações | Ações de exemplo                                                 |
|---------------------|------------------------|-----------------------------------------------------------------|
| Leitor              | Descrição            | <ul><li>Exemplo 1</li><li>Exemplo 2</li></ul>                   |
| Transcritor         | Descrição            |<ul><li>Exemplo 1</li><li>Exemplo 2</li></ul>                    |
| Gerenciador         | Descrição            | <ul><li>Exemplo 1</li><li>Exemplo 2</li><li>Exemplo 3</li></ul> |
{: caption="Tabela 2. Funções e ações de acesso de serviço do IAM" caption-side="top"}


Para obter informações sobre como designar funções de usuário na IU, consulte [Gerenciando o acesso a recursos](/docs/iam?topic=iam-iammanidaccser#iammanidaccser).

<!-- You can add an extra column to each table if you want to provide the specific action name in dot notation as it is used in the service's registration with IAM. For example: key-protect.keys.create, key-protect.keys.delete) -->
 
