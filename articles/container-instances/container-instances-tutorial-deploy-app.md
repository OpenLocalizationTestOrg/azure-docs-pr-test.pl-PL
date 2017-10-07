---
title: "Samouczek wystąpień kontenera aaaAzure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek wystąpień kontenera platformy Azure — wdrażanie aplikacji"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/04/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: b9fb098d9491e1073f0be4b14a0b9b1a18f16095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-container-tooazure-container-instances"></a><span data-ttu-id="1f01a-103">Wdrażanie kontenera tooAzure wystąpień kontenera</span><span class="sxs-lookup"><span data-stu-id="1f01a-103">Deploy a container tooAzure Container Instances</span></span>

<span data-ttu-id="1f01a-104">Jest to hello ostatnich trzech części samouczka.</span><span class="sxs-lookup"><span data-stu-id="1f01a-104">This is hello last of a three-part tutorial.</span></span> <span data-ttu-id="1f01a-105">W poprzednich sekcjach [utworzono obrazów kontenera](container-instances-tutorial-prepare-app.md) i [wypychana tooan rejestru kontenera Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="1f01a-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed tooan Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="1f01a-106">W tej sekcji zakończeniu samouczka hello wdrażając tooAzure kontenera hello wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="1f01a-106">This section completes hello tutorial by deploying hello container tooAzure Container Instances.</span></span> <span data-ttu-id="1f01a-107">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="1f01a-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f01a-108">Definiowanie grupy kontenera przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1f01a-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="1f01a-109">Wdrażanie hello kontenera grupy przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1f01a-109">Deploying hello container group using hello Azure CLI</span></span>
> * <span data-ttu-id="1f01a-110">Wyświetlanie dzienników kontenera</span><span class="sxs-lookup"><span data-stu-id="1f01a-110">Viewing container logs</span></span>

## <a name="deploy-hello-container-using-hello-azure-cli"></a><span data-ttu-id="1f01a-111">Wdrażanie kontenera hello przy użyciu hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1f01a-111">Deploy hello container using hello Azure CLI</span></span>

<span data-ttu-id="1f01a-112">Hello interfejsu wiersza polecenia Azure umożliwia wdrożenie tooAzure kontener wystąpień kontenera za pomocą jednego polecenia.</span><span class="sxs-lookup"><span data-stu-id="1f01a-112">hello Azure CLI enables deployment of a container tooAzure Container Instances in a single command.</span></span> <span data-ttu-id="1f01a-113">Ponieważ obraz kontenera hello jest obsługiwana w hello prywatnej rejestru kontenera platformy Azure, musi zawierać tooaccess wymagane poświadczenia hello go.</span><span class="sxs-lookup"><span data-stu-id="1f01a-113">Since hello container image is hosted in hello private Azure Container Registry, you must include hello credentials required tooaccess it.</span></span> <span data-ttu-id="1f01a-114">W razie potrzeby można je zapytanie, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="1f01a-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="1f01a-115">Kontener rejestru logowania serwera (aktualizacja nazwą rejestru):</span><span class="sxs-lookup"><span data-stu-id="1f01a-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="1f01a-116">Kontener rejestru hasło:</span><span class="sxs-lookup"><span data-stu-id="1f01a-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="1f01a-117">toodeploy kontener obrazu z rejestru kontenera hello z zasobem żądania 1 rdzeń procesora CPU i 1GB pamięci, uruchom następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="1f01a-117">toodeploy your container image from hello container registry with a resource request of 1 CPU core and 1GB of memory, run hello following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="1f01a-118">W ciągu kilku sekund zostanie wyświetlony początkową odpowiedź z usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1f01a-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="1f01a-119">Stan hello tooview hello wdrożenia, użyj:</span><span class="sxs-lookup"><span data-stu-id="1f01a-119">tooview hello state of hello deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="1f01a-120">Można kontynuować, wykonanie tego polecenia, dopóki hello stan zmieni się z *oczekujące* za*systemem*.</span><span class="sxs-lookup"><span data-stu-id="1f01a-120">We can continue running this command until hello state changes from *pending* too*running*.</span></span> <span data-ttu-id="1f01a-121">Następnie można przejść.</span><span class="sxs-lookup"><span data-stu-id="1f01a-121">Then we can proceed.</span></span>

## <a name="view-hello-application-and-container-logs"></a><span data-ttu-id="1f01a-122">Wyświetl dzienniki aplikacji i kontener hello</span><span class="sxs-lookup"><span data-stu-id="1f01a-122">View hello application and container logs</span></span>

<span data-ttu-id="1f01a-123">Po pomyślnym wdrożenia hello, Otwórz swój adres IP przeglądarki toohello wyświetlany w danych wyjściowych hello hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="1f01a-123">Once hello deployment succeeds, open your browser toohello IP address shown in hello output of hello following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Witaj świecie aplikację w przeglądarce hello][aci-app-browser]

<span data-ttu-id="1f01a-125">Można również wyświetlić wpisu w dzienniku hello hello kontenera:</span><span class="sxs-lookup"><span data-stu-id="1f01a-125">You can also view hello log output of hello container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="1f01a-126">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="1f01a-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="1f01a-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1f01a-127">Next steps</span></span>

<span data-ttu-id="1f01a-128">W tym samouczku została ukończona hello proces wdrażania tooAzure Twojego kontenery wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="1f01a-128">In this tutorial, you completed hello process of deploying your containers tooAzure Container Instances.</span></span> <span data-ttu-id="1f01a-129">Zakończono Hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="1f01a-129">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1f01a-130">Wdrażanie kontenera hello z hello rejestru kontenera Azure za pomocą hello wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="1f01a-130">Deploying hello container from hello Azure Container Registry using hello Azure CLI</span></span>
> * <span data-ttu-id="1f01a-131">Wyświetlanie aplikacji hello w przeglądarce hello</span><span class="sxs-lookup"><span data-stu-id="1f01a-131">Viewing hello application in hello browser</span></span>
> * <span data-ttu-id="1f01a-132">Wyświetlanie hello kontenera dzienników</span><span class="sxs-lookup"><span data-stu-id="1f01a-132">Viewing hello container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
