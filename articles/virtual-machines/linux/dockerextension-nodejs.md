---
title: Witaj aaaUse rozszerzenia maszyny Wirtualnej Azure Docker z hello Azure CLI 1.0 | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toouse hello tooquickly rozszerzenia maszyny Wirtualnej platformy Docker i bezpiecznego wdrażania środowisku Docker na platformie Azure przy użyciu szablonów usługi Resource Manager."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a>Tworzenie środowiska Docker na platformie Azure przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello z hello Azure CLI w wersji 1.0
Docker jest popularnych kontenera zarządzania i tworzenia obrazu platformy, która pozwala tooquickly pracy z kontenerami w systemie Linux (i również z systemem Windows). Na platformie Azure istnieją różne sposoby, które można wdrożyć zgodnie z potrzebami tooyour Docker. Ten artykuł dotyczy przy użyciu rozszerzenia maszyny Wirtualnej platformy Docker hello i szablonów usługi Azure Resource Manager. 

Aby uzyskać więcej informacji na temat hello różne metody wdrażania, przy użyciu rozwiązania Docker maszyny i usługi kontenera platformy Azure, w tym temacie hello następujące artykuły:

* Prototyp tooquickly usługi aplikacji, można utworzyć przy użyciu jednego hosta Docker [maszyny Docker](docker-machine.md).
* W przypadku większych i bardziej stabilne środowisk, można użyć rozszerzenia maszyny Wirtualnej Azure Docker hello, który również obsługuje [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/) toogenerate spójne kontenera wdrożeń. Przy użyciu rozszerzenia maszyny Wirtualnej Azure Docker hello szczegółów tego artykułu.
* toobuild gotowe do produkcji, skalowalnej środowiskach, które zapewniają dodatkowe planowanie i narzędzia do zarządzania, można wdrożyć [Docker Swarm klastra na usługi kontenera platformy Azure](../../container-service/dcos-swarm/container-service-deployment.md).

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#azure-docker-vm-extension-overview) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](dockerextension.md) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello 

## <a name="azure-docker-vm-extension-overview"></a>Omówienie rozszerzenia Docker maszyny Wirtualnej platformy Azure
Witaj rozszerzenia maszyny Wirtualnej Azure Docker instaluje i konfiguruje demon Docker powitania klienta Docker i rozwiązania Docker Compose na maszynie wirtualnej systemu Linux (VM). Przy użyciu rozszerzenia maszyny Wirtualnej Azure Docker hello, mieć więcej kontroli i funkcji niż po prostu przy użyciu rozwiązania Docker maszyny lub tworzenie hostów Docker hello samodzielnie. Te dodatkowe funkcje, takie jak [rozwiązania Docker Compose](https://docs.docker.com/compose/overview/), Ustaw rozszerzenie maszyny Wirtualnej Azure Docker hello nadaje się do bardziej niezawodne środowiska dewelopera lub produkcji.

Szablony usługi Azure Resource Manager zdefiniuj hello strukturę całego środowiska. Szablony umożliwiają toocreate i skonfigurować zasoby, takie jak hello Docker hosta maszyn wirtualnych, magazynu, kontroli dostępu opartej na rolach (RBAC) i diagnostyki. Te szablony toocreate dodatkowe wdrożenia można użyć ponownie w sposób ciągły. Aby uzyskać więcej informacji na temat usługi Azure Resource Manager i szablony, zobacz [omówienie Resource Manager](../../azure-resource-manager/resource-group-overview.md). 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a>Wdrażanie szablonu z hello rozszerzenia maszyny Wirtualnej Azure Docker
Teraz Użyj istniejącego toocreate szablon szybkiego startu maszyny Wirtualnej systemu Ubuntu używa tooinstall rozszerzenia maszyny Wirtualnej Azure Docker hello i skonfiguruj hello Docker hosta. Można wyświetlić szablon hello tutaj: [proste wdrożenie maszyny Wirtualnej systemu Ubuntu z rozwiązaniem Docker z](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu). 

Należy hello [najnowsze interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) zainstalowane i rejestrowane w trybie hello Resource Manager w następujący sposób:

```azurecli
azure config mode arm
```

Wdrażanie szablonu hello przy użyciu hello Azure CLI, określając hello szablon identyfikatora URI. Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *westus* lokalizacji. Użyć własnego Nazwa grupy zasobów i lokalizacji:

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

Odpowiedzi tooname monity hello konta magazynu, podaj nazwę użytkownika i hasło i podaj nazwę DNS. Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Hello Azure CLI toohello wiersz po powraca tylko kilka sekund, ale Docker host jest nadal tworzona i konfigurowane za pomocą hello rozszerzenia maszyny Wirtualnej Azure Docker. Trwa kilka minut, aż hello toofinish wdrożenia. Można wyświetlić szczegółowe informacje o stanie hosta Docker hello przy użyciu hello `azure vm show` polecenia.

Hello poniższy przykład umożliwia sprawdzenie stanu hello hello maszyny Wirtualnej o nazwie *myDockerVM* (hello domyślną nazwę szablonu hello — nie zmieniać tej nazwy) w grupie zasobów hello o nazwie *myResourceGroup*. Wprowadź nazwę grupy zasobów hello utworzony w hello poprzedzających krok hello:

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

Witaj dane wyjściowe hello `azure vm show` polecenia jest toohello podobnie poniższy przykład:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

Górze hello hello danych wyjściowych, zobacz hello **ProvisioningState** z hello maszyny Wirtualnej. Gdy zostaną wyświetlone *zakończyło się pomyślnie*, hello wdrożenia zostało ukończone i można toohello SSH maszyny Wirtualnej.

Końcowej hello wyjściowego hello *FQDN* Wyświetla hello pełni kwalifikowaną nazwę domeny hosta Docker. Ta nazwa FQDN, które jest używane tooSSH tooyour Docker hosta w hello pozostałe kroki.

## <a name="deploy-your-first-nginx-container"></a>Wdrażanie Twojego pierwszego kontener nginx
Raz hello zakończeniu wdrażania SSH tooyour nowego Docker hosta z komputera lokalnego. Wprowadź własne nazwy użytkownika i nazwy FQDN:

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
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

Otwórz z kontenera akcji, toosee Konfigurowanie przeglądarki sieci web i wprowadź nazwę FQDN hosta Docker hello:

![Kontener ngnix uruchomione](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a>Odwołanie do szablonu Azure rozszerzenia maszyny Wirtualnej platformy Docker
Witaj w poprzednim przykładzie używa istniejący szablon szybkiego startu. Można także wdrożyć rozszerzenie maszyny Wirtualnej Azure Docker hello z szablonami usługi Resource Manager. toodo tak, Dodaj hello następujące szablony Menedżera zasobów tooyour, definiowanie hello *vmName* maszyny wirtualnej odpowiednio:

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
    "typeHandlerVersion": "1.1",
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

