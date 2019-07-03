---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"

keywords: explainability, monitoring, explain, explaining, transactions, transaction ID

subcollection: ai-openscale

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}

# Explicando transações
{: #ie-ov}

Para cada implementação, é possível ver dados de explicabilidade para transações específicas.
{: shortdesc}

## Explicando transações
{: #ie-view}

No ladrilho de implementação selecionado, selecione a guia **Explicar uma transação** (![guia Explicar uma transação](images/insight-transact-tab.png)) no navegador e insira um ID de transação.

Sempre que os dados são enviados ao modelo para pontuação, ele define um ID de transação no cabeçalho de HTTP configurando o campo `X-Global-Transaction-Id`. Esse ID de transação é armazenado na tabela de carga útil. Para localizar uma explicação do comportamento do modelo para uma pontuação específica, especifique o ID de transação associado a essa solicitação de pontuação. Observe que esse comportamento se aplica somente a transações do {{site.data.keyword.pm_full}} e não é aplicável a transações não WML.
{: note}

### Localizando um ID de transação em {{site.data.keyword.aios_short}}
{: #ie-find}

1.  No gráfico de horário para sua implementação, deslize o marcador no gráfico e clique no link **Visualizar detalhes** para [visualizar dados para uma hora específica](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-vdet).
1.  Clique no botão **Visualizar transações** para [visualizar a lista de IDs de transação](/docs/services/ai-openscale?topic=ai-openscale-it-ov#it-tra).
1.  Copie um dos IDs de transação da lista, cole-o na caixa de procura na página **Explicar uma transação** e pressione Enter.

    A lista de IDs de transação também tem a opção de simplesmente clicar no link **Explicar** na coluna Ação para qualquer ID de transação, que abrirá essa transação na guia Explicabilidade.
    {: note}

  Consulte as seções a seguir para obter exemplos de explicações para diferentes tipos de modelos.

  ![Explainability transaction ID](images/insight-explain-trans-id.png)

## Exemplo de modelo categórico
{: #ie-class}

Este exemplo de explicabilidade é para um modelo de classificação binária que aprova ou nega as solicitações de seguro. É possível ver os fatores que contribuíram de forma positiva ou negativa para o resultado final de `DENIED` neste caso.

O recurso *POLICY AGE* que tem um valor de `< 1 year` teve o impacto máximo no modelo que decide um resultado DENIED. Os outros recursos que contribuíram para esse resultado foram *CLAIM FREQUENCY* (`High`) e *AGE* (`18`), com somente um impacto menor de *CAR VALUE* (`$50,000`).

![Explainability binary classification](images/insight-explain-binary.png)

Embora os gráficos sejam úteis para mostrar os fatores mais significativos na determinação do resultado de uma transação, os modelos de classificação também podem incluir explicações avançadas, detalhadas nas seções `Minimum changes for Approved outcome` e `Minimum changes for this outcome`.

Explicações avançadas não estão disponíveis para modelos de texto de regressão, imagem e não estruturados.
{: note}

O `Minimum changes for Approved outcome` nos informa que, se os valores dos recursos foram mudados para os valores listados nesta seção, a predição do modelo mudará.

Da mesma forma, o `Minimum changes for this outcome` nos informa que, mesmo se os valores dos recursos fossem mudados para aqueles listados nessa seção, a predição do modelo não teria mudado.

Assim, esses dois valores nos informa o comportamento do modelo na proximidade do ponto de dados para o qual a explicação está sendo gerada.

![Explainability binary classification](images/insight-explain-binary2.png)

## Modelos de imagem
{: #ie-image}

O {{site.data.keyword.aios_short}} suporta explicabilidade para dados de imagem.

### Trabalhando com um modelo de imagem
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

### Explicando transações do modelo de imagem
{: #ie-image-workingviewing}

Para obter um exemplo de modelo de classificação de imagem de explicabilidade, é possível ver quais partes de uma imagem contribuíram de forma positiva para o resultado previsto e quais contribuíram de forma negativa. No exemplo a seguir, a imagem na área de janela positiva mostra as partes que afetaram positivamente a predição, e a imagem na área de janela negativa mostra as partes de imagens que tiveram um impacto negativo no resultado.

![Explainability image classification](images/insight-explain-image.png)

Para o {{site.data.keyword.pm_full}}, a entrada de pontuação para modelos de classificação de imagem que são enviados para a criação de log de carga útil não pode exceder 1 MB. Para evitar problemas de tempo limite, as imagens não devem exceder 125 x 125 pixels e devem ser enviadas sequencialmente de modo que a explicação para a segunda imagem seja solicitada quando a primeira estiver concluída.
{: note}


### Exemplos de modelo de imagem
{: #ie-image-working-ntbks}

Use as duas anotações a seguir para ver amostras de código detalhadas e desenvolver suas próprias implementações do {{site.data.keyword.aios_short}}:

- [Tutorial sobre como gerar uma explicação para um modelo baseado em imagem](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation.ipynb){: external}
- [Tutorial sobre como gerar uma explicação para um modelo de classificador binário baseado em imagem](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/image_explanation_binary.ipynb){: external}


## Modelos de texto não estruturados
{: #ie-unstruct}

O {{site.data.keyword.aios_short}} suporta explicabilidade para dados de texto não estruturados.

### Trabalhando com modelos de texto não estruturados
{: #ie-unstruct-steps}

1. Configure o seu ambiente.
   2. Instale os pacotes do {{site.data.keyword.aios_short}} e do {{site.data.keyword.pm_full}}.
   3. Configure as suas credenciais.
   4. Instale as bibliotecas que são necessárias para criar os modelos e executar a análise. Essas incluem as bibliotecas a seguir:
      - `pandas`
      - `pyspark` (se não estiver usando o {{site.data.keyword.DSX}})

1. Crie e implemente o seu modelo baseado em imagem.
   2. Carregue dados de treinamento em um quadro pandas.
   2. Treine o modelo com os dados.
   3. Publique o modelo.
   4. Implemente e pontue o modelo.

7. Configure o {{site.data.keyword.aios_short}} designando o `APIClient`, assinando o ativo e pontuando o modelo.
8. Configure a explicabilidade.
   9. Ative a explicabilidade.
   10. Obtenha explicações para as transações.

### Explicando transações de texto não estruturadas
{: #ie-unstruct-xplan}

O exemplo de explicabilidade a seguir mostra um modelo de classificação que avalia texto não estruturado. A explicação mostra as palavras-chave que tiveram um impacto positivo e também negativo na predição do modelo. Mostramos também a posição das palavras-chave identificadas no texto original que foi alimentado como entrada para o modelo.

![Explainability image classification](images/insight-explain-text.png)

### Exemplo de modelo de texto não estruturado
{: #ie-unstruct-ntbkssample}

Use as anotações a seguir para ver amostras de código detalhadas e desenvolver suas próprias implementações do {{site.data.keyword.aios_short}}:

- [Tutorial sobre como gerar uma explicação para um modelo baseado em texto](https://github.ibm.com/aiopenscale/explainability/blob/master/public/notebooks/demo/text_explanation.ipynb){: external}
