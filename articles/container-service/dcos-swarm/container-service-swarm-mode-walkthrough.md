---
title: aaaQuickstart - klastra Azure Docker CE dla systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiesz toocreate klastrze Docker CE dla systemu Linux kontenerów w usłudze kontenera platformy Azure z hello wiersza polecenia platformy Azure."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, Docker, Swarm
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 6c26c12ed085ec379c3486095a5fa51379afc5a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-ce-cluster"></a>Wdrażanie klastra Docker CE

W tym szybki start klastrze Docker CE jest wdrażane za pomocą hello wiersza polecenia platformy Azure. Następnie wdrożone i uruchomić w klastrze hello aplikacji kontenera wielu składające się z frontonu sieci web oraz wystąpienia pamięci podręcznej Redis. Po ukończeniu aplikacji hello jest dostępny za pośrednictwem hello internet.

Tryb Docker CE w usłudze Azure Container Service jest w wersji zapoznawczej i **nie powinien być używany w przypadku obciążeń produkcyjnych**.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi.

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *ukwest* lokalizacji.

```azurecli-interactive
az group create --name myResourceGroup --location ukwest
```

Dane wyjściowe:

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westcentralus",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-docker-swarm-cluster"></a>Tworzenie klastra Docker Swarm

Utwórz klaster Docker CE usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia. 

Witaj poniższym przykładzie jest tworzony klaster o nazwie *mySwarmCluster* z systemem Linux jednego głównego węzła i trzech węzłów agenta systemu Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type dockerce --resource-group myResourceGroup --generate-ssh-keys
```

Po kilku minutach polecenia hello kończy i zwraca informacje o formacie json o hello klastra.

## <a name="connect-toohello-cluster"></a>Połącz toohello klastra

W tym szybki start należy hello nazwę FQDN główny Docker Swarm hello oraz hello Docker agenta puli. Uruchom następujące polecenie tooreturn hello zarówno hello master i agenta nazwy FQDN.


```bash
az acs list --resource-group myResourceGroup --query '[*].{Master:masterProfile.fqdn,Agent:agentPoolProfiles[0].fqdn}' -o table
```

Dane wyjściowe:

```bash
Master                                                               Agent
-------------------------------------------------------------------  --------------------------------------------------------------------
myswarmcluster-myresourcegroup-d5b9d4mgmt.ukwest.cloudapp.azure.com  myswarmcluster-myresourcegroup-d5b9d4agent.ukwest.cloudapp.azure.com
```

Utwórz wzorzec Swarm toohello tunelu SSH. Zastąp `MasterFQDN` adres FQDN hello hello Swarm wzorca.

```bash
ssh -p 2200 -fNL localhost:2374:/var/run/docker.sock azureuser@MasterFQDN
```

Zestaw hello `DOCKER_HOST` zmiennej środowiskowej. Dzięki temu można polecenia docker toorun przed hello Docker Swarm bez nazwy hello toospecify hello hosta.

```bash
export DOCKER_HOST=localhost:2374
```

Wszystko jest teraz gotowy toorun usługi Docker na powitania Docker Swarm.


## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Utwórz plik o nazwie `azure-vote.yaml` i hello kopiowania zawartości do niego.


```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Uruchom hello [wdrażanie stosu docker](https://docs.docker.com/engine/reference/commandline/stack_deploy/) polecenia toocreate hello Azure głos usługi.

```bash
docker stack deploy azure-vote --compose-file azure-vote.yaml
```

Dane wyjściowe:

```bash
Creating network azure-vote_default
Creating service azure-vote_azure-vote-back
Creating service azure-vote_azure-vote-front
```

Użyj hello [docker stosu ps](https://docs.docker.com/engine/reference/commandline/stack_ps/) polecenia tooreturn hello stan wdrożenia aplikacji hello.

```bash
docker stack ps azure-vote
```

Raz hello `CURRENT STATE` poszczególnych usług jest `Running`, aplikacja hello jest gotowa.

```bash
ID                  NAME                            IMAGE                                 NODE                               DESIRED STATE       CURRENT STATE                ERROR               PORTS
tnklkv3ogu3i        azure-vote_azure-vote-front.1   microsoft/azure-vote-front:redis-v1   swarmm-agentpool0-66066781000004   Running             Running 5 seconds ago                            
lg99i4hy68r9        azure-vote_azure-vote-back.1    redis:latest                          swarmm-agentpool0-66066781000002   Running             Running about a minute ago
```

## <a name="test-hello-application"></a>Testowanie aplikacji hello

Przeglądaj toohello FQDN hello Swarm agenta puli tootest limit hello Azure głos aplikacji.

![Obraz przeglądania tooAzure głosu](media/container-service-docker-swarm-mode-walkthrough/azure-vote.png)

## <a name="delete-cluster"></a>Usuwanie klastra
Gdy hello klastra nie jest już potrzebne, można użyć hello [az grupę Usuń](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove, usługi kontenera i wszystkich powiązanych zasobów.

```azurecli-interactive
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a>Pobierz kod hello

W tym szybki start kontenera wstępnie utworzony obrazy zostały używane toocreate usługi Docker. Witaj związane z kodu aplikacji, plik Dockerfile, i tworzenia plików są dostępne w serwisie GitHub.

[https://github.com/Azure-Samples/azure-voting-app-redis](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a>Następne kroki

W tym szybki start wdrożyć klaster Docker Swarm i wdrożone tooit wielu kontenera aplikacji.

toolearn temat integracji Docker ciepłych z Visual Studio Team Services, nadal toohello CI/CD z Docker Swarm i VSTS.

> [!div class="nextstepaction"]
> [Ciągła integracja/ciągłe dostarczanie z usługami Swarm i VSTS](./container-service-docker-swarm-setup-ci-cd.md)