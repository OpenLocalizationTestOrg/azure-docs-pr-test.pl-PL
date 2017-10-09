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
# <a name="open-an-application-port-in-hello-azure-load-balancer"></a>Otwórz port aplikacji w usłudze równoważenia obciążenia Azure hello

Aplikacji usługi Service Fabric, działające na platformie Azure znajduje się za usługą równoważenia obciążenia Azure hello. Ten przykładowy skrypt otwiera port do modułu równoważenia obciążenia Azure, dzięki czemu aplikacji usługi Service Fabric może komunikować się z klientami zewnętrznymi. Dostosuj parametry hello zgodnie z potrzebami. 

W razie potrzeby Zainstaluj moduł programu PowerShell usługi Service Fabric hello z hello [zestawu SDK usług sieci szkieletowej](../service-fabric-get-started.md). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-powershell[main](../../../powershell_scripts/service-fabric/open-port-in-load-balancer/open-port-in-load-balancer.ps1 "Open a port in hello load balancer")]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Get-AzureRmResource](/powershell/module/azurerm.resources/get-azurermresource) | Pobiera zasobów platformy Azure.  |
| [Get-AzureRmLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer) | Pobiera moduł równoważenia obciążenia Azure hello. |
| [Dodaj AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig) | Dodaje usługę równoważenia obciążenia badania konfiguracji tooa.|
| [Get-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/get-azurermloadbalancerprobeconfig) | Pobiera konfigurację sondę modułu równoważenia obciążenia. |
| [Dodaj AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig) | Dodaje regułę równoważenia obciążenia tooa konfiguracji. |
| [Zestaw AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer) | Ustawia hello celem stanu usługi równoważenia obciążenia. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania modułu Azure PowerShell, zobacz [dokumentacji programu Azure PowerShell](/powershell/azure/overview).

Dodatkowe przykłady środowiska Powershell dla usługi sieć szkieletowa usług Azure można znaleźć w hello [przykłady programu Azure PowerShell](../service-fabric-powershell-samples.md).
