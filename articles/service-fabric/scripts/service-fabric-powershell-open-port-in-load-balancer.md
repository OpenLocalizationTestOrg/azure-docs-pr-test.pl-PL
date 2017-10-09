---
title: "aaaAzure przykładowym skrypcie programu PowerShell — port otwartej aplikacji w usłudze równoważenia obciążenia | Dokumentacja firmy Microsoft"
description: "Azure przykładowy skrypt programu PowerShell - Otwórz port w usłudze równoważenia obciążenia Azure powitania dla aplikacji sieci szkieletowej usług."
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
ms.openlocfilehash: 6acb28942851dce63f89f7de362b7cf1dc7b1fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a><span data-ttu-id="ff3e1-103">Otwórz port aplikacji w usłudze równoważenia obciążenia Azure hello</span><span class="sxs-lookup"><span data-stu-id="ff3e1-103">Open an application port in hello Azure load balancer</span></span>

<span data-ttu-id="ff3e1-104">Aplikacji usługi Service Fabric, działające na platformie Azure znajduje się za usługą równoważenia obciążenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-104">A Service Fabric application running in Azure sits behind hello Azure load balancer.</span></span> <span data-ttu-id="ff3e1-105">Ten przykładowy skrypt otwiera port do modułu równoważenia obciążenia Azure, dzięki czemu aplikacji usługi Service Fabric może komunikować się z klientami zewnętrznymi.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-105">This sample script opens a port in an Azure load balancer so that a Service Fabric application can communicate with external clients.</span></span> <span data-ttu-id="ff3e1-106">Dostosuj parametry hello zgodnie z potrzebami.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-106">Customize hello parameters as needed.</span></span> 

<span data-ttu-id="ff3e1-107">W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ff3e1-107">If needed, install hello Service Fabric PowerShell module with hello [Service Fabric SDK](../service-fabric-get-started.md).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ff3e1-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ff3e1-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a><span data-ttu-id="ff3e1-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ff3e1-109">Script explanation</span></span>

<span data-ttu-id="ff3e1-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-110">This script uses hello following commands.</span></span> <span data-ttu-id="ff3e1-111">Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-111">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="ff3e1-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ff3e1-112">Command</span></span> | <span data-ttu-id="ff3e1-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ff3e1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ff3e1-114">Get-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="ff3e1-114">Get-AzureRmResource</span></span>](/powershell/module/azurerm.resources/get-azurermresource) | <span data-ttu-id="ff3e1-115">Pobiera zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-115">Gets an Azure resource.</span></span>  |
| [<span data-ttu-id="ff3e1-116">Get-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ff3e1-116">Get-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancer) | <span data-ttu-id="ff3e1-117">Pobiera moduł równoważenia obciążenia Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-117">Gets hello Azure load balancer.</span></span> |
| [<span data-ttu-id="ff3e1-118">Dodaj AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="ff3e1-118">Add-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | <span data-ttu-id="ff3e1-119">Dodaje usługę równoważenia obciążenia badania konfiguracji tooa.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-119">Adds a probe configuration tooa load balancer.</span></span>|
| [<span data-ttu-id="ff3e1-120">Get-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="ff3e1-120">Get-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | <span data-ttu-id="ff3e1-121">Pobiera konfigurację sondę modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-121">Gets a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="ff3e1-122">Dodaj AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="ff3e1-122">Add-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | <span data-ttu-id="ff3e1-123">Dodaje regułę równoważenia obciążenia tooa konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-123">Adds a rule configuration tooa load balancer.</span></span> |
| [<span data-ttu-id="ff3e1-124">Zestaw AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="ff3e1-124">Set-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/set-azurermloadbalancer) | <span data-ttu-id="ff3e1-125">Ustawia hello celem stanu usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ff3e1-125">Sets hello goal state for a load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ff3e1-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff3e1-126">Next steps</span></span>

<span data-ttu-id="ff3e1-127">Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ff3e1-127">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ff3e1-128">Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ff3e1-128">Additional Powershell samples for Azure Service Fabric can be found in hello [Azure PowerShell samples](../service-fabric-powershell-samples.md).</span></span>
