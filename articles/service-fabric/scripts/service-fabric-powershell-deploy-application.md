---
title: "aaaAzure przykładowy skrypt programu PowerShell — wdrożenie aplikacji tooa klastra | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — wdrażanie klastra usługi sieć szkieletowa tooa aplikacji."
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
ms.openlocfilehash: b417c9908c72f016e930c43ff2d13e0cc5451f46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a><span data-ttu-id="d976d-103">Wdrażanie klastra usługi sieć szkieletowa tooa aplikacji</span><span class="sxs-lookup"><span data-stu-id="d976d-103">Deploy an application tooa Service Fabric cluster</span></span>

<span data-ttu-id="d976d-104">Ten przykładowy skrypt kopiuje pakiet tooa klastra obrazu sklepu z aplikacjami, rejestruje typ aplikacji hello w klastrze hello i tworzy wystąpienie aplikacji na podstawie typu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="d976d-104">This sample script copies an application package tooa cluster image store, registers hello application type in hello cluster, and creates an application instance from hello application type.</span></span>  <span data-ttu-id="d976d-105">Jeśli wszystkie domyślne usługi zostały zdefiniowane w manifeście aplikacji hello typu aplikacji docelowej hello, te usługi są tworzone w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="d976d-105">If any default services were defined in hello application manifest of hello target application type, then those services are created at this time.</span></span> <span data-ttu-id="d976d-106">Dostosuj parametry hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="d976d-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="d976d-107">W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d976d-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d976d-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="d976d-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d976d-109">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="d976d-109">Clean up deployment</span></span> 

<span data-ttu-id="d976d-110">Po uruchomieniu przykładowym skrypcie hello hello skryptu w [usuwania aplikacji](service-fabric-powershell-remove-application.md) można instancji aplikacji hello tooremove używane, wyrejestrowywanie typu aplikacji hello i usunąć pakiet aplikacji hello z hello magazynu obrazów.</span><span class="sxs-lookup"><span data-stu-id="d976d-110">After hello script sample has been run, hello script in [Remove an application](service-fabric-powershell-remove-application.md) can be used tooremove hello application instance, unregister hello application type, and delete hello application package from hello image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="d976d-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="d976d-111">Script explanation</span></span>

<span data-ttu-id="d976d-112">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="d976d-112">This script uses hello following commands.</span></span> <span data-ttu-id="d976d-113">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="d976d-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d976d-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="d976d-114">Command</span></span> | <span data-ttu-id="d976d-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="d976d-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d976d-116">Kopiowanie ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="d976d-116">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="d976d-117">Skopiuj pakiet toohello klastra obrazu sklepu z aplikacjami.</span><span class="sxs-lookup"><span data-stu-id="d976d-117">Copy an application package toohello cluster image store.</span></span>  |
|[<span data-ttu-id="d976d-118">Rejestr ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="d976d-118">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="d976d-119">Rejestruje typ i wersja aplikacji w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="d976d-119">Registers an application type and version on hello cluster.</span></span> |
|[<span data-ttu-id="d976d-120">Nowe ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="d976d-120">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="d976d-121">Tworzy aplikację z typ zarejestrowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d976d-121">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d976d-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d976d-122">Next steps</span></span>

<span data-ttu-id="d976d-123">Aby uzyskać więcej informacji na powitania modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="d976d-123">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="d976d-124">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d976d-124">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
