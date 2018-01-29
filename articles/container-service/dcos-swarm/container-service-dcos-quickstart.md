---
title: "Szybki start — wdrażanie klastra DC/OS w usłudze Azure Container Service"
description: "Szybki start — wdrażanie klastra DC/OS w usłudze Azure Container Service"
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: quickstart
ms.date: 08/04/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 69f8f415ce851a5d8034d8196ab541e8491dc417
ms.sourcegitcommit: 5d3e99478a5f26e92d1e7f3cec6b0ff5fbd7cedf
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/06/2017
---
# <a name="deploy-a-dcos-cluster"></a>Wdrażanie klastra DC/OS

System DC/OS zapewnia rozproszoną platformę dla nowoczesnych, konteneryzowanych aplikacji. Usługa Azure Container Service umożliwia łatwe i szybkie inicjowanie obsługi produkcyjnego klastra DC/OS. W tym przewodniku Szybki start przedstawiono szczegółowo podstawowe kroki wdrażania klastra DC/OS oraz uruchamiania podstawowego obciążenia.

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

Dla tego samouczka wymagany jest interfejs wiersza polecenia platformy Azure w wersji 2.0.4 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczne będzie uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="log-in-to-azure"></a>Zaloguj się do platformy Azure. 

Zaloguj się do subskrypcji platformy Azure za pomocą polecenia [az login](/cli/azure/#login) i postępuj zgodnie z instrukcjami wyświetlanymi na ekranie.

```azurecli
az login
```

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Utwórz grupę zasobów za pomocą polecenia [az group create](/cli/azure/group#create). Grupa zasobów platformy Azure to logiczny kontener przeznaczony do wdrażania zasobów platformy Azure i zarządzania nimi. 

Poniższy przykład obejmuje tworzenie grupy zasobów o nazwie *myResourceGroup* w lokalizacji *eastus*.

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-dcos-cluster"></a>Tworzenie klastra DC/OS

Aby utworzyć klaster DC/OS, użyj polecenia [az acs create](/cli/azure/acs#create).

Następujący przykład umożliwia utworzenie klastra DC/OS o nazwie *myDCOSCluster* oraz kluczy SSH, jeśli jeszcze nie istnieją. Aby użyć określonego zestawu kluczy, użyj opcji `--ssh-key-value`.  

```azurecli
az acs create --orchestrator-type dcos --resource-group myResourceGroup --name myDCOSCluster --generate-ssh-keys
```

W niektórych przypadkach, np. ograniczonej wersji próbnej, subskrypcja platformy Azure ma ograniczony dostęp do zasobów platformy Azure. Jeśli wdrożenie nie powiedzie się z powodu ograniczonej liczby dostępnych rdzeni, zmniejsz domyślną liczbę agentów, dodając `--agent-count 1` do polecenia [az acs create](/cli/azure/acs#create). 

Po kilku minutach wykonywanie polecenia zostanie zakończone i zwrócone zostaną informacje o wdrożeniu.

## <a name="connect-to-dcos-cluster"></a>Nawiązywanie połączenia z klastrem DC/OS

Po utworzeniu klastra DC/OS można uzyskać do niego dostęp za pośrednictwem tunelu SSH. Uruchom następujące polecenie, aby zwrócić publiczny adres klastra DC/OS. Adres IP jest przechowywany w zmiennej i zostanie użyty w kolejnym kroku.

```azurecli
ip=$(az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-master')].[ipAddress]" -o tsv)
```

Aby utworzyć tunel SSH, uruchom następujące polecenie, po czym postępuj zgodnie z instrukcjami na ekranie. Jeśli port 80 jest już używany, wykonanie polecenia nie powiedzie się. Zmień port tunelu na port, który nie jest używany, na przykład `85:localhost:80`. 

```azurecli
sudo ssh -i ~/.ssh/id_rsa -fNL 80:localhost:80 -p 2200 azureuser@$ip
```

Możesz przetestować tunel SSH, przechodząc do lokalizacji `http://localhost`. Jeśli użyto portu innego niż port 80, odpowiednio zmień lokalizację. 

Jeśli tunel SSH został pomyślnie utworzony, zostanie zwrócony portal DC/OS.

![Interfejs użytkownika systemu DC/OS](./media/container-service-dcos-quickstart/dcos-ui.png)

## <a name="install-dcos-cli"></a>Instalowanie interfejsu wiersza polecenia DC/OS

Interfejs wiersza polecenia DC/OS służy do zarządzania klastrem DC/OS z poziomu wiersza polecenia. Zainstaluj interfejs wiersza polecenia DC/OS, używając polecenia [az acs dcos install-cli](/azure/acs/dcos#install-cli). Jeśli korzystasz z usługi Azure CloudShell, interfejs wiersza polecenia DC/OS jest już zainstalowany. 

Jeśli używasz interfejsu wiersza polecenia platformy Azure w systemie macOS lub Linux, konieczne może być uruchomienie polecenia za pomocą programu sudo.

```azurecli
az acs dcos install-cli
```

Aby można było użyć interfejsu wiersza polecenia z klastrem, należy skonfigurować go tak, aby korzystał z tunelu SSH. W tym celu uruchom następujące polecenie, w razie potrzeby dostosowując port.

```azurecli
dcos config set core.dcos_url http://localhost
```

## <a name="run-an-application"></a>Uruchamianie aplikacji

Domyślny mechanizm planowania w przypadku klastra DC/OS w usłudze ACS to Marathon. Platforma Marathon jest używana w celu uruchomienia aplikacji i zarządzania jej stanem w klastrze DC/OS. Aby zaplanować uruchomienie aplikacji za pośrednictwem platformy Marathon, utwórz plik o nazwie *marathon-app.json* i skopiuj do niego następującą zawartość. 

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

Uruchom następujące polecenie, aby zaplanować uruchomienie aplikacji w klastrze DC/OS.

```azurecli
dcos marathon app add marathon-app.json
```

Aby wyświetlić stan wdrożenia aplikacji, uruchom następujące polecenie.

```azurecli
dcos marathon app list
```

Zamiana wartości w kolumnie **OCZEKIWANIE** z *Prawda* na *Fałsz* oznacza, że wdrażanie aplikacji zostało zakończone.

```azurecli
ID     MEM  CPUS  TASKS  HEALTH  DEPLOYMENT  WAITING  CONTAINER  CMD   
/test   32   1     1/1    ---       ---      False      DOCKER   None
```

Uzyskaj publiczny adres IP agentów klastra DC/OS.

```azurecli
az network public-ip list --resource-group myResourceGroup --query "[?contains(name,'dcos-agent')].[ipAddress]" -o tsv
```

Po przejściu do tego adresu zostanie zwrócona domyślna witryna serwera NGINX.

![NGINX](./media/container-service-dcos-quickstart/nginx.png)

## <a name="delete-dcos-cluster"></a>Usuwanie klastra DC/OS

Gdy klaster nie będzie już potrzebny, można użyć polecenia [az group delete](/cli/azure/group#delete), aby usunąć grupę zasobów, klaster DC/OS oraz wszystkie pokrewne zasoby.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="next-steps"></a>Następne kroki

Podczas pracy z tym przewodnikiem Szybki start wdrożono klaster DC/OS i uruchomiono w nim prosty kontener platformy Docker. Aby dowiedzieć się więcej na temat usługi Azure Container Service, przejdź do samouczków dotyczących usługi Azure Container Service.

> [!div class="nextstepaction"]
> [Manage an ACS DC/OS Cluster](container-service-dcos-manage-tutorial.md) (Zarządzanie klastrem DC/OS usługi ACS)