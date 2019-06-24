---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-24"

keywords: feedback data, data, feedback, models

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

# Formatando e fazendo upload de dados de feedback no {{site.data.keyword.aios_short}}
{: #fmt-upld-fdbk-data}

Os dados de feedback são essenciais para manter um modelo despropenso. Deve-se fazer upload de dados de feedback para o serviço {{site.data.keyword.aios_full}} regularmente para assegurar que o seu modelo considere os dados atualizados que podem indicar mudanças no contexto de seu aplicativo preditivo.  Com um loop de feedback, o sistema aprende continuamente por meio do monitoramento da efetividade das previsões e de novo treinamento quando necessário. O monitoramento e o uso do feedback resultante estão no núcleo do aprendizado de máquina. As informações a seguir são destinadas a ajudá-lo a formatar e fazer upload de seus dados de feedback.
(: shortdesc)

## Formatação de dados de feedback
{: #fmt-upld-fdbk-data-fmt}

Para que os dados de feedback sejam lidos corretamente, eles devem ser formatados corretamente. O serviço {{site.data.keyword.aios_short}} aceita os formatos a seguir:

- Formatos de arquivo CSV, que podem ser transferidos por upload usando a IU ou a API de REST
- Formatos de arquivo JSON, que apenas podem ser transferidos por upload usando a API de REST

Esses formatos de arquivo são definidos por um esquema, `training_data_schema`, que está disponível nos detalhes da assinatura. Para visualizar o `training_data_schema`, execute o comando a seguir usando a API de Python:

```
subscription.get_details()['entity']['asset_properties']['training_data_schema']
```

Para comparar o esquema de dados de treinamento ao esquema de feedback, talvez você queira visualizar o esquema de feedback também. Para visualizar o esquema de feedback, execute o comando a seguir usando a API de Python:

```
subscription.feedback_logging.print_table_schema()
```


### formato CSV
{: #fmt-upld-fdbk-data-fmt-csv}

Para um arquivo CSV, normalmente você fornece os dados em colunas e linhas com uma linha para os nomes de coluna.

Geralmente, não são necessárias aspas quando os nomes de coluna estão todos em letras maiúsculas, o que os torna sem distinção entre maiúsculas e minúsculas para o Db2, no entanto, para outros bancos de dados e na instância em que os nomes de coluna são compostos por letras maiúsculas e minúsculas, as letras devem corresponder.
Se o arquivo contiver nomes de coluna, as colunas não precisarão corresponder à ordem da tabela necessariamente, porém, se o arquivo não tiver nomes de coluna, você deverá corresponder a ordem da tabela. É possível ter colunas que não estão nos dados de treinamento originais. Essas colunas são ignoradas durante o processamento.


### Formato JSON
{: #fmt-upld-fdbk-data-fmt-json}

O formato JSON consiste em uma coleção de objetos com campos correspondentes aos nomes de coluna.

