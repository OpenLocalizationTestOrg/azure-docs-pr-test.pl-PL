---
title: "aaaAzure wystąpień kontenera - grupy wielu kontenerów | Dokumentacja platformy Azure"
description: "Wystąpień kontenera Azure - grupy wielu kontenerów"
services: container-instances
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 976f578cd2a9bf7f05ab97f24662139bb72062ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-group"></a>Wdrożenie grupy kontenera

Wystąpień kontenera platformy Azure obsługuje hello wdrażanie wielu kontenerów na jednym hoście przy użyciu *grupy kontenerów*. Jest to przydatne podczas kompilowania aplikacji boczną rejestrowania, monitorowania lub dowolnej innej konfiguracji gdzie usługa musi drugi dołączony proces. 

Ten dokument przeprowadzi Cię przez systemem proste boczną wielu kontenera konfiguracji przy użyciu szablonu usługi Azure Resource Manager.

## <a name="configure-hello-template"></a>Konfigurowanie szablonu hello

Utwórz plik o nazwie `azuredeploy.json` i kopiowania hello json do niego. 

W tym przykładzie zdefiniowano grupę kontenera o dwa kontenery i publiczny adres IP. kontener pierwszy Hello hello grupy uruchamia połączonej aplikacji internetowej. Hello drugi kontenera boczną hello sprawia, że aplikacji HTTP żądania toohello głównego sieci web za pośrednictwem sieci lokalnej hello grupy. 

W tym przykładzie boczną mogą być rozwinięty tootrigger alert, jeśli odebrano kod odpowiedzi HTTP innych niż 200 OK. 

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",    
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
    "resources": [
      {
        "name": "myContainerGroup",
        "type": "Microsoft.ContainerInstance/containerGroups",
        "apiVersion": "2017-08-01-preview",
        "location": "[resourceGroup().location]",
        "properties": {
          "containers": [
            {
              "name": "[variables('container1name')]",
              "properties": {
                "image": "[variables('container1image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                },
                "ports": [
                  {
                    "port": 80
                  }
                ]
              }
            },
            {
              "name": "[variables('container2name')]",
              "properties": {
                "image": "[variables('container2image')]",
                "resources": {
                  "requests": {
                    "cpu": 1,
                    "memoryInGb": 1.5
                    }
                }
              }
            }
          ],
          "osType": "Linux",
          "ipAddress": {
            "type": "Public",
            "ports": [
              {
                "protocol": "tcp",
                "port": "80"
              }
            ]
          }
        }
      }
    ],
    "outputs": {
      "containerIPv4Address": {
        "type": "string",
        "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', 'myContainerGroup')).ipAddress.ip]"
      }
    }
  }
```

toouse rejestru obrazu Kontener prywatny, Dodaj dokument json toohello obiektu z hello zgodny z formatem.

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a>Wdrażanie szablonu hello

Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

Wdrażanie szablonu hello z hello [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) polecenia.

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

W ciągu kilku sekund otrzymasz wstępnej reakcji z platformy Azure. 

## <a name="view-deployment-state"></a>Wyświetl stan wdrożenia

Stan hello tooview hello wdrożenia, użyj hello `az container show` polecenia. To polecenie zwróci hello udostępniane za pośrednictwem których hello aplikacji można uzyskać dostępu do publicznego adresu IP.

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

Dane wyjściowe:

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a>Wyświetl dzienniki   

Wyświetlanie danych wyjściowych dziennika hello kontenera za pomocą hello `az container logs` polecenia. Witaj `--container-name` argument określa kontener hello, od których dzienniki toopull. W tym przykładzie kontener pierwszy hello jest określony. 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

Dane wyjściowe:

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

toosee hello dzienniki dla kontenera samochodu po stronie powitania, uruchom hello same polecenie Określanie hello drugi nazwy kontenera.

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

Dane wyjściowe:

```bash
Every 3.0s: curl -I http://localhost                                                                                                                       Mon Jul 17 11:27:36 2017

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
Accept-Ranges: bytes
Content-Length: 1663
Content-Type: text/html; charset=utf-8
Last-Modified: Sun, 16 Jul 2017 02:08:22 GMT
Date: Mon, 17 Jul 2017 18:27:36 GMT
```

Jak widać, boczną hello jest okresowo wprowadzenie aplikacji głównego sieci web toohello żądania HTTP za pośrednictwem grupy hello tooensure sieci lokalnej, czy działa.

## <a name="next-steps"></a>Następne kroki

Ten dokument objęty hello kroki potrzebne do wdrożenia kontenera wielu wystąpień kontenera platformy Azure. Dla tooend zakończenia, który wystąpić wystąpień kontenera platformy Azure zobacz samouczek wystąpień kontenera Azure hello.

> [!div class="nextstepaction"]
> [Wystąpień kontenera azure samouczek]:./container-instances-tutorial-prepare-app.md
