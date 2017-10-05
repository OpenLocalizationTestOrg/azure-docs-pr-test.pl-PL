---
title: "Skrypt programu PowerShell Azure Przykładowe — wdrożenie aplikacji do klastra | Dokumentacja firmy Microsoft"
description: "Skrypt programu PowerShell Azure przykładowe — wdrażanie aplikacji do klastra usługi sieć szkieletowa usług."
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
ms.openlocfilehash: 2863823205dbd70f63948ecd4af8898220fe1ff8
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a><span data-ttu-id="c8452-103">Wdrażanie aplikacji do klastra sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="c8452-103">Deploy an application to a Service Fabric cluster</span></span>

<span data-ttu-id="c8452-104">Ten przykładowy skrypt umożliwia skopiowanie pakietu aplikacji do magazynu obrazu klastra, rejestruje typ aplikacji w klastrze i tworzy wystąpienie aplikacji na podstawie typu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8452-104">This sample script copies an application package to a cluster image store, registers the application type in the cluster, and creates an application instance from the application type.</span></span>  <span data-ttu-id="c8452-105">Jeśli wszystkie domyślne usługi zostały zdefiniowane w manifeście aplikacji typu aplikacji docelowej, te usługi są tworzone w tym momencie.</span><span class="sxs-lookup"><span data-stu-id="c8452-105">If any default services were defined in the application manifest of the target application type, then those services are created at this time.</span></span> <span data-ttu-id="c8452-106">Dostosuj parametry zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="c8452-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="c8452-107">Jeśli to konieczne, Zainstaluj moduł programu PowerShell usługi Service Fabric [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c8452-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="c8452-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="c8452-108">Sample script</span></span>

<span data-ttu-id="c8452-109">[!code-powershell[główne](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "wdrażania aplikacji do klastra")]</span><span class="sxs-lookup"><span data-stu-id="c8452-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/deploy-application/deploy-application.ps1 "Deploy an application to a cluster")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c8452-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="c8452-110">Clean up deployment</span></span> 

<span data-ttu-id="c8452-111">Po przykładowym skrypcie zostało uruchomione, skrypt w [usuwania aplikacji](service-fabric-powershell-remove-application.md) można usunąć wystąpienia aplikacji, wyrejestrowywanie typu aplikacji i usuwanie pakietu aplikacji w magazynie obrazów.</span><span class="sxs-lookup"><span data-stu-id="c8452-111">After the script sample has been run, the script in [Remove an application](service-fabric-powershell-remove-application.md) can be used to remove the application instance, unregister the application type, and delete the application package from the image store.</span></span>

## <a name="script-explanation"></a><span data-ttu-id="c8452-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="c8452-112">Script explanation</span></span>

<span data-ttu-id="c8452-113">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="c8452-113">This script uses the following commands.</span></span> <span data-ttu-id="c8452-114">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="c8452-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c8452-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="c8452-115">Command</span></span> | <span data-ttu-id="c8452-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="c8452-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c8452-117">Kopiowanie ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="c8452-117">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="c8452-118">Skopiuj pakiet aplikacji do magazynu obrazu klastra.</span><span class="sxs-lookup"><span data-stu-id="c8452-118">Copy an application package to the cluster image store.</span></span>  |
|[<span data-ttu-id="c8452-119">Rejestr ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="c8452-119">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps)| <span data-ttu-id="c8452-120">Rejestruje typ i wersja aplikacji w klastrze.</span><span class="sxs-lookup"><span data-stu-id="c8452-120">Registers an application type and version on the cluster.</span></span> |
|[<span data-ttu-id="c8452-121">Nowe ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="c8452-121">New-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps)| <span data-ttu-id="c8452-122">Tworzy aplikację z typ zarejestrowanych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c8452-122">Creates an application from a registered application type.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c8452-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c8452-123">Next steps</span></span>

<span data-ttu-id="c8452-124">Aby uzyskać więcej informacji na modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="c8452-124">For more information on the Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="c8452-125">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c8452-125">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
