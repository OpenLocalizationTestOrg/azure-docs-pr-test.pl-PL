---
title: "Przykładowy skrypt programu PowerShell - aaaAzure skalowanie aplikacji sieci web na całym świecie z architekturą wysokiej dostępności | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt programu PowerShell Azure - skalowanie aplikacji sieci web na całym świecie z architekturą wysokiej dostępności"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="b2258-103">Skalowanie aplikacji sieci web na całym świecie z architekturą wysokiej dostępności</span><span class="sxs-lookup"><span data-stu-id="b2258-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="b2258-104">W tym scenariuszu utworzysz, grupy zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="b2258-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="b2258-105">Po zakończeniu wykonywania hello będą miały o wysokiej dostępności architekturę, dzięki czemu zapewnia globalną dostępność aplikacji sieci web oparta na powitania najniższe opóźnienia sieci.</span><span class="sxs-lookup"><span data-stu-id="b2258-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="b2258-106">W razie potrzeby zainstaluj hello Azure PowerShell przy użyciu instrukcji hello znalezione w hello [Przewodnik programu Azure PowerShell](/powershell/azure/overview), a następnie uruchom `Login-AzureRmAccount` toocreate połączenia z platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="b2258-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="b2258-107">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b2258-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b2258-108">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="b2258-108">Clean up deployment</span></span> 

<span data-ttu-id="b2258-109">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="b2258-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="b2258-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b2258-110">Script explanation</span></span>

<span data-ttu-id="b2258-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="b2258-111">This script uses hello following commands.</span></span> <span data-ttu-id="b2258-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b2258-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b2258-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b2258-113">Command</span></span> | <span data-ttu-id="b2258-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b2258-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b2258-115">Nowe AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b2258-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b2258-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b2258-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b2258-117">Nowe AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="b2258-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="b2258-118">Tworzy profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="b2258-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="b2258-119">Nowe AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="b2258-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="b2258-120">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b2258-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="b2258-121">Nowe AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="b2258-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="b2258-122">Tworzy aplikację sieci web.</span><span class="sxs-lookup"><span data-stu-id="b2258-122">Creates a web app.</span></span> |
| [<span data-ttu-id="b2258-123">Nowe AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="b2258-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="b2258-124">Tworzy punkt końcowy profilu Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="b2258-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b2258-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b2258-125">Next steps</span></span>

<span data-ttu-id="b2258-126">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b2258-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b2258-127">Dodatkowe przykłady programu Azure Powershell dla aplikacji sieci Web usługi aplikacji Azure można znaleźć w hello [przykłady programu Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b2258-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
