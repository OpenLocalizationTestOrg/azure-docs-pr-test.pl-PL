---
title: "Przykładowy skrypt programu PowerShell Azure - uaktualniania aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell — uaktualnienie aplikacji sieci szkieletowej usług."
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 454849f82ddb23ddb9d71459f86e3cf5a1589254
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="28f17-103">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="28f17-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="28f17-104">Ten przykładowy skrypt uaktualnia uruchomione wystąpienie aplikacji sieci szkieletowej usług do wersji 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="28f17-104">This sample script upgrades a running Service Fabric application instance to version 1.3.0.</span></span> <span data-ttu-id="28f17-105">Skrypt kopiuje nowy pakiet aplikacji do magazynu obrazu klastra, rejestruje typ aplikacji, rozpoczyna się uaktualnienie monitorowanych i stale sprawdza stan uaktualnienia, aż do uaktualnienia ukończenia lub wycofuje.</span><span class="sxs-lookup"><span data-stu-id="28f17-105">The script copies the new application package to the cluster image store, registers the application type, starts a monitored upgrade, and continuously checks the upgrade status until the upgrade completes or rolls back.</span></span> <span data-ttu-id="28f17-106">Dostosuj parametry zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="28f17-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="28f17-107">Jeśli to konieczne, Zainstaluj moduł programu PowerShell usługi Service Fabric [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="28f17-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="28f17-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="28f17-108">Sample script</span></span>

<span data-ttu-id="28f17-109">[!code-powershell[główne](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "uaktualnianie aplikacji")]</span><span class="sxs-lookup"><span data-stu-id="28f17-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="28f17-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="28f17-110">Script explanation</span></span>

<span data-ttu-id="28f17-111">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="28f17-111">This script uses the following commands.</span></span> <span data-ttu-id="28f17-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="28f17-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="28f17-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="28f17-113">Command</span></span> | <span data-ttu-id="28f17-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="28f17-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="28f17-115">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="28f17-115">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="28f17-116">Pobiera wszystkie aplikacje w klastrze usługi sieć szkieletowa usług lub określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28f17-116">Gets all the applications in the Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="28f17-117">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="28f17-117">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="28f17-118">Pobiera stan uaktualniania aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="28f17-118">Gets the status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="28f17-119">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="28f17-119">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="28f17-120">Pobiera typy aplikacji usługi sieć szkieletowa zarejestrowany w klastrze usługi sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="28f17-120">Gets the Service Fabric application types registered on the Service Fabric cluster.</span></span> |
| [<span data-ttu-id="28f17-121">Wyrejestruj ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="28f17-121">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="28f17-122">Wyrejestrowuje typ aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="28f17-122">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="28f17-123">Kopiowanie ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="28f17-123">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="28f17-124">Kopiuje pakiet aplikacji usługi sieci szkieletowej magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="28f17-124">Copies a Service Fabric application package to the image store.</span></span>  |
| [<span data-ttu-id="28f17-125">Rejestr ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="28f17-125">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="28f17-126">Rejestruje typ aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="28f17-126">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="28f17-127">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="28f17-127">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="28f17-128">Uaktualnia aplikacji usługi Service Fabric, do wersji typu określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="28f17-128">Upgrades a Service Fabric application to the specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="28f17-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28f17-129">Next steps</span></span>

<span data-ttu-id="28f17-130">Aby uzyskać więcej informacji na modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="28f17-130">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="28f17-131">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="28f17-131">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
