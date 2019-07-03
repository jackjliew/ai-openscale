---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: databases, connections, scoring, requests

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

# Especificando um Banco de Dados
{: #connect-db}

Especifique um banco de dados para ser usado por sua instância do {{site.data.keyword.aios_short}}.
{: shortdesc}

## Conectando-se ao seu banco de dados
{: #cdb-connect}

O {{site.data.keyword.aios_short}} usa um banco de dados para armazenar dados de carga útil, feedback e medição. Além de selecionar um banco de dados, você também pode selecionar um esquema para seu banco de dados - um esquema é uma coleção nomeada de tabelas no banco de dados.

1.  Escolha um banco de dados. Você tem duas opções: o banco de dados grátis ou um banco de dados existente ou novo.

    ![Select database](images/gs-config-database.png)

    Se você tiver uma conta paga do {{site.data.keyword.cloud_notm}}, poderá provisionar um serviço `Databases for PostgreSQL` ou `Db2 Warehouse` para tirar total proveito da integração com o Watson Studio e serviços de aprendizado contínuo. Se você escolher não provisionar um serviço pago, será possível usar o armazenamento PostgreSQL interno grátis com o {{site.data.keyword.aios_short}}, mas não será possível configurar o aprendizado contínuo para seu modelo.
    {: note}

### Banco de dados de plano Lite livre
{: #cdb-lite}

**NOTA**: O banco de dados grátis possui algumas limitações importantes:

- O banco de dados grátis é hospedado e você não pode acessá-lo diretamente.
- O {{site.data.keyword.aios_full}} terá acesso total a seu banco de dados e, assim, terá acesso total a seus dados.
- O banco de dados grátis não está em conformidade com o GDPR. Se o seu modelo processar informações pessoalmente identificáveis (PII), não será possível usar o banco de dados grátis. Deve-se comprar um novo banco de dados ou usar um banco de dados existente que se adéque às regras do GDPR. Consulte [Segurança da informação](/docs/services/ai-openscale?topic=ai-openscale-is-ov) para saber mais.

Para continuar usando o banco de dados grátis, clique no tile **Usar o banco de dados grátis hospedado pelo {{site.data.keyword.aios_short}}**, em seguida, revise os dados de resumo
e clique em **Salvar**.

  ![Select database](images/gs-config-database2.png)
  
É possível fazer upgrade para outro banco de dados do banco de dados grátis, no entanto, não é possível reconfigurar uma instância do Compose for Postgres, do Database for Postgres ou do Db2 para o banco de dados grátis. Depois de fazer upgrade, será impossível retornar ao uso do banco de dados grátis. Todos
os dados atuais, tais como a configuração, os resultados da pontuação e as explicações não podem ser
reutilizados. Ao selecionar outro esquema ou banco de dados, o ambiente do {{site.data.keyword.aios_short}}
é completamente reconfigurado.



### Banco de Dados Existente ou Novo
{: #cdb-exn}

1.  Após selecionar a opção "Usar banco de dados existente ou comprar um novo", o {{site.data.keyword.aios_short}} verifica sua conta do {{site.data.keyword.Bluemix_notm}} para localizar quaisquer bancos de dados existentes.

1.  Selecione seu tipo de banco de dados existente (Compose for Postgres, Database for Postgres ou Db2), em seguida, um banco de dados no menu suspenso **Banco de dados** e, em seguida, um **Esquema**:

    O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar dados relacionados ao modelo (dados de feedback, carga útil de pontuação) e métricas calculadas. Os planos Lite do Db2 não são suportados atualmente. Para obter mais informações sobre os dados de treinamento, veja [Por que o {{site.data.keyword.aios_short}} precisa de acesso aos meus dados de treinamento?](/docs/services/ai-openscale?topic=ai-openscale-trainingdata#trainingdata)
    {: note}

    ![Select database](images/gs-config-database3.png)

1.  Também é possível clicar em **Selecionar um local diferente** para especificar um local do banco de dados fora de sua conta do {{site.data.keyword.Bluemix_notm}}.

    O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar dados relacionados ao modelo (dados de feedback, carga útil de pontuação) e métricas calculadas. Os planos Lite do Db2 não são suportados atualmente.
    {: note}

    - Selecione o **Tipo de banco de dados** (`Compose for PostgreSQL`, `Database for PostgreSQL` ou `Db2`), em seguida, forneça as informações de conexão:

        - Para um banco de dados `Compose for PostgreSQL`, conclua o seguinte:

            - host ou endereço IP
            - Port
            - Banco de dados (nome)
            - Nome de usuário
            - Senha

            ![Specify Compose for Postgres db location](images/db-config-cpostgres.png)

        - Para um banco de dados `Database for PostgreSQL`, conclua o seguinte:

            - Nome do host ou Endereço IP
            - Porta SSL
            - Certificado Codificado Base-64
            - Banco de dados (nome)
            - Nome de usuário
            - Senha

            ![Specify Database for Postgres db location](images/db-config-dpostgres.png)

        - Para um banco de dados `Db2`, conclua o seguinte:

            - host ou endereço IP
            - Porta SSL
            - Banco de dados (nome)
            - Nome de usuário
            - Senha

            ![Specify Db2 location](images/db-config-db2.png)

    - Depois que você tiver se conectado com êxito, será possível selecionar um esquema.

      O nome do esquema precisará ser fornecido explicitamente se você fornecer uma instância do Db2 com acesso limitado, que não permite que o nome do esquema seja gerado automaticamente. Isso se aplica ao plano Entry do Db2 Warehouse.
      {: important}

      ![Select schema](images/gs-config-database5.png)

1.  Clique em **Avançar** para revisar os dados de resumo e, em seguida, clique em **Salvar**.



## Próximos passos
{: #cdb-next}

O {{site.data.keyword.aios_short}} agora está pronto para você [enviar uma carga útil de pontuação](/docs/services/ai-openscale?topic=ai-openscale-connect-db#cdb-score) e [configurar monitores para suas implementações](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
