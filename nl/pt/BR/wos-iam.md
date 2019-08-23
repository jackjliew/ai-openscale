---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"


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

Com as funções de gerenciamento de plataforma, os usuários podem receber níveis variados de permissão para executar ações de plataforma dentro da conta e em um serviço. Por exemplo, as funções de gerenciamento
da plataforma que são designadas para os recursos do catálogo permitem que os usuários concluam ações como, criar,
excluir, editar e visualizar instâncias de serviço. Além disso, as funções de gerenciamento da plataforma que são
designadas para os serviços de gerenciamento de conta permitem que os usuários concluam ações como, convidar e remover
usuários, trabalhar com grupos de recursos e visualizar as informações de faturamento. Para obter mais informações sobre os serviços de gerenciamento de conta, consulte [Designando acesso aos serviços de gerenciamento de conta](/docs/iam?topic=iam-account-services#account-services){: external}.

Selecione todas as funções que se aplicam ao criar uma política. Cada função permite que ações separadas sejam concluídas e não herdam as ações das funções menores.
{: tip}

A tabela a seguir fornece exemplos de algumas das ações de gerenciamento de plataforma que os usuários podem executar no contexto dos recursos de catálogo e dos grupos de recursos. Consulte a documentação para cada oferta de catálogo para entender como as funções se aplicam aos usuários dentro do contexto do serviço que está sendo usado.


|  | Um ou todos os serviços ativados por IAM | Serviço selecionado em um grupo de recursos | Grupo de recursos selecionados |
|:--------------|:------------|:-------------|:-------------|
| Função de visualizador | Visualizar instâncias, aliases, ligações e credenciais | Visualizar somente instâncias especificadas no grupo de recursos | Visualizar grupo de recursos |
| Função de operador |  Visualizar instâncias e gerenciar aliases, ligações e credenciais |  Não aplicável | Não aplicável |
| Função de editor |  Criar, excluir, editar e visualizar instâncias. Gerenciar aliases, ligações e credenciais | Criar, excluir, editar, suspender, continuar, visualizar e ligar somente as instâncias especificadas no grupo de recursos | Visualizar e editar o nome do grupo de recursos |
| Função de administrador |  Todas as ações de gerenciamento para serviços | Todas as ações de gerenciamento para as instâncias especificadas no grupo de recursos | Visualizar, editar e gerenciar o acesso para o grupo de recursos |
| Função de administrador de cluster (específica somente para o {{site.data.keyword.wos4d_full}}) |  Tem acesso completo à plataforma IBM Cloud Private | Tem acesso completo às instâncias especificadas no grupo de recursos | As ações a seguir podem ser concluídas apenas pelo administrador de cluster: conectar a um diretório LDAP, incluir usuários e designar a eles as funções do IAM, gerenciar cargas de trabalho, infraestrutura e aplicativos em todos os namespaces, criar namespaces, designar cotas, incluir políticas de segurança de pod, incluir um repositório interno do Helm, excluir um repositório interno do Helm, incluir gráficos do Helm no repositório interno do Helm, remover gráficos do Helm do repositório interno do Helm e sincronizar os repositórios do Helm internos e externos |
{: row-headers}
{: class="comparison-table"}
{: caption="Tabela 1. Exemplo de funções de gerenciamento de plataforma e ações para serviços em uma conta" caption-side="top"}
{: summary="The first row of the table describes separate options that you can choose from when creating a policy, and the first column describes the selected roles for the policy. The remaining cells map to which role is selected from the first column, and which type of policy has been selected from the options in the first row."}
{: #platformrolestable1}


Para as funções de acesso de serviço, que permitem que os usuários acessem o {{site.data.keyword.aios_short}}, bem como a capacidade de chamar a API de REST, o {{site.data.keyword.aios_short}} difere para as funções de gerenciamento de plataforma listadas na tabela anterior. Para obter informações sobre como designar funções de usuário na IU, consulte [Gerenciando o acesso a recursos](/docs/iam?topic=iam-iammanidaccser#iammanidaccser){: external}.

 
