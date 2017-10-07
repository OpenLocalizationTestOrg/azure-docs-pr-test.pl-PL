---
title: "aaaCreate Twojego pierwszego kontener wystąpień kontenera platformy Azure | Dokumentacja platformy Azure"
description: "Wdrażaj i rozpocznij pracę z usługą Azure Container Instances"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b57c52714933bd3b28c44d33f9af7cd1f23fb951
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-container-in-azure-container-instances"></a>Tworzenie pierwszego kontenera w usłudze Azure Container Instances

Wystąpień kontenera platformy Azure pozwala łatwo toocreate kontenerów i zarządzanie nimi na platformie Azure. W tym szybki start, utworzysz kontenera na platformie Azure i je ujawnić toohello internet z publicznym adresem IP. Ta operacja jest wykonywana za pomocą jednego polecenia. W ciągu kilku sekund w przeglądarce zobaczysz następujący wynik:

![Widziana w przeglądarce aplikacja wdrożona za pomocą usługi Azure Container Instances][aci-app-browser]

Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.12 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Tworzenie grupy zasobów

Wystąpienia Azure Container Instances są zasobami platformy Azure i należy je umieścić w grupie zasobów platformy Azure, czyli logicznej kolekcji, w której zasoby platformy Azure są wdrażane i zarządzane.

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia. 

Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a>Tworzenie kontenera

Kontener można utworzyć, podając nazwę obrazu usługi Docker i grupy zasobów platformy Azure. Opcjonalnie można ujawnić toohello kontenera hello internet z publicznym adresem IP. W tym przypadku użyjemy kontenera, który jest hostem bardzo prostej aplikacji internetowej napisanej w języku [Node.js](http://nodejs.org).

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

W ciągu kilku sekund należy pobrać żądanie tooyour odpowiedzi. Początkowo kontenera hello będą znajdować się w **tworzenie** stanu, ale powinna być uruchamiana w ciągu kilku sekund. Istnieje możliwość sprawdzenia stanu hello przy użyciu hello `show` polecenia:

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

U dołu hello hello dane wyjściowe zostanie wyświetlony stan inicjowania obsługi administracyjnej hello kontenera i jego adres IP:

```json
...
"ipAddress": {
      "ip": "13.88.8.148",
      "ports": [
        {
          "port": 80,
          "protocol": "TCP"
        }
      ]
    },
    "osType": "Linux",
    "provisioningState": "Succeeded"
...
```

Po kontenera hello przenosi toohello **zakończyło się pomyślnie** stanu, przejdziesz go w przeglądarce hello przy użyciu adresu IP hello podane. 

![Widziana w przeglądarce aplikacja wdrożona za pomocą usługi Azure Container Instances][aci-app-browser]

## <a name="pull-hello-container-logs"></a>Ściąganie hello kontenera dzienników

Można ściągnąć hello dzienniki dla kontenera hello zostały utworzone za pomocą hello `logs` polecenia:

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

Dane wyjściowe:

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a>Usunąć hello kontenera

Po wykonaniu hello kontenera, możesz je usunąć przy użyciu hello `delete` polecenia:

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

Wszystkie hello kodu kontenera hello używane w tym szybki start jest dostępny [w serwisie GitHub][app-github-repo], wraz z jego plik Dockerfile. Jeśli chcesz tootry tworzenia samodzielnie i wdrażania go przy użyciu hello rejestru kontenera Azure wystąpień kontenera tooAzure nadal toohello samouczek wystąpień kontenera platformy Azure.

> [!div class="nextstepaction"]
> [Samouczki dotyczące usługi Azure Container Instances](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png