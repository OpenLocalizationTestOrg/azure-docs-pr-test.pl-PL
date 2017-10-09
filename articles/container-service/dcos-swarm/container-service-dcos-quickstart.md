---
title: "aaaAzure Szybki Start usługi kontenera - wdrożyć klaster DC/OS | Dokumentacja firmy Microsoft"
description: "Azure kontenera usługi Szybki Start — wdrażanie klastra DC/OS"
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
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b961f15bd73deeafda5a3fc25ab53c839195219b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Wdrażanie klastra DC/OS

DC/OS przewiduje uruchamianie nowoczesnych i konteneryzowanych aplikacji rozproszonej platformy. Z usługi kontenera platformy Azure inicjowania obsługi klastra DC/OS gotowy produkcji jest proste i szybkie. To szybki start szczegóły hello podstawowe wymagane czynności toodeploy klastra DC/OS i wykonywania podstawowych obciążenia.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-tooazure"></a>Zaloguj się za tooAzure 

Zaloguj się za tooyour subskrypcji platformy Azure z hello [logowania az](/cli/azure/#login) poleceń i wykonaj hello wyświetlanymi instrukcjami.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Tworzenie klastra DC/OS

Tworzenie klastra DC/OS z hello [az acs utworzyć](/cli/azure/acs#create) polecenia.

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

Tunel SSH Hello mogą być testowane za przeglądanie za`http://localhost`. Jeśli port innych czy 80 został użyty, Dostosuj hello toomatch lokalizacji. 

W przypadku tunelowania SSH hello została pomyślnie utworzona, jest zwracana hello DC/OS portalu.

![DCOS INTERFEJSU UŻYTKOWNIKA](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Instalowanie interfejsu wiersza polecenia DC/OS

Interfejs wiersza polecenia DC/OS Hello jest używany toomanage klastra DC/OS z hello wiersza polecenia. Zainstaluj interfejs wiersza polecenia hello DC/OS jest przy użyciu hello [az dcos acs install-cli](/azure/acs/dcos#install-cli) polecenia. Jeśli używasz usługi Azure CloudShell hello interfejsu wiersza polecenia DC/OS jest już zainstalowana. 

Jeśli używasz hello Azure CLI macOS lub Linux, może być konieczne toorun hello polecenie sudo.

```azurecli
az acs dcos install-cli
```

Przed hello interfejsu wiersza polecenia można używać z klastrem hello musi ona być tunelu SSH hello toouse skonfigurowany. toodo tak, uruchom hello następujące polecenia, dostosowywania hello portu, jeśli to konieczne.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Uruchamianie aplikacji

Domyślnie Hello planowania mechanizm dla klastra usługi ACS DC/OS jest Marathon. Marathon jest toostart używanych aplikacji i zarządzanie stanem hello aplikacji hello w klastrze DC/OS hello. tooschedule aplikacji za pośrednictwem platformy Marathon, Utwórz plik o nazwie *marathon app.json*, i hello kopiowania zawartości do niego. 

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
dcos marathon app add marathon-app.json
```

toosee hello stan wdrożenia dla aplikacji hello, uruchom następujące polecenie hello.

```azurecli
dcos marathon app list
```

Gdy hello **oczekiwania** zmienia wartość kolumny z *True* za*False*, wdrażanie aplikacji zostało zakończone.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Pobierz publiczny adres IP hello agentów klastra DC/OS hello.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Przeglądanie adres toothis zwraca hello domyślnej NGINX witryny.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Usuń klaster DC/OS

Gdy nie są już potrzebne, można użyć hello [usunięcie grupy az](/cli/azure/group#delete) polecenia grupy zasobów hello tooremove klastra DC/OS i wszystkie powiązane zasoby.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Następne kroki

W tym szybki start wdrożeniu klastra DC/OS i zostały uruchomione proste kontenera Docker na powitania klastra. toolearn więcej informacji na temat usługi kontenera platformy Azure, nadal samouczki toohello ACS.

> [!div class="nextstepaction"]
> [Zarządzanie klastrem ACS DC/OS](container-service-dcos-manage-tutorial.md)