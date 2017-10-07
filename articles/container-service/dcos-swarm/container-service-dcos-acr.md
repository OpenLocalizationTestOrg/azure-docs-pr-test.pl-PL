---
title: aaaUsing ACR z klastrem Azure DC/OS | Dokumentacja firmy Microsoft
description: "Rejestru kontenera Azure za pomocą klastra DC/OS usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, kontenerów, Micro-services, Mesos, Azure, udziału plików, cifs"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a>Za pomocą ACR toodeploy klastra DC/OS aplikacji

W tym artykule, firma Microsoft Eksploruj jak toouse rejestru kontenera platformy Azure z klastrem DC/OS. Przy użyciu ACR pozwala tooprivately magazynu obrazów i zarządzanie nimi kontenera. Ten samouczek obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Wdrażanie rejestru kontenera platformy Azure (w razie potrzeby)
> * Skonfiguruj uwierzytelnianie ACR w klastrze DC/OS
> * Przekazać obraz toohello rejestru kontenera platformy Azure
> * Uruchom obrazu kontenera z hello rejestru kontenera platformy Azure

Należy ACS DC/OS hello toocomplete klastra kroków w tym samouczku. W razie potrzeby [w tym przykładzie skrypt](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) można utworzyć.

Ten samouczek wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a>Wdrażanie rejestru kontenera platformy Azure

W razie potrzeby utwórz rejestru kontenera Azure z hello [az acr utworzyć](/cli/azure/acr#create) polecenia. 

Witaj poniższy przykład tworzy rejestru z losowo wygenerować nazwę. rejestru Hello jest również konfigurowany za pomocą konta administratora przy użyciu hello `--admin-enabled` argumentu.

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

Po utworzeniu rejestru hello hello Azure CLI generuje dane podobne toohello poniżej. Zwróć uwagę na powitania `name` i `loginServer`, są one używane w kolejnych krokach.

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

Uzyskiwanie poświadczeń rejestru kontenera hello przy użyciu hello [Pokaż poświadczeń acr az](/cli/azure/acr/credential) polecenia. SUBSTITUTE hello `--name` z jedną zanotowanym w ostatnim kroku hello hello. Zwróć uwagę jednego hasła jest potrzebna w kolejnym kroku.

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

Aby uzyskać więcej informacji na rejestru kontenera platformy Azure, zobacz [rejestrów kontenera Docker tooprivate wprowadzenie](../../container-registry/container-registry-intro.md). 

## <a name="manage-acr-authentication"></a>Zarządzanie ACR uwierzytelniania

Hello konwencjonalnej sposób toopush i ściągania obrazu z rejestru prywatnej toofirst uwierzytelniania za pomocą rejestru hello. toodo tak, czy użycie hello `docker login` na klienta, który wymaga tooaccess hello prywatnej rejestru. Ponieważ klaster DC/OS może zawierać wiele węzłów, które wymagają toobe uwierzytelniani hello ACR, jest przydatne tooautomate ten proces w każdym węźle. 

### <a name="create-shared-storage"></a>Utwórz magazyn udostępniony

Ten proces wykorzystuje na udział plików na platformę Azure, który został zainstalowany w każdym węźle klastra hello. Jeśli Magazyn udostępniony nie mają już skonfigurowany, zobacz [udział plików w klastrze DC/OS](container-service-dcos-fileshare.md).

### <a name="configure-acr-authentication"></a>Skonfiguruj uwierzytelnianie ACR

Najpierw pobierz hello FQDN hello DC/OS wzorca i zapisze go w zmiennej.

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

Utwórz połączenie SSH z głównego hello (lub hello pierwszego serwera głównego) klastra systemu DC/OS. Zaktualizuj hello nazwy użytkownika, jeśli podczas tworzenia klastra hello użyto wartości innych niż domyślne.

```azurecli-interactive
ssh azureuser@$FQDN
```

Uruchom następujące polecenia toologin toohello rejestru kontenera Azure hello. Zastąp hello `--username` o nazwie hello hello kontenera rejestru i hello `--password` z haseł hello podane. Zastąp hello ostatni argument *mycontainerregistry.azurecr.io* w przykładzie hello o nazwie loginServer hello hello kontenera rejestru. 

To polecenie zapisuje wartości uwierzytelniania hello lokalnie w hello `~/.docker` ścieżki.

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

Tworzenie pliku skompresowanego, który zawiera wartości uwierzytelniania hello kontenera.

```azurecli-interactive
tar czf docker.tar.gz .docker
```

Skopiuj ten plik toohello udostępnionym w klastrze magazynu. Ten krok sprawia, że plik hello dostępne we wszystkich węzłach klastra DC/OS hello.

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a>Przekaż obraz tooACR

Teraz z komputerze deweloperskim lub inne systemy z Docker zainstalowane, tworzenie obrazu i przekaż go toohello rejestru kontenera Azure.

Utwórz kontener z hello Ubuntu obrazu.

```azurecli-interactive
docker run ubunut --name base-image
```

Teraz przechwytywania hello kontenera do nowego obrazu. Nazwa obrazu Hello musi tooinclude hello `loginServer` nazwa hello registrywith kontenera w formacie `loginServer/imageName`.

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

Zaloguj się do hello rejestru kontenera platformy Azure. Zamień nazwę hello hello loginServer nazwę, hello — nazwa użytkownika o nazwie hello hello kontenera rejestru i hello — haseł hello podać hasło.

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

Na koniec przekazać hello obrazu toohello ACR rejestru. W tym przykładzie przesyła obraz o nazwie dcos demonstracyjnej.

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a>Uruchom obrazu z ACR

toouse jako obraz z rejestru ACR hello, Utwórz plik nazwy *acrDemo.json* i hello kopiowania tekstu do niego. Zamień nazwę obrazu hello hello kontenera rejestru loginServer nazwę i nazwa obrazu, na przykład `loginServer/imageName`. Zwróć uwagę na powitania `uris` właściwości. Ta właściwość przechowuje lokalizacji hello hello kontenera rejestru uwierzytelniania pliku, który w tym przypadku jest hello udział plików na platformę Azure, który jest zainstalowany na każdym węźle w klastrze DC/OS hello.

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

Wdrażanie aplikacji hello przy użyciu interfejsu wiersza polecenia DC / ° c hello.

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku zostały skonfiguruj toouse DC/OS, który rejestru kontenera Azure tym hello następujące zadania:

> [!div class="checklist"]
> * Wdrażanie rejestru kontenera platformy Azure (w razie potrzeby)
> * Skonfiguruj uwierzytelnianie ACR w klastrze DC/OS
> * Przekazać obraz toohello rejestru kontenera platformy Azure
> * Uruchom obrazu kontenera z hello rejestru kontenera platformy Azure
