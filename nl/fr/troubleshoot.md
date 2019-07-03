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

# Résolution des problèmes
{: #ts-trouble}

## Problèmes courants avec {{site.data.keyword.aios_full}}
{: #ts-trouble-common}

Les problèmes suivants sont communs à {{site.data.keyword.aios_full}} on Cloud et {{site.data.keyword.wos4d_full}}.

### L'analyse du contenu ne s'affiche pas correctement
{: #ts-trouble-common-payloadfileformat}

- Situation : le message d'erreur suivant s'affiche :
  - code d'erreur : AIQDT0044E
  - texte d'erreur : Caractère interdit `"` dans le nom de la colonne `<column name>`

- Situation : pour le bon traitement des analyses de contenu, {{site.data.keyword.aios_short}} n'accepte pas les noms de colonne
avec des guillemets (") dans le contenu.
Cela concerne à la fois le contenu d'évaluation et les données de commentaires au format CSV ou JSON.
- Solution : retirez les guillemets (") des noms de colonne du fichier de contenu.

## Problèmes spécifiques à {{site.data.keyword.wos4d_full}}
{: #ts-trouble-icp}

Les problèmes suivants sont spécifiques à {{site.data.keyword.wos4d_full}} :

## Le service de biais/équité est indisponible
{: #ts-bfdown}

### Présentation
{: #ts-bfdov}

- Situation : ai-open-scale-ibm-aios-bias_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : etcd

### Configuration de kubectl
{: #ts-bfdck}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-bfdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep bias)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv                  2/2       Running   0          2h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **2/2**.  Nous utiliserons `ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o <format>. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

    - Vérifiez que le nom de l'image est correct.
    - Avez-vous inséré l'image dans le référentiel ?
    - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv aios-bias
      ```

      Dans la mesure où ce pod dispose de 3 conteneurs, aios-bias, ml-gateway-sidecar et check-etcd-ready, vous devez également vérifier dans le journal de ml-gateway-sidecar et check-etcd-ready si aios-bias ne rencontre pas un problème :

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-bias-7b64f7c59f-rjjdv ml-gateway-sidecar
      ```

    En général, les journaux doivent expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations des journaux.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---
## Le service {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosdown}

### Présentation
{: #ts-odov}

- Situation : ai-open-scale-ibm-aios-common-api_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc. . .
- Système de surveillance :
- Dépendances : etcd

### Configuration de kubectl
{: #ts-odkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}

    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-odvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep common-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c             1/1       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

        Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

        - Ajoutez d'autres noeuds au cluster.

        - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
        ```bash
        kubectl -n [namespace] delete pod [pod name]
        ```

        - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :

      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

        - Vérifiez que le nom de l'image est correct.
        - Avez-vous inséré l'image dans le référentiel ?
        - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-common-api-577b75c445-2dg9c
      ```

    En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---
## Le service de configuration de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosconfigdown}

### Présentation
{: #ts-ocdov}

- Situation : ai-open-scale-ibm-aios-configuration_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : etcd

### Configuration de kubectl
{: #ts-ocdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :

  ```bash
  cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
  ```

  Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
  ```bash
  cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
  ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-ocdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep configuration)
    NAME                                                     READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-configuration-554f548667-7l782    1/1       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-configuration-554f548667-7l782` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-configuration-554f548667-7l782
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-configuration-554f548667-7l782
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service de tableau de bord de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosdashdown}

### Présentation
{: #ts-oddov}

- Situation : ai-open-scale-ibm-aios-dashboard_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : N/A

### Configuration de kubectl
{: #ts-oddkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-oddvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep dashboard)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz             1/1       Running   0          4h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-dashboard-55444db6b6-t6ckz
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---
## Le service de magasin de données est arrêté
{: #ts-datamartdown}

### Présentation
{: #ts-dmdov}

- Situation : ai-open-scale-ibm-aios-data-mart_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : etcd

### Configuration de kubectl
{: #ts-dmdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

2.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-dmdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep datamart)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb                1/1       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-datamart-7b84c7667-spzsb
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service d'explicabilité est indisponible
{: #ts-expdown}

### Présentation
{: #ts-esdov}

- Situation : ai-open-scale-ibm-aios-explainability_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : etcd

### Configuration de kubectl
{: #ts-esdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-esdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep explainability)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984        2/2       Running   0          4h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **2/2**.  Nous utiliserons `ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 explainability-service
      ```

      Dans la mesure où ce pod dispose de 3 conteneurs, explainability-service, ml-gateway-sidecar et check-etcd-ready, vous devez également vérifier dans le journal de ml-gateway-sidecar et check-etcd-ready si explainability-service ne rencontre pas un problème :

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-explainability-5cdb4687f5-4c984 ml-gateway-sidecar
      ```

      En général, les journaux doivent expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations des journaux.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service de commentaires de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosfeedbackdown}

### Présentation
{: #ts-fsdov}

- Situation : ai-open-scale-ibm-aios-feedback_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : etcd

### Configuration de kubectl
{: #ts-fsdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-fsdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep feedback)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f               2/2       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **2/2**.  Nous utiliserons `ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f aios-feedback
      ```

      Dans la mesure où ce pod dispose de 3 conteneurs, aios-feedback, ml-gateway-sidecar et check-etcd-ready, vous devez également vérifier dans le journal de ml-gateway-sidecar et check-etcd-ready si aios-feedback ne rencontre pas un problème :

      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-feedback-75d466f5d8-hxx9f ml-gateway-sidecar
      ```

      En général, les journaux doivent expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations des journaux.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service de reconnaissance de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosdiscdown}

### Présentation
{: #ts-dsdov}

- Situation : ai-open-scale-ibm-aios-ml-gateway-discovery_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : N/A

### Configuration de kubectl
{: #ts-dsdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Option 2 : Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-dsdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep ml-gateway-discovery)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt   1/1       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-ml-gateway-discovery-5d8c5db99b-qjxgt
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service nginx de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosnginxdown}

### Présentation
{: #ts-nsdov}

- Situation : ai-open-scale-ibm-aios-nginx_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : N/A

### Configuration de kubectl
{: #ts-nsdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-nsdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep nginx)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5                 1/1       Running   0          4h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-nginx-7d7695c447-5t2r5
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service d'API de journalisation de contenu de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiospayloadapidown}

### Présentation
{: #ts-pladov}

- Situation : ai-open-scale-ibm-aios-payload-logging-api_micro_service_is_down:
- Impact client : les clients ne peuvent pas écrire de contenu dans notre service à partir de services externes (Azur, Amazon, etc.) et, par conséquent, n'ont pas de données à analyser.
- Système de surveillance :
- Dépendances : IBM Event Stream

### Configuration de kubectl
{: #ts-pladkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-pladvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging-api)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65    1/1       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o <format>. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-api-744888549d-qvz65
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service de journalisation de contenu de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiospayloaddown}

### Présentation
{: #ts-plsdov}

- Situation : ai-open-scale-ibm-aios-payload-logging_micro_service_is_down:
- Impact client : les clients ne peuvent pas écrire de contenu dans notre service à partir de services externes (Azur, Amazon, etc.) et, par conséquent, n'ont pas de données à analyser.
- Système de surveillance :
- Dépendances : IBM Event Stream

### Configuration de kubectl
{: #ts-plsdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host`}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-plsdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep payload-logging)
    ```
    ```bash
    $ kubectl get pod -n aiopenscale | (head -n 1; grep payload-logging)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8        1/1       Running   1          6h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o <format>. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-payload-logging-865d488bfc-nqmz8
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service de planification de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosscheddown}

### Présentation
{: #ts-ssdov}

- Situation : ai-open-scale-ibm-aios-scheduling_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : N/A

### Configuration de kubectl
{: #ts-ssdkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}`:8443
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-ssdvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

    ```bash
    kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    ```

    ```bash
    $ kubectl -n aiopenscale get pods | (head -n 1; grep scheduling)
    NAME                                                           READY     STATUS    RESTARTS   AGE
    ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww            1/1       Running   0          2h
    ```

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous ai-open-scale-ibm-aios-scheduling-78b9965bf4-jrwww
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service redis de {{site.data.keyword.aios_short}} est indisponible
{: #ts-aiosredisdown}

### Présentation
{: #ts-redov}

- Situation : ai-open-scale-ibm-aios-redis_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : N/A

### Configuration de kubectl
{: #ts-redkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-redvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

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

    Vérifiez que le statut est **En cours d'exécution** et qu'il est entièrement prêt **1/1**.  Nous utiliserons `aios-redis-server-6f4c55fd75-nlrr4` comme pod pour les exemples suivants.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod aios-redis-server-6f4c55fd75-nlrr4
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o <format>. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs aios-redis-server-6f4c55fd75-nlrr4
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous aios-redis-server-6f4c55fd75-nlrr4
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Le service etcd est indisponible
{: #ts-etcddown}

### Présentation
{: #ts-etcov}

- Situation : etcd_micro_service_is_down:
- Impact client : les clients ne peuvent pas utiliser les fonctionnalités telles que la configuration de nouvelles instances, l'analyse des demandes, le stockage de contenu, etc.
- Système de surveillance :
- Dépendances : aucune

### Configuration de kubectl
{: #ts-etckc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n aiopenscale
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n aiopenscale
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Etapes de vérification/reprise
{: #ts-etcvr}

1.  Vérifiez le statut du pod en exécutant les commandes suivantes :

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

    Vérifiez qu'il existe trois pods d'etcd, que leur état est **En cours d'exécution**et qu'ils sont entièrement prêts **1/1**.

1.  Décrivez le pod s'il n'est pas en cours d'exécution :

    ```bash
    kubectl -n aiopenscale describe pod etcd-0
    kubectl -n aiopenscale describe pod etcd-1
    kubectl -n aiopenscale describe pod etcd-2
    ```

    Cette commande affiche les caractéristiques du pod.  Elle indique également les erreurs si votre pod n'est pas en cours d'exécution.  Votre pod peut rencontrer les cas suivants lorsqu'il n'est pas en cours d'exécution :

    - **Mon pod reste en attente**

      Si le pod reste **en attente**, cela signifie qu'il ne peut pas être planifié sur un noeud.  Cela est généralement dû à une insuffisance de ressource d'un type ou d'un autre qui empêche la planification.  Exécutez la commande précédente pour obtenir plus d'information. Le planificateur devrait émettre des messages sur la raison pour laquelle il ne peut pas planifier votre pod. Vous avez peut-être épuisé la quantité d'UC ou l'espace mémoire dans votre cluster. Dans ce cas, vous pouvez essayer plusieurs choses :

      - Ajoutez d'autres noeuds au cluster.

      - Mettez fin aux pods non nécessaires pour faire de la place pour les pods en attente.
      ```bash
      kubectl -n [namespace] delete pod [pod name]
      ```

      - Vérifiez que le pod n'est pas plus grand que vos noeuds. Par exemple, si tous les noeuds ont une capacité d'UC de 1, un pod demandant une capacité d'UC de 1.1 ne sera jamais planifié.

      Vous pouvez vérifier les capacités de noeud à l'aide de la commande kubectl get nodes -o `<format>`. Voici quelques exemples de lignes de commande permettant d'extraire uniquement les informations nécessaires :
      ```bash
      kubectl get nodes -o yaml | grep '\sname\|cpu\|memory'
      kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, cap: .status.capacity}'
      ```

    - **Mon pod reste en attente**

      Si un pod est bloqué à l'état **En attente**, cela signifie qu'il a été planifié sur un noeud worker et qu'il ne peut pas s'exécuter sur cette machine. Une fois encore, les informations issues de kubectl devraient être informatives. La cause la plus courante de pods à l'état **En attente** est l'impossibilité d'extraire l'image. Il y a trois choses à vérifier :

      - Vérifiez que le nom de l'image est correct.
      - Avez-vous inséré l'image dans le référentiel ?
      - Exécutez une commande `docker pull` manuelle pour extraire l'image sur votre cluster afin de voir si l'image peut être extraite.

    - **Mon pod se plante ou est dans un mauvais état**

      Tout d'abord, consultez les journaux du conteneur actuel :
      ```bash
      kubectl -n aiopenscale logs etcd-0
      kubectl -n aiopenscale logs etcd-1
      kubectl -n aiopenscale logs etcd-2
      ```

      Si votre conteneur s'est précédemment planté, vous pouvez accéder au journal des plantages à l'aide de la commande suivante :
      ```bash
      kubectl -n aiopenscale logs --previous etcd-0
      kubectl -n aiopenscale logs --previous etcd-1
      kubectl -n aiopenscale logs --previous etcd-2
      ```

      En général, le journal doit expliquer pourquoi le pod n'a pas démarré.  Corrigez le problème en fonction des informations du journal.  Si aucune de ces méthodes ne fonctionne, passez à l'étape d'escalade.

---

## Création d'un tableau de bord avec event_stream
{: #ts-createdashes}

### Présentation
{: #ts-dshov}

- Ce document explique comment créer un tableau de bord pour surveiller les services {{site.data.keyword.aios_full}}.

### Configuration de kubectl
{: #ts-dshkc}

Il existe deux façons de configurer le client kubectl.

1.  Utilisation de l'outil cloudctl

    Si cloudctl n'est pas disponible sur votre ordinateur portable, exécutez la commande suivante pour configurer kubectl :
    ```bash
    cloudctl login -u ${username} -p ${password} --skip-ssl-validation -c id-mycluster-account -a `https://${ICP Host}:8443` -n es
    ```
    Remplacez `${username}`,  `${password}`, `${ICP Host}` par une valeur réelle.  Par exemple :
    ```bash
    cloudctl login -u admin -p admin --skip-ssl-validation -c id-mycluster-account -a https://9.30.123.169:8443 -n es
    ```

1.  Utilisation de la configuration kubectl depuis la console {{site.data.keyword.icpfull}}
    - Connectez-vous à votre cluster {{site.data.keyword.icpfull}} `https://${Hôte ICP}:8443`
    - Sélectionnez l'icône **personne dans un rond** > **Configurer le client**
    - Cliquez sur l'icône **Copier dans le presse-papiers** pour copier les informations de configuration dans le presse-papiers
    - Remplacez l'espace de nom `aiopenscale` par `es` si nécessaire.
    - Collez les informations de configuration sur votre ligne de commande, puis appuyez sur **Entrée**.

### Affichage du flux d'événements
{: #ts-dshve}

Le flux d'événements comprend plusieurs services.  Pour plus de détails sur chaque service, consultez le sous-dossier correspondant.

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

## Utilisation de la surveillance de {{site.data.keyword.aios_short}}
{: #ts-aiosusemonitor}

### Présentation
{: #ts-omov}

- Ce document explique comment créer un tableau de bord pour surveiller les services {{site.data.keyword.aios_full}}.

### Configuration du tableau de bord
{: #ts-omsd}

- Extrayez le fichier aios-dashboard.json d'ibm-aiopenscale-x86_64-1.0.0.tar.gz.  Ce fichier se trouve dans le répertoire `utils`.
- Connectez-vous à votre cluster ICP `https://${Hôte ICP}:8443`
- Sélectionnez `Menu` > `Plateforme` > `Surveillance`
- Cliquez sur l'icône `Accueil`
- Cliquez sur l'option de menu `Importer le tableau de bord`
- Cliquez sur le bouton `Télécharger le fichier .json` et pointez vers votre aios-dashboard.json
- Sélectionnez `prometheus` pour la zone d'entrée prometheus

### Affichage du tableau de bord
{: #ts-omvd}

Le tableau de bord est constitué des lignes suivantes :

- Utilisation totale du cluster

  Cette ligne affiche le niveau d'utilisation de l'UC à l'échelle du cluster, ainsi que le niveau d'utilisation de la mémoire et du système de fichiers. Les compteurs vous indiquent si votre cluster est en bonne santé. S'ils indiquent une mauvaise santé, ajoutez des noeuds au cluster ou arrêtez des pods inutiles pour faire de la place pour d'autres déploiements.

- Disponibilité par service

  Cette ligne indique la disponibilité de chaque service.  Les panneaux initiaux indiquent le nombre total de conteneurs prêts.  Si le compteur indique 100 %, cela signifie que votre instance de {{site.data.keyword.aios_short}} est en bonne santé.  Dans le cas contraire, vous pouvez examiner le tableau afin de déterminer quel sevice est arrêté et le mettre en fonctionnement.  Il y a d'autres runbooks {{site.data.keyword.aios_short}} qui aident à déterminer pourquoi un conteneur n'est pas correctement démarré.  Après les panneaux initiaux viennent les panneaux des différents services. Différentes lignes indiquent le nombre de conteneurs prêts et demandés.

- UC par service

  Cette ligne indique l'utilisation de l'UC pour chaque service
et elle inclut le nombre de coeurs d'UC utilisés par chaque conteneur et le maximum qu'il peut utiliser.  Si ces valeurs sont trop proches, déterminez pourquoi le conteneur consomme trop de ressource UC.  Si nécessaire, vous pouvez augmenter la limite d'UC pour le conteneur en éditant le déploiement et en modifiant la limite d'UC :
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Exemple :
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Espace mémoire par service

  Cette ligne indique l'utilisation de mémoire pour chaque service
et elle inclut la mémoire utilisée par chaque conteneur et le maximum qu'il peut utiliser.  Si ces valeurs sont trop proches, déterminez pourquoi le conteneur consomme trop de mémoire.  Si nécessaire, vous pouvez augmenter la mémoire pour le conteneur en éditant le déploiement et en modifiant la limite de mémoire :
  ```bash
  kubectl -n aiopenscale edit deployment ${deployment name}
  ```

  Exemple :
  ```bash
  kubectl -n aiopenscale edit deployment ai-open-scale-ibm-aios-bias
  ```

- Système de fichiers par service

  Cette ligne indique le niveau d'utilisation du système de fichiers pour chaque service.  Si le moniteur indique une utilisation du système de fichiers en constante augmentation,
inspectez le conteneur pour déterminer pourquoi l'utilisation ne cesse d'augmenter.  Au besoin, vous pouvez contacter le canal Slack précédent pour plus d'assistance.

- Images et versions

  Cette ligne affiche la liste de toutes les images et versions utilisées pour {{site.data.keyword.aios_full}}.
