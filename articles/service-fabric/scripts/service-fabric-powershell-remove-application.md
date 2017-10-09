---
title: "aaaAzure przykładowym skrypcie programu PowerShell — Usuń aplikację z klastra | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell — Usuń aplikację z klastra usługi sieć szkieletowa usług."
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
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 3fe2082c2fbeffbff1622f206021d4d907197d19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a><span data-ttu-id="83f0f-103">Usuń aplikację z klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="83f0f-103">Remove an application from a Service Fabric cluster</span></span>

<span data-ttu-id="83f0f-104">Ten przykładowy skrypt usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług, wyrejestrowuje typ i wersja aplikacji z klastra hello i usuwa pakiet aplikacji hello z magazynu obrazu klastra hello.</span><span class="sxs-lookup"><span data-stu-id="83f0f-104">This sample script deletes a running Service Fabric application instance, unregisters an application type and version from hello cluster, and deletes hello application package from hello cluster image store.</span></span>  <span data-ttu-id="83f0f-105">Trwa usuwanie wystąpienia aplikacji hello spowoduje również usunięcie hello wszystkie uruchomione wystąpienia usługi skojarzoną z daną aplikacją.</span><span class="sxs-lookup"><span data-stu-id="83f0f-105">Deleting hello application instance also deletes all hello running service instances associated with that application.</span></span> <span data-ttu-id="83f0f-106">Dostosuj parametry hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="83f0f-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="83f0f-107">W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="83f0f-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="83f0f-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="83f0f-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/remove-application/remove-application.ps1 "Remove an application from a cluster")]

## <a name="script-explanation"></a><span data-ttu-id="83f0f-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="83f0f-109">Script explanation</span></span>

<span data-ttu-id="83f0f-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="83f0f-110">This script uses hello following commands.</span></span> <span data-ttu-id="83f0f-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="83f0f-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="83f0f-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="83f0f-112">Command</span></span> | <span data-ttu-id="83f0f-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="83f0f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="83f0f-114">Usuń ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="83f0f-114">Remove-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="83f0f-115">Usuwa uruchomione wystąpienie aplikacji sieci szkieletowej usług z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="83f0f-115">Removes a running Service Fabric application instance from hello cluster.</span></span>  |
| [<span data-ttu-id="83f0f-116">Wyrejestruj ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="83f0f-116">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="83f0f-117">Wyrejestrowuje sieci szkieletowej usług typ i wersja aplikacji z hello klastra.</span><span class="sxs-lookup"><span data-stu-id="83f0f-117">Unregisters a Service Fabric application type and version from hello cluster.</span></span> |
| [<span data-ttu-id="83f0f-118">Usuń ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="83f0f-118">Remove-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="83f0f-119">Usuwa pakiet aplikacji sieci szkieletowej usług z hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="83f0f-119">Removes a Service Fabric application package from hello image store.</span></span>|

## <a name="next-steps"></a><span data-ttu-id="83f0f-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83f0f-120">Next steps</span></span>

<span data-ttu-id="83f0f-121">Aby uzyskać więcej informacji na powitania modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="83f0f-121">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="83f0f-122">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="83f0f-122">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
