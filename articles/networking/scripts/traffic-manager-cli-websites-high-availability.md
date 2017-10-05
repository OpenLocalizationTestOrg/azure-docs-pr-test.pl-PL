---
title: "Azure CLI przykładowym skrypcie - kierować ruchem wysoką dostępność aplikacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="b0775-103">Kierować ruchem wysoką dostępność aplikacji</span><span class="sxs-lookup"><span data-stu-id="b0775-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="b0775-104">Ten skrypt tworzy grupę zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="b0775-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="b0775-105">Menedżer ruchu kieruje ruch do aplikacji w jednym regionie jako regionu podstawowego, a w regionie pomocniczym, gdy aplikacja w regionie podstawowym jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="b0775-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="b0775-106">Przed wykonaniem skryptu, należy zmienić wartości MyWebApp, MyWebAppL1 i MyWebAppL2 unikatowych wartości na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="b0775-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="b0775-107">Po uruchomieniu skryptu, można uzyskać dostępu do aplikacji w regionie podstawowym z mywebapp.trafficmanager.net adresu URL.</span><span class="sxs-lookup"><span data-stu-id="b0775-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b0775-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b0775-108">Sample script</span></span>

<span data-ttu-id="b0775-109">[!code-azurecli-interactive[główne](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "kierować ruchem w celu zapewnienia wysokiej dostępności")]</span><span class="sxs-lookup"><span data-stu-id="b0775-109">[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="b0775-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b0775-110">Clean up deployment</span></span> 

<span data-ttu-id="b0775-111">Po uruchomieniu przykładowym skrypcie, wykonaj polecenie może służyć do usunięcia grupy zasobów, aplikacji usługi app Service i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="b0775-111">After the script sample has been run, the follow command can be used to remove the resource group, App Service app, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a><span data-ttu-id="b0775-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b0775-112">Script explanation</span></span>

<span data-ttu-id="b0775-113">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web profilu Menedżera ruchu i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="b0775-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="b0775-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="b0775-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b0775-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b0775-115">Command</span></span> | <span data-ttu-id="b0775-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b0775-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b0775-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="b0775-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b0775-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b0775-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b0775-119">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="b0775-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b0775-120">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b0775-120">Creates an App Service plan.</span></span> <span data-ttu-id="b0775-121">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b0775-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b0775-122">Utwórz az appservice w sieci web</span><span class="sxs-lookup"><span data-stu-id="b0775-122">az appservice web create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#create) | <span data-ttu-id="b0775-123">Tworzy aplikację sieci web platformy Azure w ramach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b0775-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="b0775-124">Utwórz profil Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="b0775-124">az network traffic-manager profile create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | <span data-ttu-id="b0775-125">Tworzy profil Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0775-125">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="b0775-126">Tworzenie punktu końcowego Menedżera ruchu sieciowego az</span><span class="sxs-lookup"><span data-stu-id="b0775-126">az network traffic-manager endpoint create</span></span>](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | <span data-ttu-id="b0775-127">Dodaje punkt końcowy profilu Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="b0775-127">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b0775-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b0775-128">Next steps</span></span>

<span data-ttu-id="b0775-129">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b0775-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b0775-130">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [Azure Networking dokumentacji](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b0775-130">Additional App Service CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>
