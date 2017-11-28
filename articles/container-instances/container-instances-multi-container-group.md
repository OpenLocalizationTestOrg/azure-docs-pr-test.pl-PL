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
# <a name="deploy-a-container-group"></a><span data-ttu-id="d973f-103">Wdrożenie grupy kontenera</span><span class="sxs-lookup"><span data-stu-id="d973f-103">Deploy a container group</span></span>

<span data-ttu-id="d973f-104">Wystąpień kontenera platformy Azure obsługuje hello wdrażanie wielu kontenerów na jednym hoście przy użyciu *grupy kontenerów*.</span><span class="sxs-lookup"><span data-stu-id="d973f-104">Azure Container Instances support hello deployment of multiple containers onto a single host using a *container group*.</span></span> <span data-ttu-id="d973f-105">Jest to przydatne podczas kompilowania aplikacji boczną rejestrowania, monitorowania lub dowolnej innej konfiguracji gdzie usługa musi drugi dołączony proces.</span><span class="sxs-lookup"><span data-stu-id="d973f-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span> 

<span data-ttu-id="d973f-106">Ten dokument przeprowadzi Cię przez systemem proste boczną wielu kontenera konfiguracji przy użyciu szablonu usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d973f-106">This document walks through running a simple multi-container sidecar configuration using an Azure Resource Manager template.</span></span>

## <a name="configure-hello-template"></a><span data-ttu-id="d973f-107">Konfigurowanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="d973f-107">Configure hello template</span></span>

<span data-ttu-id="d973f-108">Utwórz plik o nazwie `azuredeploy.json` i kopiowania hello json do niego.</span><span class="sxs-lookup"><span data-stu-id="d973f-108">Create a file named `azuredeploy.json` and copy hello following json into it.</span></span> 

<span data-ttu-id="d973f-109">W tym przykładzie zdefiniowano grupę kontenera o dwa kontenery i publiczny adres IP.</span><span class="sxs-lookup"><span data-stu-id="d973f-109">In this sample, a container group with two containers and a public IP address is defined.</span></span> <span data-ttu-id="d973f-110">kontener pierwszy Hello hello grupy uruchamia połączonej aplikacji internetowej.</span><span class="sxs-lookup"><span data-stu-id="d973f-110">hello first container of hello group runs an internet facing application.</span></span> <span data-ttu-id="d973f-111">Hello drugi kontenera boczną hello sprawia, że aplikacji HTTP żądania toohello głównego sieci web za pośrednictwem sieci lokalnej hello grupy.</span><span class="sxs-lookup"><span data-stu-id="d973f-111">hello second container, hello sidecar, makes an HTTP request toohello main web application via hello group's local network.</span></span> 

<span data-ttu-id="d973f-112">W tym przykładzie boczną mogą być rozwinięty tootrigger alert, jeśli odebrano kod odpowiedzi HTTP innych niż 200 OK.</span><span class="sxs-lookup"><span data-stu-id="d973f-112">This sidecar example could be expanded tootrigger an alert if it received an HTTP response code other than 200 OK.</span></span> 

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

<span data-ttu-id="d973f-113">toouse rejestru obrazu Kontener prywatny, Dodaj dokument json toohello obiektu z hello zgodny z formatem.</span><span class="sxs-lookup"><span data-stu-id="d973f-113">toouse a private container image registry, add an object toohello json document with hello following format.</span></span>

```json
"imageRegistryCredentials": [
    {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
    }
]
```

## <a name="deploy-hello-template"></a><span data-ttu-id="d973f-114">Wdrażanie szablonu hello</span><span class="sxs-lookup"><span data-stu-id="d973f-114">Deploy hello template</span></span>

<span data-ttu-id="d973f-115">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d973f-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="d973f-116">Wdrażanie szablonu hello z hello [Utwórz wdrożenie grupy az](/cli/azure/group/deployment#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="d973f-116">Deploy hello template with hello [az group deployment create](/cli/azure/group/deployment#create) command.</span></span>

```azurecli-interactive
az group deployment create --name myContainerGroup --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="d973f-117">W ciągu kilku sekund otrzymasz wstępnej reakcji z platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d973f-117">Within a few seconds, you will receive an initial response from Azure.</span></span> 

## <a name="view-deployment-state"></a><span data-ttu-id="d973f-118">Wyświetl stan wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d973f-118">View deployment state</span></span>

<span data-ttu-id="d973f-119">Stan hello tooview hello wdrożenia, użyj hello `az container show` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d973f-119">tooview hello state of hello deployment, use hello `az container show` command.</span></span> <span data-ttu-id="d973f-120">To polecenie zwróci hello udostępniane za pośrednictwem których hello aplikacji można uzyskać dostępu do publicznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="d973f-120">This returns hello provisioned public IP address over which hello application can be accessed.</span></span>

```azurecli-interactive
az container show --name myContainerGroup --resource-group myResourceGroup -o table
```

<span data-ttu-id="d973f-121">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d973f-121">Output:</span></span>

```azurecli
Name              ResourceGroup    ProvisioningState    Image                                                             IP:ports           CPU/Memory    OsType    Location
----------------  ---------------  -------------------  ----------------------------------------------------------------  -----------------  ------------  --------  ----------
myContainerGroup  myResourceGrou2  Succeeded            microsoft/aci-tutorial-sidecar,microsoft/aci-tutorial-app:v1      40.118.253.154:80  1.0 core/1.5 gb   Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="d973f-122">Wyświetl dzienniki</span><span class="sxs-lookup"><span data-stu-id="d973f-122">View logs</span></span>   

<span data-ttu-id="d973f-123">Wyświetlanie danych wyjściowych dziennika hello kontenera za pomocą hello `az container logs` polecenia.</span><span class="sxs-lookup"><span data-stu-id="d973f-123">View hello log output of a container using hello `az container logs` command.</span></span> <span data-ttu-id="d973f-124">Witaj `--container-name` argument określa kontener hello, od których dzienniki toopull.</span><span class="sxs-lookup"><span data-stu-id="d973f-124">hello `--container-name` argument specifies hello container from which toopull logs.</span></span> <span data-ttu-id="d973f-125">W tym przykładzie kontener pierwszy hello jest określony.</span><span class="sxs-lookup"><span data-stu-id="d973f-125">In this example, hello first container is specified.</span></span> 

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-app --resource-group myResourceGroup
```

<span data-ttu-id="d973f-126">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d973f-126">Output:</span></span>

```bash
istening on port 80
::1 - - [27/Jul/2017:17:35:29 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:32 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:35 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [27/Jul/2017:17:35:38 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="d973f-127">toosee hello dzienniki dla kontenera samochodu po stronie powitania, uruchom hello same polecenie Określanie hello drugi nazwy kontenera.</span><span class="sxs-lookup"><span data-stu-id="d973f-127">toosee hello logs for hello side-car container, run hello same command specifying hello second container name.</span></span>

```azurecli-interactive
az container logs --name myContainerGroup --container-name aci-tutorial-sidecar --resource-group myResourceGroup
```

<span data-ttu-id="d973f-128">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="d973f-128">Output:</span></span>

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

<span data-ttu-id="d973f-129">Jak widać, boczną hello jest okresowo wprowadzenie aplikacji głównego sieci web toohello żądania HTTP za pośrednictwem grupy hello tooensure sieci lokalnej, czy działa.</span><span class="sxs-lookup"><span data-stu-id="d973f-129">As you can see, hello sidecar is periodically making an HTTP request toohello main web application via hello group's local network tooensure that it is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d973f-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d973f-130">Next steps</span></span>

<span data-ttu-id="d973f-131">Ten dokument objęty hello kroki potrzebne do wdrożenia kontenera wielu wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="d973f-131">This document covered hello steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="d973f-132">Dla tooend zakończenia, który wystąpić wystąpień kontenera platformy Azure zobacz samouczek wystąpień kontenera Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d973f-132">For an end tooend Azure Container Instances experience, see hello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="d973f-133">[Wystąpień kontenera azure samouczek]:./container-instances-tutorial-prepare-app.md</span><span class="sxs-lookup"><span data-stu-id="d973f-133">[Azure Container Instances tutorial]: ./container-instances-tutorial-prepare-app.md</span></span>
