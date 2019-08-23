---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

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

# Configurando o monitor de detecção de desvio ![beta tag](images/beta.png)
{: #behavior-drift-config}

Deve-se configurar o monitor de desvio do {{site.data.keyword.aios_full}} antes que ele possa começar a analisar seu modelo. Há duas opções: treinar o seu modelo on-line ou usar um bloco de notas.
{: shortdesc}

Será possível treinar o seu modelo on-line usando o {{site.data.keyword.aios_short}} se você usar o {{site.data.keyword.pm_full}} e seus dados não excederem 500 MB. Caso contrário, deve-se usar um bloco de notas para treinar o modelo.

## Etapas para configurar o desvio no {{site.data.keyword.aios_short}}
{: #behavior-drift-config-steps-wos}

Se você usar o {{site.data.keyword.pm_full}}, você terá a opção de usar a interface com o usuário do {{site.data.keyword.aios_short}} para configurar a detecção de desvio.

1. Na guia **Desvio**, em **O que é desvio**? clique em **Iniciar** para começar o processo de configuração.

   ![página O que é desvio?](images/wos-drift-config-1.png)

2. Clique no bloco **Treinar no Watson OpenScale**.

   ![página O que é desvio?](images/drift-config-2.png)

3. Configure o limite de alerta.

   ![página O que é desvio?](images/drift-config-3.png)

3. Configure o tamanho da amostra.

   ![página O que é desvio?](images/drift-config-4.png)
   
3. Clique em **Salvar**.


## Etapas para configurar o desvio usando um bloco de notas
{: #behavior-drift-config-steps-ntbk}

Se você usar um provedor de aprendizado de máquina diferente do {{site.data.keyword.pm_full}}, como o Microsoft Azure, o Amazon SageMaker ou um mecanismo de aprendizado de máquina customizado, você deverá usar um bloco de notas para configurar a detecção de desvio. Também é possível configurar o desvio para o {{site.data.keyword.pm_full}} usando esse método.

Essa opção é útil se os dados de treinamento não são armazenados no Db2 ou no {{site.data.keyword.cos_full}}. Usando um notebook, deve-se ler os dados de treinamento em um quadro de dados. O bloco de notas especializado que pode ser transferido por download por meio do {{site.data.keyword.aios_short}} cria uma saída especializada que pode ser transferida por upload para o {{site.data.keyword.aios_short}}.

1. Crie um bloco de notas para gerar o modelo de detecção de desvio. Use [o bloco de notas de amostra](https://github.com/IBM-Watson/aios-data-distribution/blob/master/training_statistics_notebook.ipynb) que está disponível na IU do {{site.data.keyword.aios_short}}.
2. Use o software de compactação para compactar o modelo de detecção de desvio em um arquivo .tar.gz.

1. Na guia **Desvio**, em **O que é desvio**? clique em **Iniciar** para começar o processo de configuração.

   ![página O que é desvio?](images/wos-drift-config-1.png)

2. Clique no bloco **Treinar em um bloco de notas**.

   ![Página Configuração de desvio com uma opção on-line e uma opção de bloco de notas](images/drift-config-2.png)

3. Arraste o arquivo de modelo compactado para a zona de destino ou navegue para selecioná-lo e clique em **Avançar**.

   ![página O que é desvio?](images/wos-drift-config-2b.png)
   
3. Faça upload do modelo de detecção de desvio e clique em **Avançar**.

   ![página O que é desvio?](images/drift-config-upload.png)
   
3. Configure o limite de alerta.

   ![página O que é desvio?](images/drift-config-3.png)

3. Configure o tamanho da amostra.

   ![página O que é desvio?](images/drift-config-4.png)
   
3. Clique em **Salvar**.

## Próximos passos
{: #behavior-drift-config-next-steps}

- Para obter mais informações sobre a interpretação de desvio, consulte [Magnitude de desvio](/docs/services/ai-openscale?topic=ai-openscale-behavior-drift-ovr)
