---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-28"

keywords: fairness, monitoring, charts, de-biasing, bias, accuracy

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

# Explicando modelos de imagem
{: #ie-image}

O {{site.data.keyword.aios_short}} suporta explicabilidade para dados de imagem.
{: shortdesc}

## Trabalhando com um modelo de imagem
{: #ie-image-working}

1. Configure o seu ambiente.
   2. Instale os pacotes do {{site.data.keyword.aios_short}} e do {{site.data.keyword.pm_full}}.
   3. Configure as suas credenciais.
   4. Instale as bibliotecas que são necessárias para criar os modelos e executar a análise. Essas incluem as bibliotecas a seguir:
      - `keras`
      - `tensorflow`
      - `keras_sequential_ascii`
      - `numpy`
      - `pillow`

1. Crie e implemente o seu modelo baseado em imagem.
   2. Crie pastas para as imagens com base em como classificá-las.
       - Dentro do diretório `data` principal, deve-se ter os subdiretórios `train` e `validation`.
       - Dentro de cada um dos subdiretórios, deve-se ter seus diretórios de classificação.
  2. Padronize o tamanho da imagem e, em seguida, configure os subdiretórios a serem usados para treinamento e validação.
  3. Pré-processe os dados para escalar novamente e recuperar as imagens e suas classes.
  4. Defina e treine o modelo.
  5. Armazene o modelo.
  6. Implemente o modelo.

7. Configure o {{site.data.keyword.aios_short}} designando o `APIClient`, assinando o ativo e pontuando o modelo.
8. Configure a explicabilidade.
   9. Ative a explicabilidade.
   10. Obtenha explicações para as transações.
   11. Exiba as imagens explicadas. 

## Explicando transações do modelo de imagem
{: #ie-image-workingviewing}

Para obter um exemplo de modelo de classificação de imagem de explicabilidade, é possível ver quais partes de uma imagem contribuíram de forma positiva para o resultado previsto e quais contribuíram de forma negativa. No exemplo a seguir, a imagem na área de janela positiva mostra as partes que afetaram positivamente a predição, e a imagem na área de janela negativa mostra as partes de imagens que tiveram um impacto negativo no resultado.

![O detalhe de confiança da classificação da imagem de explicabilidade é exibido com uma imagem de um cão que também tem partes destacadas para mostrar que elas ajudaram a determinar a imagem como um cão](images/insight-explain-image.png)

Para o {{site.data.keyword.pm_full}}, a entrada de pontuação para modelos de classificação de imagem enviados para a criação de log de carga útil não pode exceder ai-open-scale-ibm-aios-scheduling  | 1 | Planejando o serviceMB. Para evitar problemas de tempo limite, as imagens não devem exceder 125 x 125 pixels e devem ser enviadas sequencialmente de modo que a explicação para a segunda imagem seja solicitada quando a primeira estiver concluída.
{: note}


## Exemplos de modelo de imagem
{: #ie-image-working-ntbks}

Use as duas anotações a seguir para ver amostras de código detalhadas e desenvolver suas próprias implementações do {{site.data.keyword.aios_short}}:

- [Tutorial sobre como gerar uma explicação para um modelo baseado em imagem](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Tutorial sobre como gerar uma explicação para um modelo de classificador binário baseado em imagem](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}

