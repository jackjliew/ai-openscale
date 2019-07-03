---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-11"


keywords: troubleshooting, bias

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

# Solução de Problemas
{: #ts-trouble}

## Problemas comuns do {{site.data.keyword.aios_full}}
{: #ts-trouble-common}

Os problemas a seguir são comuns para o {{site.data.keyword.aios_full}} on Cloud e o {{site.data.keyword.wos4d_full}}.

### A análise da carga útil não é exibida corretamente
{: #ts-trouble-common-payloadfileformat}

- Situação: a mensagem de erro a seguir é exibida:
  - código de erro: AIQDT0044E
  - texto do erro: caractere proibido `"` no nome da coluna `<column name>`

- Situação: para um processamento adequado de análise da carga útil, o {{site.data.keyword.aios_short}} não suporta nomes de coluna com aspas duplas (") na carga útil. Isso afeta a carga útil de pontuação e os dados de feedback nos formatos de CSV e de JSON.
- Solução: remova as aspas duplas (") dos nomes de colunas do arquivo de carga útil.

## Problemas específicos do {{site.data.keyword.wos4d_full}}
{: #ts-trouble-icp}

Os problemas a seguir são específicos do {{site.data.keyword.wos4d_full}}:

## O serviço de Bias / Fairness está inativo
{: #ts-bfdown}

### Visão geral
{: #ts-bfdov}

- Situação: ai-open-scale-ibm-aios-bias_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: etcd

### Configurar kubectl
{: #ts-bfdck}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-bfdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **2/2**.  Usaremos `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o <format>. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

    - Certifique-se de que você tenha o nome da imagem correta.
    - Você enviou por push a imagem para o repositório?
    - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Como esse pod tem 3 contêineres aios-bias, ml-gateway-sidecar e check-etcd-ready, também será necessário consultar o log de ml-gateway-sidecar e check-etcd-ready se aios-bias não tiver nenhum problema:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    Em geral, os logs devem conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações dos logs.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---
## {{site.data.keyword.aios_short}} o serviço está inativo
{: #ts-aiosdown}

### Visão geral
{: #ts-odov}

- Situação: ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil . . .
- Sistema de Monitoramento:
- Dependências: etcd

### Configurar kubectl
{: #ts-odkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}

    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-odvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

        Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

        - Inclua mais nós no cluster.

        - Finalize os pods desnecessários para dar espaço para os pods pendentes.
        ```bash
        kubectl -n [namespace] delete pod [pod name]
        ```

        - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

        - Certifique-se de que você tenha o nome da imagem correta.
        - Você enviou por push a imagem para o repositório?
        - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---
## {{site.data.keyword.aios_short}} o serviço de configuração está inativo
{: #ts-aiosconfigdown}

### Visão geral
{: #ts-ocdov}

- Situação: ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: etcd

### Configurar kubectl
{: #ts-ocdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-ocdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-configuration-554f548667-7l782` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} o serviço de painel está inativo
{: #ts-aiosdashdown}

### Visão geral
{: #ts-oddov}

- Situação: ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: N/A

### Configurar kubectl
{: #ts-oddkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-oddvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---
## O serviço Data Mart é mostrado
{: #ts-datamartdown}

### Visão geral
{: #ts-dmdov}

- Situação: ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: etcd

### Configurar kubectl
{: #ts-dmdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-dmdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## O serviço de explainabilidade está inativo
{: #ts-expdown}

### Visão geral
{: #ts-esdov}

- Situação: ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: etcd

### Configurar kubectl
{: #ts-esdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-esdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **2/2**.  Usaremos `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Como esse pod tem 3 contêineres explainability-service, ml-gateway-sidecar e check-etcd-ready, também será necessário consultar o log de ml-gateway-sidecar e check-etcd-ready se explainability-service não tiver nenhum problema:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      Em geral, os logs devem conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações dos logs.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} o serviço de feedback está inativo
{: #ts-aiosfeedbackdown}

### Visão geral
{: #ts-fsdov}

- Situação: ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: etcd

### Configurar kubectl
{: #ts-fsdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-fsdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **2/2**.  Usaremos `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Como esse pod tem 3 contêineres aios-feedback, ml-gateway-sidecar e check-etcd-ready, também será necessário consultar o log de ml-gateway-sidecar e check-etcd-ready se aios-feedback não tiver nenhum problema:

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      Em geral, os logs devem conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações dos logs.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} o serviço de descoberta está inativo
{: #ts-aiosdiscdown}

### Visão geral
{: #ts-dsdov}

- Situação: ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: N/A

### Configurar kubectl
{: #ts-dsdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Opção 2: usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-dsdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} O serviço nginx está inativo
{: #ts-aiosnginxdown}

### Visão geral
{: #ts-nsdov}

- Situação: ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: N/A

### Configurar kubectl
{: #ts-nsdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-nsdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## O serviço de API de criação de log de carga útil do {{site.data.keyword.aios_short}} está inativo
{: #ts-aiospayloadapidown}

### Visão geral
{: #ts-pladov}

- Situação: ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- Impacto ao cliente: os clientes não podem gravar a Carga útil em nosso serviço por meio de serviços externos (Azure, Amazon, outros), portanto os clientes não têm dados atuais para análise.
- Sistema de Monitoramento:
- Dependências: IBM Event Stream

### Configurar kubectl
{: #ts-pladkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-pladvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o <format>. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} o serviço de registro de carga útil está inativo
{: #ts-aiospayloaddown}

### Visão geral
{: #ts-plsdov}

- Situação: ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- Impacto ao cliente: os clientes não podem gravar a Carga útil em nosso serviço por meio de serviços externos (Azure, Amazon, outros), portanto os clientes não têm dados atuais para análise.
- Sistema de Monitoramento:
- Dependências: IBM Event Stream

### Configurar kubectl
{: #ts-plsdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-plsdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running   1          6h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o <format>. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} o serviço de planejamento está inativo
{: #ts-aiosscheddown}

### Visão geral
{: #ts-ssdov}

- Situação: ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: N/A

### Configurar kubectl
{: #ts-ssdkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}`:8443
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-ssdvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Nós usaremos `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## {{site.data.keyword.aios_short}} o serviço redis está inativo
{: #ts-aiosredisdown}

### Visão geral
{: #ts-redov}

- Situação: ai-open-scale-ibm-aios-redis_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: N/A

### Configurar kubectl
{: #ts-redkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-redvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep redis)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    aios-redis-sentinel-6d5bffbcd8-hjvgk                          1/1       Running    0          14m
    aios-redis-sentinel-6d5bffbcd8-j4htd                          1/1       Running    0          14m
    aios-redis-sentinel-6d5bffbcd8-w4vcb                          1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-h4nfh                            1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-k9ggw                            1/1       Running    0          14m
    aios-redis-server-6f4c55fd75-nlrr4                            1/1       Running    0          14m
    ```

    Assegure-se de que o status seja **em execução** e que esteja totalmente pronto **1/1**.  Usaremos o `aios-redis-server-6f4c55fd75-nlrr4` como nosso pod para os exemplos a seguir.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale descreve pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o <format>. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## o serviço etcd está inativo
{: #ts-etcddown}

### Visão geral
{: #ts-etcov}

- Situação: etcd_micro_service_is_down:
- Impacto ao cliente: os clientes não podem usar nenhuma funcionalidade, como configurar novas instâncias, analisar solicitações, armazenar carga útil...
- Sistema de Monitoramento:
- Dependências: Nenhuma

### Configurar kubectl
{: #ts-etckc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Etapas de Verificação / Recuperação
{: #ts-etcvr}

1.  Verifique o status do pod com os comandos a seguir:

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep etcd)
    NAME                                         READY     STATUS    RESTARTS   AGE
    etcd-0                                       1/1       Running             3          8d
    etcd-1                                       1/1       Running             0          8d
    etcd-2                                       1/1       Running             0          8d
    ```

    Assegure-se de que haja três pods etcd, seus status sejam **em execução** e eles estejam totalmente prontos **1/1**.

1.  Descreva o pod se ele não estiver no estágio de execução:

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    Esse comando exibirá detalhes sobre o pod.  Isso também fornecerá erros se seu módulo não estiver no estágio de execução.  Seu pod poderá encontrar os casos a seguir quando ele não estiver no estágio de execução:

    - **Meu pod permanece pendente**

      Se o pod permanecer **Pendente**, isso significa que ele não pode ser planejado em um nó.  Geralmente, isso é porque há recurso insuficiente de um tipo ou outro que impede o planejamento.  Execute o comando anterior para obter mais informações. Deve haver mensagens do planejador sobre por que ele não pode planejar seu pod. Você pode ter esgotado o fornecimento de CPU ou Memória em seu cluster. Nesse caso, é possível tentar várias coisas:

      - Inclua mais nós no cluster.

      - Finalize os pods desnecessários para dar espaço para os pods pendentes.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Verifique se o pod não é maior que seus nós. Por exemplo, se todos os nós tiverem uma capacidade de cpu:1, um pod com uma solicitação de cpu: 1.1 nunca será planejado.

      É possível verificar as capacidades de nó com o comando kubectl get nodes -o `<format>`. Aqui estão algumas linhas de comandos de exemplo que extraem apenas as informações necessárias:
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Meu pod permanece esperando**

      Se um pod estiver preso no estado **Em espera**, ele foi planejado para um nó do trabalhador, mas não pode ser executado nessa máquina. Novamente, as informações do Kubectl descrevem ... devem ser informativas. A causa mais comum de pods **Em espera** é uma falha no pull da
imagem. Há três coisas para verificar:

      - Certifique-se de que você tenha o nome da imagem correta.
      - Você enviou por push a imagem para o repositório?
      - Execute um `docker pull` manual para puxar a imagem em seu cluster para ver se a imagem pode ser puxada.

    - **Meu pod está travando ou, de alguma forma, não é funcional**

      Primeiro, consulte os logs do contêiner atual:
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      Se o contêiner tiver travado anteriormente, será possível acessar o log de travamento do contêiner anterior com:
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      Em geral, o log deve conter informações sobre por que o pod não foi iniciado com êxito.  Corrija o problema com base nas informações do log.  Se nenhuma dessas abordagens funcionar, continue com as etapas de Escalada

---

## Criar um painel com event_stream
{: #ts-createdashes}

### Visão geral
{: #ts-dshov}

- Este documento descreve como criar o novo painel para monitorar os serviços do {{site.data.keyword.aios_full}}.

### Configurar kubectl
{: #ts-dshkc}

Há duas maneiras de configurar o cliente kubectl.

1.  Usando a ferramenta cloudctl

    Se o cloudctl estiver disponível em seu laptop, execute o comando a seguir para configurar o kubectl:
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    Substitua `${username}`, `${password}`, `${ICP Host}` pelo valor real.  Por
Exemplo:
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  Usando a configuração kubectl por meio do console do {{site.data.keyword.icpfull}}
    - Efetue login em seu cluster do {{site.data.keyword.icpfull}} `https://${ICP Host}:8443`
    - Selecione o ícone **pessoa redonda** > **Configurar cliente**
    - Clique no ícone **Copiar para a área de transferência** para copiar as informações de configuração para a área de transferência
    - Mude o namespace de `aiopenscale` para `es`, se necessário.
    - Cole as informações de configuração em sua linha de comandos e pressione **Enter**.

### Visualizando o fluxo de eventos
{: #ts-dshve}

O fluxo do evento consiste em vários serviços.  Consulte a subpasta para obter detalhes de cada serviço.

  ```bash
  $ kubectl get pods -n eventstream
  NAME                                                  READY     STATUS              RESTARTS   AGE
  es-ibm-es-access-controller-deploy-54cd9bc959-899s7   2/2       Running             0          20d
  es-ibm-es-access-controller-deploy-54cd9bc959-zcgx8   2/2       Running             0          16d
  es-ibm-es-kafka-sts-0                                 4/4       Running             15         17d
  es-ibm-es-kafka-sts-1                                 4/4       Running             264        15d
  es-ibm-es-kafka-sts-2                                 4/4       Running             370        22d
  es-ibm-es-proxy-deploy-5866fbd8cb-jk6rd               1/1       Running             0          9d
  es-ibm-es-proxy-deploy-5866fbd8cb-rjx5q               1/1       Running             0          9d
  es-ibm-es-rest-deploy-585df7f77c-j2d5k                3/3       Running             0          22d
  es-ibm-es-ui-deploy-6f59c7764c-7tlzn                  3/3       Running             55         16d
  es-ibm-es-zookeeper-sts-0                             1/1       Running             0          17d
  es-ibm-es-zookeeper-sts-1                             1/1       Running             1          15d
  es-ibm-es-zookeeper-sts-2                             1/1       Running   488        9d
  ```

---

## Usando o {{site.data.keyword.aios_short}} monitoramento
{: #ts-aiosusemonitor}

### Visão geral
{: #ts-omov}

- Este documento descreve como criar o novo painel para monitorar os serviços do {{site.data.keyword.aios_full}}.

### Configurando o Painel
{: #ts-omsd}

- Obtenha o arquivo aios-dashboard.json do ibm-aiopenscale-x86_64-1.0.0.tar.gz.  Esse arquivo pode ser localizado no diretório `utils`.
- Efetue login em seu cluster do ICP `https://${ICP Host}:8443`
- Selecione `Menu` > `Plataforma` > `Monitoramento`
- Clique no ícone `Início`
- Clique no item de menu `Importar painel`
- Clique no botão `Upload .json File` e aponte para o seu aios-dashboard.json
- Selecione `prometheus` para o campo de entrada prometheus

### Visualizando o painel
{: #ts-omvd}

O painel consiste nas linhas a seguir:

- Uso total do cluster

  Essa linha mostra o uso de CPU em todo o cluster, o uso de memória e o uso de sistema de arquivos. Os velocímetros mostram se o seu cluster é funcional. Se eles mostrarem condições não funcionais, inclua mais nós no cluster ou finalize os pods desnecessários para criar espaço para outras implementações.

- Disponibilidade por Serviço

  Essa linha mostra a disponibilidade para cada serviço.  Os painéis iniciais mostram o total de contêineres prontos.  Se o velocímetro mostra 100%, seu {{site.data.keyword.aios_short}} está funcional.  Caso contrário, é possível consultar a tabela para descobrir qual serviço está inativo para tomar a ação para deixar esse serviço ativo.  Há outros runbooks do {{site.data.keyword.aios_short}} que ajudam a diagnosticar por que um contêiner não foi iniciado com êxito.  Após os painéis iniciais estão os painéis para os serviços individuais. Diferentes linhas mostram o número de contêineres que estão prontos e que são solicitados.

- CPU por serviço

  Essa linha mostra o uso de CPU para cada serviço e inclui o número de núcleos da CPU que cada contêiner usa e o número limite de núcleos de CPU que cada contêiner pode usar.  Se esses valores estiverem muito próximos, verifique por que o contêiner consome muito recurso de CPU.  Se necessário, será possível aumentar o limite de cpu para esse contêiner editando o limite de implementação e atualização de cpu:
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Por exemplo:
  ```bash
  kubectl -n aiopenscale editar implementação ai-open-scale-ibm-aios-bias
  ```

- Memória por Serviço

  Essa linha mostra o uso de memória para cada serviço e inclui a memória que cada contêiner usa e a memória que cada contêiner pode usar.  Se esses valores estiverem muito próximos, verifique por que o contêiner consome muita memória.  Se necessário, será possível aumentar a memória para esse contêiner editando o limite de implementação e atualização de memória:
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Por exemplo:
  ```bash
  kubectl -n aiopenscale editar implementação ai-open-scale-ibm-aios-bias
  ```

- Sistema de arquivos por serviço

  Essa linha mostra o uso de sistema de arquivos para cada serviço.  Se o monitor mostrar o uso de sistema de arquivos que está aumentando constantemente, inspecione o contêiner para ver por que o uso do sistema de arquivos continua subindo.  Se necessário, é possível entrar em contato com o canal Slack anterior para obter ajuda adicional.

- Imagens e versões

  Essa linha lista todas as imagens e versões que são usadas para o {{site.data.keyword.aios_full}}.
