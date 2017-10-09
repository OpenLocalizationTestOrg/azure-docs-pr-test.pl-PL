---
title: "Przykładowy skrypt programu PowerShell — kierować ruchem wysokiej dostępności aplikacji aaaAzure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 11d15780403b4ed79e85d7b3495bc5d674bfdaee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a><span data-ttu-id="6c3e0-103">Kierować ruchem wysoką dostępność aplikacji</span><span class="sxs-lookup"><span data-stu-id="6c3e0-103">Route traffic for high availability of applications</span></span>

<span data-ttu-id="6c3e0-104">Ten skrypt tworzy grupę zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-104">This script creates a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="6c3e0-105">Menedżera ruchu kieruje ruch toohello aplikacji w jeden region jako hello regionu podstawowego, a region pomocniczy toohello, gdy aplikacja hello w regionie podstawowym hello jest niedostępna.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-105">Traffic Manager directs traffic toohello application in one region as hello primary region, and toohello secondary region when hello application in hello primary region is unavailable.</span></span> <span data-ttu-id="6c3e0-106">Przed wykonaniem skryptu hello, musisz zmienić hello MyWebApp, MyWebAppL1 i MyWebAppL2 wartości toounique wartości w obrębie platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-106">Before executing hello script, you must change hello MyWebApp, MyWebAppL1 and MyWebAppL2 values toounique values across Azure.</span></span> <span data-ttu-id="6c3e0-107">Po uruchomieniu skryptu hello, można uzyskać dostępu do aplikacji hello w regionie podstawowym hello z hello mywebapp.trafficmanager.net adresu URL.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-107">After running hello script, you can access hello app in hello primary region with hello URL mywebapp.trafficmanager.net.</span></span>

<span data-ttu-id="6c3e0-108">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="6c3e0-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6c3e0-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.ps1 "Route traffic for high availability")]


<span data-ttu-id="6c3e0-110">Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup1
Remove-AzureRmResourceGroup -Name myResourceGroup2
```


## <a name="script-explanation"></a><span data-ttu-id="6c3e0-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6c3e0-111">Script explanation</span></span>

<span data-ttu-id="6c3e0-112">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, profilu Menedżera ruchu, a wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-112">This script uses hello following commands toocreate a resource group, web app, traffic manager profile, and all related resources.</span></span> <span data-ttu-id="6c3e0-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6c3e0-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6c3e0-114">Command</span></span> | <span data-ttu-id="6c3e0-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6c3e0-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c3e0-116">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6c3e0-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="6c3e0-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c3e0-118">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6c3e0-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6c3e0-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-119">Creates an App Service plan.</span></span> <span data-ttu-id="6c3e0-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6c3e0-121">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6c3e0-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6c3e0-122">Tworzy aplikację sieci web platformy Azure w ramach hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-122">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="6c3e0-123">Zestaw AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="6c3e0-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/new-azurermresource) | <span data-ttu-id="6c3e0-124">Tworzy aplikację sieci web platformy Azure w ramach hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-124">Creates an Azure web app within hello App Service plan.</span></span> |
| [<span data-ttu-id="6c3e0-125">Nowe AzureRmTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="6c3e0-125">New-AzureRmTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="6c3e0-126">Tworzy profil Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-126">Creates an Azure Traffic Manager profile.</span></span> |
| [<span data-ttu-id="6c3e0-127">Nowe AzureRmTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="6c3e0-127">New-AzureRmTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="6c3e0-128">Dodaje tooan punktu końcowego profilu Menedżera ruchu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c3e0-128">Adds a endpoint tooan Azure Traffic Manager Profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c3e0-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c3e0-129">Next steps</span></span>

<span data-ttu-id="6c3e0-130">Aby uzyskać więcej informacji na powitania programu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c3e0-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="6c3e0-131">Dodatkowe przykłady skryptów PowerShell sieci można znaleźć w hello [Azure Przegląd dokumentacji](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c3e0-131">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
