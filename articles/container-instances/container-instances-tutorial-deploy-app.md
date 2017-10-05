---
title: "Samouczek wystąpień kontenera platformy Azure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 54151a5c1850ab7120fe666a46dc5dc99c0f5157
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-a-container-to-azure-container-instances"></a><span data-ttu-id="7c68a-103">Wdrażanie kontenera do wystąpień kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c68a-103">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="7c68a-104">Jest to ostatni trzech części samouczka.</span><span class="sxs-lookup"><span data-stu-id="7c68a-104">This is the last of a three-part tutorial.</span></span> <span data-ttu-id="7c68a-105">W poprzednich sekcjach [utworzono obrazów kontenera](container-instances-tutorial-prepare-app.md) i [do rejestru kontenera Azure](container-instances-tutorial-prepare-acr.md).</span><span class="sxs-lookup"><span data-stu-id="7c68a-105">In previous sections, [a container image was created](container-instances-tutorial-prepare-app.md) and [pushed to an Azure Container Registry](container-instances-tutorial-prepare-acr.md).</span></span> <span data-ttu-id="7c68a-106">W tej sekcji zakończeniu samouczka przez wdrożenie kontenera do wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c68a-106">This section completes the tutorial by deploying the container to Azure Container Instances.</span></span> <span data-ttu-id="7c68a-107">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="7c68a-107">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c68a-108">Definiowanie grupy kontenera przy użyciu szablonu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7c68a-108">Defining a container group using an Azure Resource Manager template</span></span>
> * <span data-ttu-id="7c68a-109">Wdrażanie grupy kontenerów przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c68a-109">Deploying the container group using the Azure CLI</span></span>
> * <span data-ttu-id="7c68a-110">Wyświetlanie dzienników kontenera</span><span class="sxs-lookup"><span data-stu-id="7c68a-110">Viewing container logs</span></span>

## <a name="deploy-the-container-using-the-azure-cli"></a><span data-ttu-id="7c68a-111">Wdrażanie kontenera przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c68a-111">Deploy the container using the Azure CLI</span></span>

<span data-ttu-id="7c68a-112">Interfejsu wiersza polecenia Azure umożliwia wdrożenie kontenera do wystąpień kontenera Azure za pomocą jednego polecenia.</span><span class="sxs-lookup"><span data-stu-id="7c68a-112">The Azure CLI enables deployment of a container to Azure Container Instances in a single command.</span></span> <span data-ttu-id="7c68a-113">Ponieważ obraz kontenera znajduje się w rejestrze prywatnej kontenera platformy Azure, musi zawierać poświadczenia wymagane do niego dostęp.</span><span class="sxs-lookup"><span data-stu-id="7c68a-113">Since the container image is hosted in the private Azure Container Registry, you must include the credentials required to access it.</span></span> <span data-ttu-id="7c68a-114">W razie potrzeby można je zapytanie, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="7c68a-114">If necessary, you can query them as shown below.</span></span>

<span data-ttu-id="7c68a-115">Kontener rejestru logowania serwera (aktualizacja nazwą rejestru):</span><span class="sxs-lookup"><span data-stu-id="7c68a-115">Container registry login server (update with your registry name):</span></span>

```azurecli-interactive
az acr show --name <acrName> --query loginServer
```

<span data-ttu-id="7c68a-116">Kontener rejestru hasło:</span><span class="sxs-lookup"><span data-stu-id="7c68a-116">Container registry password:</span></span>

```azurecli-interactive
az acr credential show --name <acrName> --query "passwords[0].value"
```

<span data-ttu-id="7c68a-117">Aby wdrożyć obraz kontenera z rejestru kontenera żądanie zasobu 1 rdzeń procesora CPU i 1GB pamięci, uruchom następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="7c68a-117">To deploy your container image from the container registry with a resource request of 1 CPU core and 1GB of memory, run the following command:</span></span>

```azurecli-interactive
az container create --name aci-tutorial-app --image <acrLoginServer>/aci-tutorial-app:v1 --cpu 1 --memory 1 --registry-password <acrPassword> --ip-address public -g myResourceGroup
```

<span data-ttu-id="7c68a-118">W ciągu kilku sekund zostanie wyświetlony początkową odpowiedź z usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7c68a-118">Within a few seconds, you will receive an initial response from Azure Resource Manager.</span></span> <span data-ttu-id="7c68a-119">Aby wyświetlić stan wdrożenia, należy użyć:</span><span class="sxs-lookup"><span data-stu-id="7c68a-119">To view the state of the deployment, use:</span></span>

```azurecli-interactive
az container show --name aci-tutorial-app --resource-group myResourceGroup --query state
```

<span data-ttu-id="7c68a-120">Można kontynuować, wykonanie tego polecenia, aż stan zmieni się z *oczekujące* do *systemem*.</span><span class="sxs-lookup"><span data-stu-id="7c68a-120">We can continue running this command until the state changes from *pending* to *running*.</span></span> <span data-ttu-id="7c68a-121">Następnie można przejść.</span><span class="sxs-lookup"><span data-stu-id="7c68a-121">Then we can proceed.</span></span>

## <a name="view-the-application-and-container-logs"></a><span data-ttu-id="7c68a-122">Wyświetl dzienniki aplikacji i kontenera</span><span class="sxs-lookup"><span data-stu-id="7c68a-122">View the application and container logs</span></span>

<span data-ttu-id="7c68a-123">Po pomyślnym wdrożeniu, otwórz przeglądarkę z adresem IP wyświetlany w danych wyjściowych z następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7c68a-123">Once the deployment succeeds, open your browser to the IP address shown in the output of the following command:</span></span>

```bash
az container show --name aci-tutorial-app --resource-group myResourceGroup --query ipAddress.ip
```

```json
"13.88.176.27"
```

![Witaj świecie aplikacji w przeglądarce][aci-app-browser]

<span data-ttu-id="7c68a-125">Można również wyświetlić dziennik wyjściowy kontenera:</span><span class="sxs-lookup"><span data-stu-id="7c68a-125">You can also view the log output of the container:</span></span>

```azurecli-interactive
az container logs --name aci-tutorial-app -g myResourceGroup
```

<span data-ttu-id="7c68a-126">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7c68a-126">Output:</span></span>

```bash
listening on port 80
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
::ffff:10.240.0.4 - - [21/Jul/2017:06:00:02 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://13.88.176.27/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_12_5) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/59.0.3071.115 Safari/537.36"
```

## <a name="next-steps"></a><span data-ttu-id="7c68a-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7c68a-127">Next steps</span></span>

<span data-ttu-id="7c68a-128">W tym samouczku wykonaniu procesu wdrażania kontenerów do wystąpień kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7c68a-128">In this tutorial, you completed the process of deploying your containers to Azure Container Instances.</span></span> <span data-ttu-id="7c68a-129">Wykonano następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="7c68a-129">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7c68a-130">Wdrażanie kontenera z rejestru kontenera Azure za pomocą wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="7c68a-130">Deploying the container from the Azure Container Registry using the Azure CLI</span></span>
> * <span data-ttu-id="7c68a-131">Wyświetlanie aplikacji w przeglądarce</span><span class="sxs-lookup"><span data-stu-id="7c68a-131">Viewing the application in the browser</span></span>
> * <span data-ttu-id="7c68a-132">Wyświetlanie dzienników kontenera</span><span class="sxs-lookup"><span data-stu-id="7c68a-132">Viewing the container logs</span></span>

<!-- LINKS -->
[prepare-app]: ./container-instances-tutorial-prepare-app.md

<!-- IMAGES -->
[aci-app-browser]: ./media/container-instances-quickstart/aci-app-browser.png
