---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - kierować ruchem wysoką dostępność aplikacji | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - kierować ruchem wysoką dostępność aplikacji"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="a2649-103">Kierować ruchem wysoką dostępność aplikacji</span><span class="sxs-lookup"><span data-stu-id="a2649-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="a2649-104">Ten skrypt tworzy grupę zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="a2649-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="a2649-105">Menedżera ruchu kieruje ruch toohello aplikacji w jeden region jako hello regionu podstawowego, a region pomocniczy toohello, gdy aplikacja hello w regionie podstawowym hello jest niedostępna.</span><span class="sxs-lookup"><span data-stu-id="a2649-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="a2649-106">Przed wykonaniem skryptu hello, musisz zmienić hello MyWebApp, MyWebAppL1 i MyWebAppL2 wartości toounique wartości w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2649-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="a2649-107">Po uruchomieniu skryptu hello, można uzyskać dostępu do aplikacji hello w regionie podstawowym hello z hello mywebapp.trafficmanager.net adresu URL.</span><span class="sxs-lookup"><span data-stu-id="a2649-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a2649-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a2649-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a><span data-ttu-id="a2649-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a2649-109">Clean up deployment</span></span> 

<span data-ttu-id="a2649-110">Po uruchomieniu przykładowym skrypcie hello hello wykonaj polecenie może być grupy zasobów hello tooremove używanych aplikacji usługi app Service i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="a2649-110">After hello script sample has been run, hello follow command can be used tooremove hello resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="a2649-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a2649-111">Script explanation</span></span>

<span data-ttu-id="a2649-112">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, profilu Menedżera ruchu, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="a2649-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="a2649-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="a2649-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a2649-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a2649-114">Command</span></span> | <span data-ttu-id="a2649-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a2649-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a2649-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="a2649-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a2649-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="a2649-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a2649-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="a2649-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a2649-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="a2649-119">Creates an App Service plan.</span></span> <span data-ttu-id="a2649-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a2649-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="a2649-121">Utwórz az appservice w sieci web</span><span class="sxs-lookup"><span data-stu-id="a2649-121">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="a2649-122">Tworzy aplikację sieci web platformy Azure w ramach hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="a2649-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="a2649-123">Utwórz profil Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="a2649-123">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="a2649-124">Tworzy profil Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="a2649-124">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="a2649-125">Tworzenie punktu końcowego Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="a2649-125">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="a2649-126">Dodaje tooan punktu końcowego profilu Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="a2649-126">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a2649-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a2649-127">Next steps</span></span>

<span data-ttu-id="a2649-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a2649-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a2649-129">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [Azure Networking dokumentacji](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a2649-129">Additional App Service CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
