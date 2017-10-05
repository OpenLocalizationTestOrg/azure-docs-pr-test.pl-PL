---
title: "Przykładowy skrypt programu PowerShell Azure - port otwartej aplikacji w usłudze równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell - Otwórz port w usłudze równoważenia obciążenia Azure dla aplikacji sieci szkieletowej usług."
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
ms.date: 08/15/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: 2958bdef0889076249918608c04c66678fa80b97
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="open-an-application-port-in-the-azure-load-balancer"></a><span data-ttu-id="f6205-103">Otwórz port aplikacji w usłudze równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="f6205-103">Open an application port in the Azure load balancer</span></span>

<span data-ttu-id="f6205-104">Aplikacji usługi Service Fabric, działające na platformie Azure znajduje się za usługą równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="f6205-104">A Service Fabric application running in Azure sits behind the Azure load balancer.</span></span> <span data-ttu-id="f6205-105">Ten przykładowy skrypt otwiera port do modułu równoważenia obciążenia Azure, dzięki czemu aplikacji usługi Service Fabric może komunikować się z klientami zewnętrznymi.</span><span class="sxs-lookup"><span data-stu-id="f6205-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="f6205-106">Dostosuj parametry zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="f6205-106">Customize the parameters as needed.</span></span> 

<span data-ttu-id="f6205-107">Jeśli to konieczne, Zainstaluj moduł programu PowerShell usługi Service Fabric [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f6205-107">If needed, install the Service Fabric PowerShell module with the [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f6205-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f6205-108">Sample script</span></span>

<span data-ttu-id="f6205-109">[!code-powershell[główne](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "otwarcie portu w usłudze równoważenia obciążenia")]</span><span class="sxs-lookup"><span data-stu-id="f6205-109">[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in the load balancer")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="f6205-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f6205-110">Script explanation</span></span>

<span data-ttu-id="f6205-111">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="f6205-111">This script uses the following commands.</span></span> <span data-ttu-id="f6205-112">Każde polecenie w tabeli łącza do dokumentacji specyficzne dla polecenia.</span><span class="sxs-lookup"><span data-stu-id="f6205-112">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="f6205-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f6205-113">Command</span></span> | <span data-ttu-id="f6205-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f6205-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f6205-115">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f6205-115">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="f6205-116">Pobiera zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f6205-116">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="f6205-117">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="f6205-117">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="f6205-118">Pobiera moduł równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="f6205-118">Gets the Azure load balancer.</span></span> |
| [<span data-ttu-id="f6205-119">Dodaj AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="f6205-119">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="f6205-120">Dodaje konfiguracji sondowania z modułem równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="f6205-120">Adds a probe configuration to a load balancer.</span></span>|
| [<span data-ttu-id="f6205-121">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="f6205-121">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="f6205-122">Pobiera konfigurację sondę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="f6205-122">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="f6205-123">Dodaj AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="f6205-123">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="f6205-124">Dodaje konfiguracji reguły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="f6205-124">Adds a rule configuration to a load balancer.</span></span> |
| [<span data-ttu-id="f6205-125">Zestaw AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="f6205-125">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="f6205-126">Ustawia stan celem usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="f6205-126">Sets the goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f6205-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f6205-127">Next steps</span></span>

<span data-ttu-id="f6205-128">Aby uzyskać więcej informacji dotyczących modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f6205-128">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f6205-129">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f6205-129">Additional Powershell samples for Azure Service Fabric can be found in the [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
