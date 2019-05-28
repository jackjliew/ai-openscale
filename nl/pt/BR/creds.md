---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-29"

keywords: credentials, REST API

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Criando credenciais
{: #cred-create}

Para acessar as APIs de REST do {{site.data.keyword.aios_short}}, uma chave de API da Plataforma e o ID do data mart (instância de serviço) são necessários. A chave de API da Plataforma fornece a um usuário individual a capacidade de acessar recursos no {{site.data.keyword.cloud_notm}}.

Para contas corporativas, um administrador pode criar o data mart e, em seguida, convidar outros usuários para a conta, concedendo a esses usuários acesso a um data mart específico do {{site.data.keyword.aios_short}}. Um usuário pode criar sua própria chave de API da Plataforma e acessar o mesmo data mart do {{site.data.keyword.aios_short}}; não há risco de segurança ou conflito.

Para criar uma chave de API da Plataforma, conclua as etapas a seguir:

- Efetue login no [{{site.data.keyword.cloud_notm}} ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://{DomainName}){: new_window}.

- Selecione **Gerenciar** --> **Segurança** --> **Chaves de API da Plataforma**

    ![Chaves de API da Plataforma](images/cred-api-key.png)

- Crie e salve uma chave de API da Plataforma.

Para localizar seu ID do data mart (ou instância de serviço):

- Na página {{site.data.keyword.aios_short}} **Configuração --> Resumo**, a primeira entrada é seu ID de Data Mart (instância de serviço).

    ![ID do Data Mart](images/data-mart-id.png)
