---
title: "Przykładowy skrypt programu PowerShell - aaaAzure uaktualniania aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 4f4777607bd6b35a76029e09ddb441006565d4cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-a-service-fabric-application"></a><span data-ttu-id="33103-103">Uaktualnianie aplikacji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="33103-103">Upgrade a Service Fabric application</span></span>

<span data-ttu-id="33103-104">Ten przykładowy skrypt uaktualnia uruchomionej usługi sieć szkieletowa usług aplikacji wystąpienia tooversion 1.3.0.</span><span class="sxs-lookup"><span data-stu-id="33103-104">This sample script upgrades a running Service Fabric application instance tooversion 1.3.0.</span></span> <span data-ttu-id="33103-105">skrypt Hello kopiuje hello nowego pakietu toohello klastra obrazu sklepu z aplikacjami, rejestruje typ aplikacji hello uruchamia monitorowanych uaktualnienia i stale sprawdza stan uaktualnienia hello aż do ukończenia uaktualnienia hello, lub wycofuje.</span><span class="sxs-lookup"><span data-stu-id="33103-105">hello script copies hello new application package toohello cluster image store, registers hello application type, starts a monitored upgrade, and continuously checks hello upgrade status until hello upgrade completes or rolls back.</span></span> <span data-ttu-id="33103-106">Dostosuj parametry hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="33103-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="33103-107">W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="33103-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="33103-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="33103-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/upgrade-application/upgrade-application.ps1 "Upgrade an application")]

## <a name="script-explanation"></a><span data-ttu-id="33103-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="33103-109">Script explanation</span></span>

<span data-ttu-id="33103-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="33103-110">This script uses hello following commands.</span></span> <span data-ttu-id="33103-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="33103-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="33103-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="33103-112">Command</span></span> | <span data-ttu-id="33103-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="33103-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="33103-114">Get-ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="33103-114">Get-ServiceFabricApplication</span></span>](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) | <span data-ttu-id="33103-115">Pobiera wszystkich aplikacji hello w hello klastra sieci szkieletowej usług lub określonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33103-115">Gets all hello applications in hello Service Fabric cluster or a specific application.</span></span>  |
| [<span data-ttu-id="33103-116">Get-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="33103-116">Get-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="33103-117">Pobiera stan hello uaktualniania aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="33103-117">Gets hello status of a Service Fabric application upgrade.</span></span> |
| [<span data-ttu-id="33103-118">Get-ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="33103-118">Get-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="33103-119">Pobiera typy aplikacji usługi sieć szkieletowa hello zarejestrowany w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="33103-119">Gets hello Service Fabric application types registered on hello Service Fabric cluster.</span></span> |
| [<span data-ttu-id="33103-120">Wyrejestruj ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="33103-120">Unregister-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="33103-121">Wyrejestrowuje typ aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="33103-121">Unregisters a Service Fabric application type.</span></span>  |
| [<span data-ttu-id="33103-122">Kopiowanie ServiceFabricApplicationPackage</span><span class="sxs-lookup"><span data-stu-id="33103-122">Copy-ServiceFabricApplicationPackage</span></span>](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) | <span data-ttu-id="33103-123">Kopie przechowywania obrazu toohello pakietu sieci szkieletowej usług aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33103-123">Copies a Service Fabric application package toohello image store.</span></span>  |
| [<span data-ttu-id="33103-124">Rejestr ServiceFabricApplicationType</span><span class="sxs-lookup"><span data-stu-id="33103-124">Register-ServiceFabricApplicationType</span></span>](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) | <span data-ttu-id="33103-125">Rejestruje typ aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="33103-125">Registers a Service Fabric application type.</span></span> |
| [<span data-ttu-id="33103-126">Start-ServiceFabricApplicationUpgrade</span><span class="sxs-lookup"><span data-stu-id="33103-126">Start-ServiceFabricApplicationUpgrade</span></span>](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) | <span data-ttu-id="33103-127">Uaktualnia wersję typu sieci szkieletowej usług aplikacji toohello określonej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="33103-127">Upgrades a Service Fabric application toohello specified application type version.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="33103-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33103-128">Next steps</span></span>

<span data-ttu-id="33103-129">Aby uzyskać więcej informacji na powitania modułu programu PowerShell usługi Service Fabric, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/service-fabric/?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="33103-129">For more information on hello Service Fabric PowerShell module, see [Azure PowerShell documentation](/powershell/azure/service-fabric/?view=azureservicefabricps).</span></span>

<span data-ttu-id="33103-130">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="33103-130">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
