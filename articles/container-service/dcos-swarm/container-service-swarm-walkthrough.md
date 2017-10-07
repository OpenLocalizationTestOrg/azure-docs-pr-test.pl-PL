---
title: aaaQuickstart - Azure Docker Swarm klastra dla systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiesz toocreate klaster Docker Swarm dla systemu Linux kontenerów w usłudze kontenera platformy Azure z hello wiersza polecenia platformy Azure."
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
ms.date: 08/14/2017
ms.author: nepeters
ms.custom: 
ms.openlocfilehash: 3028d2d00585360ec163518bf98f69bb0dd44dec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-docker-swarm-cluster"></a>Wdrażanie klastra Docker Swarm

W tym szybki start klaster Docker Swarm jest wdrażane za pomocą hello wiersza polecenia platformy Azure. Następnie wdrożone i uruchomić w klastrze hello aplikacji kontenera wielu składające się z frontonu sieci web oraz wystąpienia pamięci podręcznej Redis. Po ukończeniu aplikacji hello jest dostępny za pośrednictwem hello internet.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

Ta opcja szybkiego startu wymaga, że używasz wersji interfejsu wiersza polecenia Azure hello 2.0.4 lub nowszym. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczna grupa przeznaczona do wdrażania zasobów platformy Azure i zarządzania nimi.

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westus* lokalizacji.

```azurecli-interactive
az group create --name myResourceGroup --location westus
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

Utwórz klaster Docker Swarm usługi kontenera platformy Azure z hello [az acs utworzyć](/cli/azure/acs#create) polecenia. 

Witaj poniższym przykładzie jest tworzony klaster o nazwie *mySwarmCluster* z systemem Linux jednego głównego węzła i trzech węzłów agenta systemu Linux.

```azurecli-interactive
az acs create --name mySwarmCluster --orchestrator-type Swarm --resource-group myResourceGroup --generate-ssh-keys
```

Po kilku minutach polecenia hello kończy i zwraca informacje o formacie json o hello klastra.

## <a name="connect-toohello-cluster"></a>Połącz toohello klastra

W tym szybki start należy adres IP hello główny Docker Swarm hello oraz hello Docker agenta puli. Uruchom następujące polecenie tooreturn hello oba adresy IP.


```bash
az network public-ip list --resource-group myResourceGroup --query '[*].{Name:name,IPAddress:ipAddress}' -o table
```

Dane wyjściowe:

```bash
Name                                                                 IPAddress
-------------------------------------------------------------------  -------------
swarmm-agent-ip-myswarmcluster-myresourcegroup-d5b9d4agent-66066781  52.179.23.131
swarmm-master-ip-myswarmcluster-myresourcegroup-d5b9d4mgmt-66066781  52.141.37.199
```

Utwórz wzorzec Swarm toohello tunelu SSH. Zastąp `IPAddress` o adresie IP hello hello Swarm wzorca.

```bash
ssh -p 2200 -fNL 2375:localhost:2375 azureuser@IPAddress
```

Zestaw hello `DOCKER_HOST` zmiennej środowiskowej. Dzięki temu można polecenia docker toorun przed hello Docker Swarm bez nazwy hello toospecify hello hosta.

```bash
export DOCKER_HOST=:2375
```

Wszystko jest teraz gotowy toorun usługi Docker na powitania Docker Swarm.


## <a name="run-hello-application"></a>Uruchamianie aplikacji hello

Utwórz plik o nazwie `docker-compose.yaml` i hello kopiowania zawartości do niego.

```yaml
version: '3'
services:
  azure-vote-back:
    image: redis
    container_name: azure-vote-back
    ports:
        - "6379:6379"

  azure-vote-front:
    image: microsoft/azure-vote-front:redis-v1
    container_name: azure-vote-front
    environment:
      REDIS: azure-vote-back
    ports:
        - "80:80"
```

Uruchom hello następujące polecenia toocreate hello Azure głos usługi.

```bash
docker-compose up -d
```

Dane wyjściowe:

```bash
Creating network "user_default" with hello default driver
Pulling azure-vote-front (microsoft/azure-vote-front:redis-v1)...
swarm-agent-EE873B23000005: Pulling microsoft/azure-vote-front:redis-v1...
swarm-agent-EE873B23000004: Pulling microsoft/azure-vote-front:redis-v1... : downloaded
Pulling azure-vote-back (redis:latest)...
swarm-agent-EE873B23000004: Pulling redis:latest... : downloaded
Creating azure-vote-front ... 
Creating azure-vote-back ... 
Creating azure-vote-front
Creating azure-vote-back ...
```

## <a name="test-hello-application"></a>Testowanie aplikacji hello

Przeglądaj adres IP toohello hello Swarm agenta puli tootest limit hello Azure głos aplikacji.

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