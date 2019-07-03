---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: Amazon SageMaker, machine learning, services, AWS

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

# Especificando uma instância de serviço do Amazon SageMaker ML
{: #csm-connect}

Sua primeira etapa na ferramenta {{site.data.keyword.aios_short}} é especificar uma instância de serviço do Amazon SageMaker. Sua instância de serviço do Amazon SageMaker é onde você armazena seus modelos e implementações de IA.
{: shortdesc}

Também é possível incluir o seu provedor de aprendizado de máquina usando o Python SDK. Para obter mais informações sobre como executar isso programaticamente, consulte [Ligue o seu mecanismo de aprendizado de máquina do Amazon SageMaker](/docs/services/ai-openscale?topic=ai-openscale-cml-connect#cml-smbind).

## Conecte sua instância de serviço Amazon SageMaker
{: #csm-config}

O {{site.data.keyword.aios_short}} se conecta a modelos e implementações de IA em uma instância de serviço do Amazon SageMaker.

1.  Na página inicial da ferramenta {{site.data.keyword.aios_short}}, clique em **Iniciar**.

    ![Home page](images/gs-config-start.png)

1.  Selecione o ladrilho **Amazon SageMaker** e clique em **Avançar**.

    ![Select Amazon SageMaker service](images/connect-sage.png)

1.  Insira suas credenciais:

    - ID da chave de acesso: seu ID da chave de acesso da AWS, `aws_access_key_id`, que verifica quem você é, além de autenticar e autorizar chamadas feitas para a AWS.
    - Chave de acesso secreta: sua chave de acesso secreta da AWS, `aws_secret_access_key`, que é necessária para verificar quem você, além de para autenticar e autorizar chamadas feitas para a AWS.
    - Região: insira a região onde seu ID da chave de acesso foi criado. As chaves são armazenadas e usadas na região em que foram criadas e não podem ser transferidas para outra região. 

    ![Enter Amazon SageMaker service credentials](images/connect-sage-cred.png)

1.  Clique em **Avançar**.

1.  O {{site.data.keyword.aios_short}} listará seus modelos implementados; selecione os que você deseja monitorar

    ![Select Amazon SageMaker deployed models](images/connect-sage-deploys.png)

1.  Clique em **Avançar**.

### Próximos passos
{: #csm-next}

O {{site.data.keyword.aios_short}} agora está pronto para você [especificar um banco de dados](/docs/services/ai-openscale?topic=ai-openscale-connect-db).
