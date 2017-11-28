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
# <a name="create-your-first-container-in-azure-container-instances"></a><span data-ttu-id="3f3d1-103">Tworzenie pierwszego kontenera w usłudze Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="3f3d1-103">Create your first container in Azure Container Instances</span></span>

<span data-ttu-id="3f3d1-104">Wystąpień kontenera platformy Azure pozwala łatwo toocreate kontenerów i zarządzanie nimi na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-104">Azure Container Instances makes it easy toocreate and manage containers in Azure.</span></span> <span data-ttu-id="3f3d1-105">W tym szybki start, utworzysz kontenera na platformie Azure i je ujawnić toohello internet z publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-105">In this quick start, you will create a container in Azure and expose it toohello internet with a public IP address.</span></span> <span data-ttu-id="3f3d1-106">Ta operacja jest wykonywana za pomocą jednego polecenia.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-106">This operation is completed in a single command.</span></span> <span data-ttu-id="3f3d1-107">W ciągu kilku sekund w przeglądarce zobaczysz następujący wynik:</span><span class="sxs-lookup"><span data-stu-id="3f3d1-107">Within just a few seconds, you will see this in your browser:</span></span>

![Widziana w przeglądarce aplikacja wdrożona za pomocą usługi Azure Container Instances][aci-app-browser]

<span data-ttu-id="3f3d1-109">Jeśli nie masz subskrypcji platformy Azure, przed rozpoczęciem utwórz [bezpłatne konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="3f3d1-109">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="3f3d1-110">Wybierz tooinstall, użyj interfejsu wiersza polecenia hello lokalnie tego przewodnika Szybki Start wymaga działają hello Azure CLI w wersji 2.0.12 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-110">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.12 or later.</span></span> <span data-ttu-id="3f3d1-111">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3f3d1-112">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3f3d1-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="3f3d1-113">Tworzenie grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="3f3d1-113">Create a resource group</span></span>

<span data-ttu-id="3f3d1-114">Wystąpienia Azure Container Instances są zasobami platformy Azure i należy je umieścić w grupie zasobów platformy Azure, czyli logicznej kolekcji, w której zasoby platformy Azure są wdrażane i zarządzane.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-114">Azure Container Instances are Azure resources and must be placed in an Azure resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="3f3d1-115">Utwórz grupę zasobów o hello [Tworzenie grupy az](/cli/azure/group#create) polecenia.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-115">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="3f3d1-116">Witaj poniższy przykład tworzy grupę zasobów o nazwie *myResourceGroup* w hello *eastus* lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="3f3d1-117">Tworzenie kontenera</span><span class="sxs-lookup"><span data-stu-id="3f3d1-117">Create a container</span></span>

<span data-ttu-id="3f3d1-118">Kontener można utworzyć, podając nazwę obrazu usługi Docker i grupy zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-118">You can create a container by providing a name, a Docker image, and an Azure resource group.</span></span> <span data-ttu-id="3f3d1-119">Opcjonalnie można ujawnić toohello kontenera hello internet z publicznym adresem IP.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-119">You can optionally expose hello container toohello internet with a public IP address.</span></span> <span data-ttu-id="3f3d1-120">W tym przypadku użyjemy kontenera, który jest hostem bardzo prostej aplikacji internetowej napisanej w języku [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="3f3d1-120">In this case, we'll use a container that hosts a very simple web app written in [Node.js](http://nodejs.org).</span></span>

```azurecli-interactive
az container create --name mycontainer --image microsoft/aci-helloworld --resource-group myResourceGroup --ip-address public 
```

<span data-ttu-id="3f3d1-121">W ciągu kilku sekund należy pobrać żądanie tooyour odpowiedzi.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-121">Within a few seconds, you should get a response tooyour request.</span></span> <span data-ttu-id="3f3d1-122">Początkowo kontenera hello będą znajdować się w **tworzenie** stanu, ale powinna być uruchamiana w ciągu kilku sekund.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-122">Initially, hello container will be in a **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="3f3d1-123">Istnieje możliwość sprawdzenia stanu hello przy użyciu hello `show` polecenia:</span><span class="sxs-lookup"><span data-stu-id="3f3d1-123">You can check hello status using hello `show` command:</span></span>

```azurecli-interactive
az container show --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="3f3d1-124">U dołu hello hello dane wyjściowe zostanie wyświetlony stan inicjowania obsługi administracyjnej hello kontenera i jego adres IP:</span><span class="sxs-lookup"><span data-stu-id="3f3d1-124">At hello bottom of hello output, you will see hello container's provisioning state and its IP address:</span></span>

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

<span data-ttu-id="3f3d1-125">Po kontenera hello przenosi toohello **zakończyło się pomyślnie** stanu, przejdziesz go w przeglądarce hello przy użyciu adresu IP hello podane.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-125">Once hello container moves toohello **Succeeded** state, you can reach it in hello browser using hello IP address provided.</span></span> 

![Widziana w przeglądarce aplikacja wdrożona za pomocą usługi Azure Container Instances][aci-app-browser]

## <a name="pull-hello-container-logs"></a><span data-ttu-id="3f3d1-127">Ściąganie hello kontenera dzienników</span><span class="sxs-lookup"><span data-stu-id="3f3d1-127">Pull hello container logs</span></span>

<span data-ttu-id="3f3d1-128">Można ściągnąć hello dzienniki dla kontenera hello zostały utworzone za pomocą hello `logs` polecenia:</span><span class="sxs-lookup"><span data-stu-id="3f3d1-128">You can pull hello logs for hello container you created using hello `logs` command:</span></span>

```azurecli-interactive
az container logs --name mycontainer --resource-group myResourceGroup
```

<span data-ttu-id="3f3d1-129">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="3f3d1-129">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.255.105 - - [21/Jul/2017:00:01:46 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://104.210.39.122/" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="delete-hello-container"></a><span data-ttu-id="3f3d1-130">Usunąć hello kontenera</span><span class="sxs-lookup"><span data-stu-id="3f3d1-130">Delete hello container</span></span>

<span data-ttu-id="3f3d1-131">Po wykonaniu hello kontenera, możesz je usunąć przy użyciu hello `delete` polecenia:</span><span class="sxs-lookup"><span data-stu-id="3f3d1-131">When you are done with hello container, you can remove it using hello `delete` command:</span></span>

```azurecli-interactive
az container delete --name mycontainer --resource-group myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="3f3d1-132">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="3f3d1-132">Next steps</span></span>

<span data-ttu-id="3f3d1-133">Wszystkie hello kodu kontenera hello używane w tym szybki start jest dostępny [w serwisie GitHub][app-github-repo], wraz z jego plik Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-133">All of hello code for hello container used in this quick start is available [on GitHub][app-github-repo], along with its Dockerfile.</span></span> <span data-ttu-id="3f3d1-134">Jeśli chcesz tootry tworzenia samodzielnie i wdrażania go przy użyciu hello rejestru kontenera Azure wystąpień kontenera tooAzure nadal toohello samouczek wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="3f3d1-134">If you'd like tootry building it yourself and deploying it tooAzure Container Instances using hello Azure Container Registry, continue toohello Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f3d1-135">Samouczki dotyczące usługi Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="3f3d1-135">Azure Container Instances tutorials</span></span>](./container-instances-tutorial-prepare-app.md)


<!-- LINKS -->
[app-github-repo]: https://github.com/Azure-Samples/aci-helloworld.git

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png