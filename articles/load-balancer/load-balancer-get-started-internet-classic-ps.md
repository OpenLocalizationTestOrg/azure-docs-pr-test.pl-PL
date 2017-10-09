---
title: "Moduł równoważenia - obciążenia aaaCreate internetowy, klasycznym Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usługa równoważenia w trybie klasycznym przy użyciu programu PowerShell obciążenia toocreate umożliwiających dostęp z Internetu"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a><span data-ttu-id="ff48d-103">Wprowadzenie do tworzenia dostępnego z Internetu modułu równoważenia obciążenia (klasycznego) przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff48d-103">Get started creating an Internet facing load balancer (classic) in PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff48d-104">Klasyczna witryna Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ff48d-104">Azure classic portal</span></span>](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [<span data-ttu-id="ff48d-105">Program PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff48d-105">PowerShell</span></span>](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [<span data-ttu-id="ff48d-106">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="ff48d-106">Azure CLI</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [<span data-ttu-id="ff48d-107">Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="ff48d-107">Azure Cloud Services</span></span>](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="ff48d-108">Przed rozpoczęciem pracy z zasobów platformy Azure, jest ważne toounderstand, że Azure ma obecnie dwa modele wdrażania: usługi Azure Resource Manager i model klasyczny.</span><span class="sxs-lookup"><span data-stu-id="ff48d-108">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="ff48d-109">Przed rozpoczęciem pracy z dowolnym zasobem Azure należy zapoznać się z [modelami i narzędziami wdrażania](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="ff48d-109">Make sure you understand [deployment models and tools](../azure-classic-rm.md) before you work with any Azure resource.</span></span> <span data-ttu-id="ff48d-110">Hello dokumentację dotyczącą różnych narzędzi można wyświetlić, klikając karty hello u góry hello tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="ff48d-110">You can view hello documentation for different tools by clicking hello tabs at hello top of this article.</span></span> <span data-ttu-id="ff48d-111">W tym artykule omówiono hello klasycznego modelu wdrażania.</span><span class="sxs-lookup"><span data-stu-id="ff48d-111">This article covers hello classic deployment model.</span></span> <span data-ttu-id="ff48d-112">Możesz również [Dowiedz się, jak usługa równoważenia przy użyciu usługi Azure Resource Manager obciążenia toocreate Internetem](load-balancer-get-started-internet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="ff48d-112">You can also [Learn how toocreate an Internet facing load balancer using Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).</span></span>

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a><span data-ttu-id="ff48d-113">Konfiguracja modułu równoważenia obciążenia za pomocą programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="ff48d-113">Set up load balancer using PowerShell</span></span>

<span data-ttu-id="ff48d-114">tooset się moduł równoważenia obciążenia przy użyciu programu powershell, wykonaj poniższe kroki hello:</span><span class="sxs-lookup"><span data-stu-id="ff48d-114">tooset up a load balancer using powershell, follow hello steps below:</span></span>

1. <span data-ttu-id="ff48d-115">Jeśli nie znasz programu Azure PowerShell, zobacz [jak tooInstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) i wykonaj instrukcje hello wszystkich toohello sposób hello kończyć toosign na platformie Azure i wyboru subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="ff48d-115">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="ff48d-116">Po utworzeniu maszyny wirtualnej, można użyć tooadd poleceń cmdlet programu PowerShell maszyny wirtualnej tooa usługi równoważenia obciążenia w ramach hello sama usługa w chmurze.</span><span class="sxs-lookup"><span data-stu-id="ff48d-116">After creating a virtual machine, you can use PowerShell cmdlets tooadd a load balancer tooa virtual machine within hello same cloud service.</span></span>

<span data-ttu-id="ff48d-117">W hello następujące przykładowe, należy dodać zestaw usługi równoważenia obciążenia o nazwie "farma sieci Web" toocloud maszyny "mytestcloud" (lub myctestcloud.cloudapp.net), dodając toovirtual usługi równoważenia obciążenia hello hello punktów końcowych usługi o nazwie "web1" i "Web 2".</span><span class="sxs-lookup"><span data-stu-id="ff48d-117">In hello following example you will add a load balancer set called "webfarm" toocloud service "mytestcloud" (or myctestcloud.cloudapp.net) , adding hello endpoints for hello load balancer toovirtual machines named "web1" and "web2".</span></span> <span data-ttu-id="ff48d-118">Witaj modułu równoważenia obciążenia odbiera ruch sieciowy na porcie 80 i równoważy obciążenia między maszynami wirtualnymi hello zdefiniowane przez hello lokalnego punktu końcowego (w tym przypadku port 80) za pomocą protokołu TCP.</span><span class="sxs-lookup"><span data-stu-id="ff48d-118">hello load balancer receives network traffic on port 80 and load balances between hello virtual machines defined by hello local endpoint (in this case port 80) using TCP.</span></span>

### <a name="step-1"></a><span data-ttu-id="ff48d-119">Krok 1</span><span class="sxs-lookup"><span data-stu-id="ff48d-119">Step 1</span></span>

<span data-ttu-id="ff48d-120">Tworzenie punktu końcowego ze zrównoważonym obciążeniem na serwerze web1"hello pierwszej maszyny Wirtualnej"</span><span class="sxs-lookup"><span data-stu-id="ff48d-120">Create a load balanced endpoint for hello first VM "web1"</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a><span data-ttu-id="ff48d-121">Krok 2</span><span class="sxs-lookup"><span data-stu-id="ff48d-121">Step 2</span></span>

<span data-ttu-id="ff48d-122">Utwórz inny punkt końcowy dla hello drugi maszyny Wirtualnej "sieci Web 2" przy użyciu hello sama nazwa zestawu równoważenia</span><span class="sxs-lookup"><span data-stu-id="ff48d-122">Create another endpoint for hello second VM  "web2" using hello same load balancer set name</span></span>

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a><span data-ttu-id="ff48d-123">Usuwanie maszyny wirtualnej z modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="ff48d-123">Remove a virtual machine from a load balancer</span></span>

<span data-ttu-id="ff48d-124">Można użyć tooremove AzureEndpoint Usuń punkt końcowy maszyny wirtualnej z hello modułu równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="ff48d-124">You can use Remove-AzureEndpoint tooremove a virtual machine endpoint from hello load balancer</span></span>

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a><span data-ttu-id="ff48d-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ff48d-125">Next steps</span></span>

<span data-ttu-id="ff48d-126">Możesz też zapoznać się z artykułem na temat [wprowadzenia do tworzenia wewnętrznego modułu równoważenia obciążenia](load-balancer-get-started-ilb-classic-ps.md) i określić typ [trybu dystrybucji](load-balancer-distribution-mode.md) dotyczącego danego ruchu sieciowego modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="ff48d-126">You can also [get started creating an internal load balancer](load-balancer-get-started-ilb-classic-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="ff48d-127">Jeśli aplikacja wymaga połączenia tookeep aktywności dla serwerów za modułem równoważenia obciążenia, użytkownik może dowiedzieć się więcej o [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="ff48d-127">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="ff48d-128">Aby ułatwić toolearn dotyczących zachowania bezczynności połączenia podczas korzystania z usługi równoważenia obciążenia Azure.</span><span class="sxs-lookup"><span data-stu-id="ff48d-128">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
