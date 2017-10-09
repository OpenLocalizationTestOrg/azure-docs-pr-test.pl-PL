---
title: Witaj aaaUse rozszerzenia maszyny Wirtualnej Azure Docker | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello tooquickly rozszerzenia maszyny Wirtualnej platformy Docker bezpiecznego wdrażania w środowisku Docker na platformie Azure przy użyciu szablonów usługi Resource Manager i hello Azure CLI 2.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a>Tworzenie środowiska Docker na platformie Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello
Docker jest popularnych kontenera zarządzania i tworzenia obrazu platformy, która umożliwia tooquickly pracy z kontenerami w systemie Linux. Na platformie Azure istnieją różne sposoby, które można wdrożyć zgodnie z potrzebami tooyour Docker. Ten artykuł skupia się na używanie rozszerzenia maszyny Wirtualnej platformy Docker hello i szablony usługi Azure Resource Manager z hello Azure CLI 2.0. Można również wykonać te kroki hello [Azure CLI 1.0](dockerextension-nodejs.md).

## <a name="azure-docker-vm-extension-overview"></a>Omówienie rozszerzenia Docker maszyny Wirtualnej platformy Azure
Witaj rozszerzenia maszyny Wirtualnej Azure Docker instaluje i konfiguruje demon Docker powitania klienta Docker i rozwiązania Docker Compose na maszynie wirtualnej systemu Linux (VM). Przy użyciu rozszerzenia maszyny Wirtualnej Azure Docker hello, mieć więcej kontroli i funkcji niż po prostu przy użyciu rozwiązania Docker maszyny lub tworzenie hostów Docker hello samodzielnie. Te dodatkowe funkcje, takie jak [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/), Ustaw rozszerzenie maszyny Wirtualnej Azure Docker hello nadaje się do bardziej niezawodne środowiska dewelopera lub produkcji.

Aby uzyskać więcej informacji na temat hello różne metody wdrażania, przy użyciu rozwiązania Docker maszyny i usługi kontenera platformy Azure, w tym temacie hello następujące artykuły:

* Prototyp tooquickly usługi aplikacji, można utworzyć przy użyciu jednego hosta Docker [maszyny Docker](docker-machine.md).
* toobuild gotowe do produkcji, skalowalnej środowiskach, które zapewniają dodatkowe planowanie i narzędzia do zarządzania, można wdrożyć [Docker Swarm klastra na usługi kontenera platformy Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Wdrażanie szablonu z hello rozszerzenia maszyny Wirtualnej Azure Docker
Teraz Użyj istniejącego toocreate szablon szybkiego startu maszyny Wirtualnej systemu Ubuntu używa tooinstall rozszerzenia maszyny Wirtualnej Azure Docker hello i skonfiguruj hello Docker hosta. Można wyświetlić szablon hello tutaj: [proste wdrożenie maszyny Wirtualnej systemu Ubuntu z rozwiązaniem Docker z](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Najnowsza wersja należy hello [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zarejestrowane za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Najpierw utwórz nową grupę zasobów o [Tworzenie grupy az](/cli/azure/group#create). Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westus* lokalizacji:

```azurecli
az group create --name myResourceGroup --location westus
```

Następnie Wdróż maszynę Wirtualną za pomocą [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) zawierająca rozszerzenia maszyny Wirtualnej Azure Docker hello [tego szablonu usługi Azure Resource Manager w witrynie GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). Podać własne wartości *newStorageAccountName*, *adminUsername*, *adminPassword*, i *dnsNameForPublicIP* w następujący sposób:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Trwa kilka minut, aż hello toofinish wdrożenia. Po ukończeniu wdrażania hello [Przenieś krok toonext](#deploy-your-first-nginx-container) tooyour tooSSH maszyny Wirtualnej. 

Opcjonalnie dodaj monit toohello zwracany kontroli tooinstead i hello umożliwiają wdrożenie nadal w tle hello hello `--no-wait` Flaga toohello poprzedzających polecenia. Dzięki temu tooperform pracować w hello CLI wdrożenia hello kontynuuje kilka minut. 

Można wyświetlić szczegółowe informacje o stanie hosta Docker hello z [az maszyny wirtualnej pokazu](/cli/azure/vm#show). Hello poniższy przykład umożliwia sprawdzenie stanu hello hello maszyny Wirtualnej o nazwie *myDockerVM* (hello domyślną nazwę szablonu hello — nie zmieniać tej nazwy) w grupie zasobów hello o nazwie *myResourceGroup*:

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

Jeśli to polecenie zwraca *zakończyło się pomyślnie*, hello wdrożenia zostało ukończone i można toohello SSH maszyny Wirtualnej w powitania po kroku.

## <a name="deploy-your-first-nginx-container"></a>Wdrażanie Twojego pierwszego kontener nginx
Szczegóły tooview maszyny wirtualnej, takie jak nazwa DNS hello, użyj `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`. SSH tooyour Docker nowego hosta z komputera lokalnego w następujący sposób:

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

Po zalogowaniu toohello Docker hosta, uruchom teraz kontener nginx:

```bash
sudo docker run -d -p 80:80 nginx
```

dane wyjściowe Hello jest toohello podobnie poniższy przykład, jak obraz nginx hello jest pobierany i kontener uruchomiona:

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

Sprawdź stan hello kontenerów hello uruchomionych na hoście Docker w następujący sposób:

```bash
sudo docker ps
```

dane wyjściowe Hello toohello podobnie poniższy przykład, przedstawiający ten kontener nginx hello jest uruchomiona i porty TCP 80 i 443 i przesyłane dalej:

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

Otwórz z kontenera akcji, toosee Konfigurowanie przeglądarki sieci web i wprowadź nazwę DNS hello danego hosta Docker:

![Kontener ngnix uruchomione](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Odwołanie do szablonu Azure rozszerzenia maszyny Wirtualnej platformy Docker
Witaj w poprzednim przykładzie używa istniejący szablon szybkiego startu. Można także wdrożyć rozszerzenie maszyny Wirtualnej Azure Docker hello z szablonami usługi Resource Manager. toodo tak, Dodaj hello następujące szablony Menedżera zasobów tooyour, definiowanie hello `vmName` maszyny wirtualnej odpowiednio:

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

Można znaleźć bardziej szczegółowe wskazówki na korzystanie z szablonów usługi Resource Manager odczytując [Omówienie usługi Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).

## <a name="next-steps"></a>Następne kroki
Warto zapoznać się z zbyt[skonfigurować port TCP demon Docker hello](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), zrozumieć [zabezpieczeń Docker](https://docs.docker.com/engine/security/security/), lub wdrażanie kontenerów przy użyciu [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/). Aby uzyskać więcej informacji na powitania rozszerzenia maszyny Wirtualnej platformy Docker Azure się w temacie hello [projektu GitHub](https://github.com/Azure/azure-docker-extension/).

Przeczytaj więcej informacji na temat opcji hello do wdrażania dodatkowych Docker na platformie Azure:

* [Użyj Docker maszyny z hello Azure sterownika](docker-machine.md)  
* [Rozpoczynanie pracy z rozwiązaniem Docker tworzą toodefine i uruchomić aplikację usługi kontenera na maszynie wirtualnej platformy Azure](docker-compose-quickstart.md).
* [Wdrażanie klastra usługi Azure Container Service](../../container-service/dcos-swarm/container-service-deployment.md)

