---
title: "Samouczek usługi kontenera aaaAzure — Zarządzanie DC/OS | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — Zarządzanie DC/OS"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b91c433bfd7e48ec405cc62be1486d9d4662839d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-container-service-tutorial---manage-dcos"></a>Samouczek usługi kontenera platformy Azure — Zarządzanie DC/OS

DC/OS przewiduje uruchamianie nowoczesnych i konteneryzowanych aplikacji rozproszonej platformy. Z usługi kontenera platformy Azure inicjowania obsługi klastra DC/OS gotowy produkcji jest proste i szybkie. To szybki start szczegóły podstawowe kroki potrzebne toodeploy klastra DC/OS i wykonywania podstawowych obciążenia.

> [!div class="checklist"]
> * Tworzenie klastra usługi ACS DC/OS
> * Połącz toohello klastra
> * Zainstaluj interfejs wiersza polecenia DC/OS hello
> * Wdrażanie klastra toohello aplikacji
> * Skalowanie aplikacji w klastrze hello
> * Skalowanie węzłów klastra DC/OS hello
> * Podstawowe możliwości zarządzania DC/OS
> * Usuń klaster DC/OS hello

Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-dcos-cluster"></a>Tworzenie klastra DC/OS

Najpierw utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westeurope* lokalizacji.

```azurecli
az group create --name myResourceGroup --location westeurope
```

Następnie Utwórz klaster DC/OS z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.

Witaj poniższy przykład tworzy klaster DC/OS o nazwie *myDCOSCluster* i tworzy kluczy SSH, jeśli jeszcze nie istnieje. toouse określonego zestawu kluczy, należy użyć hello `--ssh-key-value` opcji.  

```azurecli
az acs create \
  --orchestrator-type dcos \
  --resource-group myResourceGroup \
  --name myDCOSCluster \
  --generate-ssh-keys
```

Po kilku minutach polecenia hello kończy i zwraca informacje na temat wdrażania hello.

## <a name="connect-toodcos-cluster"></a>Połącz klaster tooDC/OS

Po utworzeniu klastra DC/OS, może być dostęp za pośrednictwem tunelu SSH. Uruchom następujące polecenia tooreturn hello publicznego adresu IP wzorca DC/OS hello hello. Ten adres IP jest przechowywana w zmiennej i używane w hello następnego kroku.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

toocreate hello tunelu SSH, uruchom następujące polecenie hello i hello wyświetlanymi instrukcjami. Jeśli port 80 jest już w użyciu, hello polecenie kończy się niepowodzeniem. Aktualizacja hello tunelowane tooone portu nieużywany, takich jak `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

## <a name="install-dcos-cli"></a>Instalowanie interfejsu wiersza polecenia DC/OS

Zainstaluj interfejs wiersza polecenia hello DC/OS jest przy użyciu hello [az dcos acs install-cli](/azure/acs/dcos#install-cli) polecenia. Jeśli używasz usługi Azure CloudShell hello interfejsu wiersza polecenia DC/OS jest już zainstalowana. Jeśli używasz hello Azure CLI macOS lub Linux, może być konieczne toorun hello polecenie sudo.

```azurecli
az acs dcos install-cli
```

Przed hello interfejsu wiersza polecenia można używać z klastrem hello musi ona być tunelu SSH hello toouse skonfigurowany. toodo tak, uruchom hello następujące polecenia, dostosowywania hello portu, jeśli to konieczne.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Uruchamianie aplikacji

Domyślnie Hello planowania mechanizm dla klastra usługi ACS DC/OS jest Marathon. Marathon jest toostart używanych aplikacji i zarządzanie stanem hello aplikacji hello w klastrze DC/OS hello. tooschedule aplikacji za pośrednictwem platformy Marathon, Utwórz plik o nazwie **marathon app.json**, i hello kopiowania zawartości do niego. 

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Uruchom następujące polecenie tooschedule hello aplikacji toorun w klastrze DC/OS hello hello.

```azurecli
dcos marathon app add marathon-app.json
```

toosee hello stan wdrożenia dla aplikacji hello, uruchom następujące polecenie hello.

```azurecli
dcos marathon app list
```

Gdy hello **zadania** zmienia wartość kolumny z *0/1* za*1/1*, wdrażanie aplikacji zostało zakończone.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     0/1    ---       ---      False      DOCKER   None
```

## <a name="scale-marathon-application"></a>Skalowanie aplikacji platformy Marathon

W poprzednim przykładzie hello została utworzona aplikacja pojedynczego wystąpienia. To wdrożenie, aby trzy wystąpienia aplikacji hello są dostępne, otwarcie hello tooupdate **marathon app.json** pliku, a następnie zaktualizuj hello wystąpienia właściwości too3.

```json
{
  "id": "demo-app-private",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 3,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  }
}
```

Aktualizowanie aplikacji hello przy użyciu hello `dcos marathon app update` polecenia.

```azurecli
dcos marathon app update demo-app-private < marathon-app.json
```

toosee hello stan wdrożenia dla aplikacji hello, uruchom następujące polecenie hello.

```azurecli
dcos marathon app list
```

Gdy hello **zadania** zmienia wartość kolumny z *1/3* za*3/1*, wdrażanie aplikacji zostało zakończone.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/3    ---       ---      False      DOCKER   None
```

## <a name="run-internet-accessible-app"></a>Uruchamianie aplikacji dostępny z Internetu

Witaj ACS DC/OS klaster składa się z dwóch zestawów węzła, jeden publiczny, który jest dostępny na hello internet i prywatnego, który nie jest dostępny na hello internet. Hello domyślny zestaw jest hello prywatnej węzłów, użytego w przykładzie ostatniego hello.

toomake aplikacji, które są dostępne na hello internet, wdrażania ich toohello zestaw węzłów publicznych. toodo tak, nadaj hello `acceptedResourceRoles` obiekt wartość `slave_public`.

Utwórz plik o nazwie **nginx public.json** i hello kopiowania zawartości do niego.

```json
{
  "id": "demo-app",
  "cmd": null,
  "cpus": 1,
  "mem": 32,
  "disk": 0,
  "instances": 1,
  "container": {
    "docker": {
      "image": "nginx",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ]
    },
    "type": "DOCKER"
  },
  "acceptedResourceRoles": [
    "slave_public"
  ]
}
```

Uruchom następujące polecenie tooschedule hello aplikacji toorun w klastrze DC/OS hello hello.

```azurecli 
dcos marathon app add nginx-public.json
```

Pobierz publiczny adres IP hello agentów publicznych klastra DC/OS hello.

```azurecli 
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Przeglądanie adres toothis zwraca hello domyślnej NGINX witryny.

![NGINX](./media/container-service-dcos-manage-tutorial/nginx.png)

## <a name="scale-dcos-cluster"></a>Skalowanie klastra DC/OS

W poprzednich przykładach hello aplikacji była skalowana toomultiple wystąpienia. Hello DC/OS infrastruktury można także skalowanie tooprovide więcej lub mniej wydajności obliczeniowej. Jest to zrobić za pomocą hello [skalować acs az]() polecenia. 

toosee hello bieżąca liczba agentów DC/OS, użyj hello [Pokaż acs az](/cli/azure/acs#show) polecenia.

```azurecli
az acs show --resource-group myResourceGroup --name myDCOSCluster --query "agentPoolProfiles[0].count"
```

tooincrease hello too5 liczby, użyj hello [skalować acs az](/cli/azure/acs#scale) polecenia. 

```azurecli
az acs scale --resource-group myResourceGroup --name myDCOSCluster --new-agent-count 5
```

## <a name="delete-dcos-cluster"></a>Usuń klaster DC/OS

Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove klastra DC/OS i wszystkie powiązane zasoby.

```azurecli 
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku uzyskanych o podstawowe zadania zarządzania DC/OS w tym następujących hello. 

> [!div class="checklist"]
> * Tworzenie klastra usługi ACS DC/OS
> * Połącz toohello klastra
> * Zainstaluj interfejs wiersza polecenia DC/OS hello
> * Wdrażanie klastra toohello aplikacji
> * Skalowanie aplikacji w klastrze hello
> * Skalowanie węzłów klastra DC/OS hello
> * Usuń klaster DC/OS hello

ADVANCE toohello następny samouczek toolearn o załadować równoważenia aplikacji w DC/OS na platformie Azure. 

> [!div class="nextstepaction"]
> [Równoważenie obciążenia aplikacji](container-service-load-balancing.md)