---

copyright:
  years: 2018, 2019
lastupdated: "2019-04-09"

keywords: databases, connections, scoring, requests

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Especificando um Banco de Dados
{: #connect-db}

Especifique um banco de dados para ser usado por sua instância do {{site.data.keyword.aios_short}}.
{: shortdesc}

## Conectando-se ao seu banco de dados
{: #cdb-connect}

O {{site.data.keyword.aios_short}} usa um banco de dados para armazenar dados de carga útil, feedback e medição. Além de selecionar um banco de dados, você também pode selecionar um esquema para seu banco de dados - um esquema é uma coleção nomeada de tabelas no banco de dados.

1.  Escolha um banco de dados. Você tem duas opções: o banco de dados do plano Lite grátis ou um banco de dados novo ou existente.

    ![Select database](images/gs-config-database.png)

    Se você tiver uma conta paga do {{site.data.keyword.cloud_notm}}, poderá provisionar um serviço `Databases for PostgreSQL` ou `Db2 Warehouse` para tirar total proveito da integração com o Watson Studio e serviços de aprendizado contínuo. Se você escolher não provisionar um serviço pago, será possível usar o armazenamento PostgreSQL interno grátis com o {{site.data.keyword.aios_short}}, mas não será possível configurar o aprendizado contínuo para seu modelo.
    {: note}

### Banco de dados de plano Lite livre
{: #cdb-lite}

**NOTA**: o banco de dados do plano Lite grátis tem algumas limitações importantes:

- O banco de dados do plano Lite grátis é hospedado e não está acessível diretamente a você.
- O {{site.data.keyword.aios_full}} terá acesso total a seu banco de dados e, assim, terá acesso total a seus dados.
- O banco de dados do plano Lite grátis não é compatível com GDPR. Se seu modelo processa informações pessoalmente identificáveis (PII), não é possível usar o banco de dados do plano Lite grátis. Deve-se comprar um novo banco de dados ou usar um banco de dados existente que se adéque às regras do GDPR. Consulte [Segurança de Informações](/docs/services/ai-openscale?topic=ai-openscale-is-ov) para saber mais.

Para continuar com o uso do banco de dados do plano Lite grátis, simplesmente selecione essa opção e, em seguida, revise os dados de resumo e clique em **Salvar**.

  ![Select database](images/gs-config-database2.png)

### Banco de Dados Existente ou Novo
{: #cdb-exn}

1.  Após a seleção da opção "Usar banco de dados existente ou comprar um novo", o {{site.data.keyword.aios_short}} verifica sua conta do {{site.data.keyword.Bluemix_notm}} para localizar quaisquer bancos de dados existentes.

1.  Selecione seu tipo de banco de dados existente (Compose for Postgres, Database for Postgres ou Db2), em seguida, um banco de dados no menu suspenso **Banco de dados** e, em seguida, um **Esquema**:

    O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar o resultado da implementação de modelo e os dados de novo treinamento. Os planos Lite do Db2 não são suportados atualmente.
    {: note}

    ![Select database](images/gs-config-database3.png)

1.  Também é possível clicar em **Selecionar um local diferente** para especificar um local do banco de dados fora de sua conta do {{site.data.keyword.Bluemix_notm}}.

    O {{site.data.keyword.aios_short}} usa um banco de dados PostgreSQL ou Db2 para armazenar o resultado da implementação de modelo e os dados de novo treinamento. Os planos Lite do Db2 não são suportados atualmente.
    {: note}

    - Selecione o **Tipo de banco de dados** (`Compose for PostgreSQL`, `Database for PostgreSQL` ou `Db2`), em seguida, forneça as informações de conexão:

        - Para um banco de dados `Compose for PostgreSQL`, conclua o seguinte:

            - host ou endereço IP
            - Port (Porta)
            - Banco de dados (nome)
            - Username
            - Senha

            ![Specify Compose for Postgres db location](images/db-config-cpostgres.png)

        - Para um banco de dados `Database for PostgreSQL`, conclua o seguinte:

            - Nome do host e endereço IP
            - Porta SSL
            - Certificado Codificado Base-64
            - Banco de dados (nome)
            - Username
            - Senha

            ![Specify Database for Postgres db location](images/db-config-dpostgres.png)

        - Para um banco de dados `Db2`, conclua o seguinte:

            - host ou endereço IP
            - Porta SSL
            - Banco de dados (nome)
            - Username
            - Senha

            ![Specify Db2 location](images/db-config-db2.png)

    - Depois que você tiver se conectado com êxito, será possível selecionar um esquema.

      O nome do esquema precisará ser fornecido explicitamente se você fornecer uma instância do Db2 com acesso limitado, que não permite que o nome do esquema seja gerado automaticamente. Isso se aplica ao plano Entry do Db2 Warehouse.
      {: important}

      ![Select schema](images/gs-config-database5.png)

1.  Clique em **Avançar** para revisar os dados de resumo e, em seguida, clique em **Salvar**.

## Enviando uma Solicitação de Pontuação
{: #cdb-score}

Para configurar os monitores, o {{site.data.keyword.aios_short}} requer que você envie uma solicitação de pontuação para começar a registrar os dados que serão monitorados.

Os modelos implementados no Watson Machine Learning são pontuados automaticamente pelo {{site.data.keyword.aios_short}}. Se tiver somente modelos implementados no Watson Machine Learning, você não verá essa tela.
{: note:}

Selecione uma implementação, neste caso, "Detector de fraude" e, em seguida, use os fragmentos de código `cURL` ou `Python` fornecidos para registrar os dados de solicitação e resposta da implementação de modelo. Consulte [Criação de log de carga útil para instâncias de serviço não do Watson Machine Learning](/docs/services/ai-openscale?topic=ai-openscale-cml-connect) para obter mais detalhes.

Os campos e valores nos fragmentos de código precisam ser substituídos por seus valores reais, uma vez que os fornecidos são apenas exemplos.
{: important}

![Select database](images/config-send-scoring.png)

Depois de ter executado a criação de log de carga útil, você verá um visto na coluna "Pronto para monitorar" para a implementação selecionada. Clique em **Configurar Monitores** para continuar.

## Próximos passos
{: #cdb-next}

O {{site.data.keyword.aios_short}} está agora pronto para você [configurar monitores para suas implementações](/docs/services/ai-openscale?topic=ai-openscale-mo-config).
