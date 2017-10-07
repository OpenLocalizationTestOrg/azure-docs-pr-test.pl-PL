---
title: "aaaJenkins CI/CD z Kubernetes usługi kontenera platformy Azure | Dokumentacja firmy Microsoft"
description: "Sposobu tooautomate CI/CD procesu z Wpięć toodeploy i uaktualniania konteneryzowanych aplikacji na Kubernetes usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: chzbrgr71
manager: johny
editor: 
tags: acs, azure-container-service, jenkins
keywords: "Rozwiązanie docker kontenerów, Kubernetes, Azure, Wpięć"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: briar
ms.custom: mvc
ms.openlocfilehash: e00e13bf06619bed73e82878777e55458ea3dd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="jenkins-integration-with-azure-container-service-and-kubernetes"></a>Wpięć integracji z usługą kontenera Azure i Kubernetes 
W tym samouczku będziemy przeprowadzenie tooset procesu hello zapasowej ciągłej integracji aplikacji kontenera wielu do Kubernetes usługi kontenera platformy Azure przy użyciu platformy Wpięć hello. przepływ pracy Hello aktualizacji hello kontener obrazu w Centrum Docker i uaktualnień stanowiskami Kubernetes hello przy użyciu wdrażania. 

## <a name="high-level-process"></a>Wysokiego poziomu ładowania
podstawowe kroki Hello szczegółowo opisane w tym artykule przedstawiono: 
- Zainstaluj Kubernetes klaster usługi kontenera
- Konfigurowanie Wpięć i konfigurowanie tooContainer dostępu usługi
- Tworzenie przepływów pracy Wpięć
- Testowanie tooend zakończenia procesu CI/CD hello

## <a name="install-a-kubernetes-cluster"></a>Zainstaluj klaster Kubernetes
    
Wdrażanie hello Kubernetes klastra usługi kontenera platformy Azure przy użyciu hello następujące kroki. Pełną dokumentację znajduje się [tutaj](container-service-kubernetes-walkthrough.md).

### <a name="step-1-create-a-resource-group"></a>Krok 1: Tworzenie grupy zasobów
```azurecli
RESOURCE_GROUP=my-resource-group
LOCATION=westus

az group create --name=$RESOURCE_GROUP --location=$LOCATION
```

### <a name="step-2-deploy-hello-cluster"></a>Krok 2: Wdrażanie klastra hello
> [!NOTE]
> Witaj poniższe czynności wymagają lokalnych klucz publiczny SSH, przechowywane w folderze ~/.ssh hello.
>

```azurecli
RESOURCE_GROUP=my-resource-group
DNS_PREFIX=some-unique-value
CLUSTER_NAME=any-acs-cluster-name

az acs create \
--orchestrator-type=kubernetes \
--resource-group $RESOURCE_GROUP \
--name=$CLUSTER_NAME \
--dns-prefix=$DNS_PREFIX \
--ssh-key-value ~/.ssh/id_rsa.pub \
--admin-username=azureuser \
--master-count=1 \
--agent-count=5 \
--agent-vm-size=Standard_D1_v2
```

## <a name="set-up-jenkins-and-configure-access-toocontainer-service"></a>Konfigurowanie Wpięć i konfigurowanie tooContainer dostępu usługi

### <a name="step-1-install-jenkins"></a>Krok 1: Instalowanie Wpięć
1. Tworzenie maszyny Wirtualnej platformy Azure z Ubuntu 16.04 LTS.  Ponieważ w dalszej części hello kroków będzie konieczne tooconnect toothis maszynę Wirtualną przy użyciu bash na komputerze lokalnym, a klucz publiczny zestawu hello "Typ uwierzytelniania" too'SSH "i Wklej hello klucz publiczny SSH jest przechowywany lokalnie w folderze ~/.ssh.  Ponadto pod uwagę hello 'Nazwa użytkownika', że możesz określić, ponieważ ta nazwa użytkownika będzie pulpitu nawigacyjnego Wpięć hello tooview potrzebne i łączenia toohello Wpięć maszyny Wirtualnej w kolejnych krokach.
2. Zainstaluj Wpięć za pośrednictwem tych [instrukcje](https://wiki.jenkins-ci.org/display/JENKINS/Installing+Jenkins+on+Ubuntu). Bardziej szczegółowy samouczek jest przeznaczony na [howtoforge.com](https://www.howtoforge.com/tutorial/how-to-install-jenkins-with-apache-on-ubuntu-16-04).
3. tooview hello pulpitu nawigacyjnego Wpięć na komputerze lokalnym, zaktualizuj hello sieć platformy Azure zabezpieczeń grupy tooallow portu 8080, dodając regułę ruchu przychodzącego, który umożliwia dostęp tooport 8080.  Alternatywnie mogą instalacji przekierowania portów, uruchamiając poniższe polecenie:`ssh -i ~/.ssh/id_rsa -L 8080:localhost:8080 <your_jenkins_user>@<your_jenkins_public_ip`
4. Połącz przy użyciu przeglądarki hello przechodząc toohello publiczny adres IP serwera Wpięć tooyour (http:// < your_jenkins_public_ip >: 8080) i odblokować hello Wpięć, odwiedź pulpit nawigacyjny hello o hasło administratora początkowej powitania po raz pierwszy.  hasło administratora Hello są przechowywane w /var/lib/jenkins/secrets/initialAdminPassword na powitania Wpięć maszyny Wirtualnej.  Tooget łatwo to hasło jest tooSSH do hello wirtualna Wpięć: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Następnie uruchom: `sudo cat /var/lib/jenkins/secrets/initialAdminPassword`.
5. Zainstaluj Docker na maszynie Wpięć hello za pośrednictwem tych [instrukcje](https://docs.docker.com/cs-engine/1.13/#install-on-ubuntu-1404-lts-or-1604-lts). Umożliwia to uruchamianie zadań Wpięć toobe polecenia Docker.
6. Skonfiguruj Docker uprawnienia tooallow Wpięć tooaccess hello Docker punktu końcowego.

    ```bash
    sudo chmod 777 /run/docker.sock
    ```
8. Zainstaluj `kubectl` CLI na Wpięć. Szczegółowe informacje są w [Instalowanie i konfigurowanie kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).  Zadania Wpięć będzie używać toomanage "kubectl" i wdróż toohello Kubernetes klastra.

    ```bash
    curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl

    chmod +x ./kubectl

    sudo mv ./kubectl /usr/local/bin/kubectl
    ```

### <a name="step-2-set-up-access-toohello-kubernetes-cluster"></a>Krok 2: Konfigurowanie klastra Kubernetes toohello dostępu

> [!NOTE]
> Istnieje wiele metod tooaccomplishing hello następujące kroki. Podejście hello Użyj najłatwiej dla Ciebie.
>

1. Kopiuj hello `kubectl` Wpięć komputera tak, aby zadania Wpięć mają dostęp toohello Kubernetes klastra toohello pliku konfiguracji. W poniższych instrukcjach przyjęto, że używasz bash z innego komputera niż hello Wpięć maszyny Wirtualnej i że lokalny klucz publiczny SSH jest przechowywany w folderze ~/.ssh hello maszyny.

```bash
export KUBE_MASTER=<your_cluster_master_fqdn>
export JENKINS_USER=<your_jenkins_user>
export JENKINS_SERVER=<your_jenkins_public_ip>
sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir -m 777 /home/$JENKINS_USER/.kube/ \
&& sudo ssh $JENKINS_USER@$JENKINS_SERVER sudo mkdir /var/lib/jenkins/.kube/ \
&& sudo scp -3 -i ~/.ssh/id_rsa azureuser@$KUBE_MASTER:.kube/config $JENKINS_USER@$JENKINS_SERVER:~/.kube/config \
&& sudo ssh -i ~/.ssh/id_rsa $JENKINS_USER@$JENKINS_SERVER sudo cp /home/$JENKINS_USER/.kube/config /var/lib/jenkins/.kube/config \
```
        
2. Sprawdzanie poprawności z Wpięć tego hello Kubernetes klastra jest dostępny.  toodo tego SSH do hello wirtualna Wpięć: `ssh <your_jenkins_user>@<your_jenkins_public_ip>`.  Następnie sprawdź połączenia klastra tooyour Wpięć: `kubectl cluster-info`.
    

## <a name="create-a-jenkins-workflow"></a>Tworzenie przepływów pracy Wpięć

### <a name="prerequisites"></a>Wymagania wstępne

- Konto usługi GitHub repozytorium kodu.
- Centrum konta toostore i aktualizacji obrazy usługi docker.
- Konteneryzowanych aplikacja, która może być ponownie skompilowany i zaktualizować. Można użyć tej przykładowej aplikacji kontenera napisana Golang: https://github.com/chzbrgr71/go-web 

> [!NOTE]
> Witaj poniższe kroki należy wykonać na koncie usługi GitHub. Hello wolnego tooclone powyżej repozytorium, możesz, ale należy użyć własnych elementów webhook hello tooconfigure konta i Wpięć dostępu.
>

### <a name="step-1-deploy-initial-v1-of-application"></a>Krok 1: Wdrażanie początkowej v1 aplikacji
1. Tworzenie aplikacji hello z hello developer maszyny z hello następujące polecenia. Zastąp `myrepo` własnymi.
    
    ```bash
    git clone https://github.com/chzbrgr71/go-web.git
    cd go-web
    docker build -t myrepo/go-web .
    ```

2. Wypchnij tooDocker obrazu koncentratora.

    ```bash
    docker login
    docker push myrepo/go-web
    ```

3. Wdrażanie klastra Kubernetes toohello.
    
    > [!NOTE] 
    > Edytuj hello `go-web.yaml` pliku tooupdate Twojego obraz kontenera i repozytorium.
    >
        
    ```bash
    kubectl create -f ./go-web.yaml --record
    ```
### <a name="step-2-configure-jenkins-system"></a>Krok 2: Konfigurowanie Wpięć systemu
1. Kliknij przycisk **Zarządzanie Wpięć** > **skonfigurować System**.
2. W obszarze **GitHub**, wybierz pozycję **Dodaj serwer GitHub**.
3. Pozostaw **adres URL interfejsu API** jako domyślny.
4. W obszarze **poświadczenia**, Dodaj poświadczenie Wpięć przy użyciu **tajny tekstu**. Firma Microsoft zaleca używanie GitHub osobiste tokeny dostępu, które są konfigurowane w ustawieniach konta użytkownika usługi GitHub. Więcej informacji na ten [tutaj.](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
5. Kliknij przycisk **połączenie testowe** tooensure to jest poprawnie skonfigurowany.
6. W obszarze **globalnych właściwości**, dodać zmienną środowiskową `DOCKER_HUB` i podaj hasło do Centrum Docker. (Jest to przydatne w przypadku tego pokazu, ale scenariuszu produkcyjnym wymagają bardziej bezpieczną metodą).
7. Zapisz.

![GitHub Wpięć dostępu](./media/container-service-kubernetes-jenkins/jenkins-github-access.png)

### <a name="step-3-create-hello-jenkins-workflow"></a>Krok 3: Tworzenie przepływu pracy Wpięć hello
1. Utwórz element Wpięć.
2. Podaj nazwę (na przykład "Przejdź sieci web") i wybierz **projektu dowolne**. 
3. Sprawdź **projektu GitHub** i podaj repozytorium GitHub tooyour adres URL hello.
4. W **zarządzania kodem źródłowym**, podaj adres URL repozytorium GitHub hello i poświadczenia. 
5. Dodaj **krok kompilacji** typu **wykonywania powłoki** i hello Użyj następującego tekstu:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    docker build -t $WEB_IMAGE_NAME .
    docker login -u <your-dockerhub-username> -p ${DOCKER_HUB}
    docker push $WEB_IMAGE_NAME
    ```

6. Dodaj inny **krok kompilacji** typu **wykonywania powłoki** i hello Użyj następującego tekstu:

    ```bash
    WEB_IMAGE_NAME="myrepo/go-web:kube${BUILD_NUMBER}"
    kubectl set image deployment/go-web go-web=$WEB_IMAGE_NAME --kubeconfig /var/lib/jenkins/config
    ```

![Kroki procesu kompilacji Wpięć](./media/container-service-kubernetes-jenkins/jenkins-build-steps.png)
    
7. Zapisz element Wpięć hello i testowania **kompilacji teraz**.

### <a name="step-4-connect-github-webhook"></a>Krok 4: Łączenie element webhook GitHub
1. W elemencie Wpięć hello został utworzony, kliknij przycisk **Konfiguruj**.
2. W obszarze **kompilacji wyzwalaczy**, wybierz pozycję **wyzwalacza haku GitHub dla sondowania GITScm** i **zapisać**. Spowoduje to automatyczne skonfigurowanie hello element webhook GitHub.
3. W Twojej repozytorium GitHub dla go w sieci web, kliknij przycisk **Ustawienia > elementów Webhook**.
4. Upewnij się, że hello webhook Wpięć, który został pomyślnie dodany adres URL. adres URL Hello powinien kończyć się "element webhook github".

![Konfiguracja elementu webhook Wpięć](./media/container-service-kubernetes-jenkins/jenkins-webhook.png)

## <a name="test-hello-cicd-process-end-tooend"></a>Testowanie tooend zakończenia procesu CI/CD hello

1. Zaktualizuj kod dla repozytorium hello i wypychania/synchronizacji z repozytorium GitHub hello.
2. Za pomocą konsoli Wpięć hello, sprawdź hello **kompilacji historii** i zweryfikować tego hello zadanie zostało uruchomione. Wyświetl szczegóły toosee danych wyjściowych konsoli.
3. Z Kubernetes Wyświetl szczegóły hello uaktualnić wdrożenia:

    ```bash
    kubectl rollout history deployment/go-web
    ```

## <a name="next-steps"></a>Następne kroki

- Wdróż rejestru kontenera Azure i przechowywania w bezpiecznym repozytorium obrazów. Zobacz [docs rejestru kontenera Azure](https://docs.microsoft.com/azure/container-registry).
- Tworzyć bardziej złożone przepływu pracy, który obejmuje side-by-side wdrożenia oraz testów automatycznych w Wpięć.
- Aby uzyskać więcej informacji na temat CI/CD z Wpięć i Kubernetes, zobacz hello [blog Wpięć](https://jenkins.io/blog/2015/07/24/integrating-kubernetes-and-jenkins/).
