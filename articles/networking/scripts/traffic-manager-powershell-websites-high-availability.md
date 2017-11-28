---
title: "Przykładowy skrypt programu PowerShell Azure - kierować ruchem wysoką dostępność aplikacji | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - kierować ruchem wysoką dostępność aplikacji"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: georgewallace
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 2f0ac4fd1779661aab04bafb217e64af5d619a2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="54e04-103">Kierować ruchem wysoką dostępność aplikacji</span><span class="sxs-lookup"><span data-stu-id="54e04-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="54e04-104">Ten skrypt tworzy grupę zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="54e04-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="54e04-105">Menedżer ruchu kieruje ruch do aplikacji w jednym regionie jako regionu podstawowego, a w regionie pomocniczym, gdy aplikacja w regionie podstawowym jest niedostępny.</span><span class="sxs-lookup"><span data-stu-id="54e04-105">Traffic Manager directs traffic to the application in one region as the primary region, and to the secondary region when the application in the primary region is unavailable.</span></span> <span data-ttu-id="54e04-106">Przed wykonaniem skryptu, należy zmienić wartości MyWebApp, MyWebAppL1 i MyWebAppL2 unikatowych wartości na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="54e04-106">Before executing the script, you must change the MyWebApp, MyWebAppL1 and MyWebAppL2 values to unique values across Azure.</span></span> <span data-ttu-id="54e04-107">Po uruchomieniu skryptu, można uzyskać dostępu do aplikacji w regionie podstawowym z mywebapp.trafficmanager.net adresu URL.</span><span class="sxs-lookup"><span data-stu-id="54e04-107">After running the script, you can access the app in the primary region with the URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="54e04-108">W razie potrzeby zainstalować program Azure PowerShell przy użyciu instrukcji w [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` można utworzyć połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="54e04-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="54e04-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="54e04-109">Sample script</span></span>

<span data-ttu-id="54e04-110">[!code-powershell[główne](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "kierować ruchem w celu zapewnienia wysokiej dostępności")]</span><span class="sxs-lookup"><span data-stu-id="54e04-110">[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]</span></span>


<span data-ttu-id="54e04-111">Uruchom następujące polecenie, aby usunąć grupę zasobów, maszyny Wirtualnej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="54e04-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="54e04-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="54e04-112">Script explanation</span></span>

<span data-ttu-id="54e04-113">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web profilu Menedżera ruchu i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="54e04-113">This script uses the following commands to create a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="54e04-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="54e04-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="54e04-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="54e04-115">Command</span></span> | <span data-ttu-id="54e04-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="54e04-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="54e04-117">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="54e04-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="54e04-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="54e04-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="54e04-119">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="54e04-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="54e04-120">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="54e04-120">Creates an App Service plan.</span></span> <span data-ttu-id="54e04-121">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="54e04-121">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="54e04-122">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="54e04-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="54e04-123">Tworzy aplikację sieci web platformy Azure w ramach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54e04-123">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="54e04-124">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="54e04-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="54e04-125">Tworzy aplikację sieci web platformy Azure w ramach planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="54e04-125">Creates an Azure web app within the App Service plan.</span></span> |
| [<span data-ttu-id="54e04-126">Nowe AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="54e04-126">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="54e04-127">Tworzy profil Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="54e04-127">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="54e04-128">Nowe AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="54e04-128">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="54e04-129">Dodaje punkt końcowy profilu Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="54e04-129">Adds a endpoint to an Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="54e04-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="54e04-130">Next steps</span></span>

<span data-ttu-id="54e04-131">Aby uzyskać więcej informacji dotyczących programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="54e04-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="54e04-132">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="54e04-132">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>