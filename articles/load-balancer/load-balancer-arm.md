---
title: "Obsługa Menedżera zasobów dla usługi równoważenia obciążenia aaaAzure | Dokumentacja firmy Microsoft"
description: "Przy użyciu programu powershell dla usługi równoważenia obciążenia z usługi Azure Resource Manager. Za pomocą szablonów usługi równoważenia obciążenia"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="e8938-104">Za pomocą techniczną platformy Azure Resource Manager z usługą równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="e8938-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="e8938-105">Usługa Azure Resource Manager jest hello preferowane framework dla usług Azure.</span><span class="sxs-lookup"><span data-stu-id="e8938-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="e8938-106">Moduł równoważenia obciążenia Azure mogą być zarządzane przy użyciu usługi Azure Resource Manager na podstawie interfejsów API i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="e8938-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="e8938-107">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="e8938-107">Concepts</span></span>

<span data-ttu-id="e8938-108">Usługa Resource Manager modułu równoważenia obciążenia Azure zawiera hello następujące zasoby podrzędne:</span><span class="sxs-lookup"><span data-stu-id="e8938-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="e8938-109">Konfiguracja IP frontonu — modułu równoważenia obciążenia może zawierać co najmniej jeden adres IP frontonu, znanej także jako wirtualnych adresów IP (VIP).</span><span class="sxs-lookup"><span data-stu-id="e8938-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="e8938-110">Te adresy IP stanowią wejściowych hello ruchu.</span><span class="sxs-lookup"><span data-stu-id="e8938-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="e8938-111">Pula adresów zaplecza — są to adresy IP skojarzone z maszyną wirtualną hello sieci karta sieciowa (NIC) będą dystrybuowane toowhich obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8938-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="e8938-112">Reguły równoważenia obciążenia — właściwości reguły mapowania IP frontonu danego portu kombinacja tooa zbiór adresów IP zaplecza i portu kombinacji.</span><span class="sxs-lookup"><span data-stu-id="e8938-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="e8938-113">Moduł równoważenia obciążenia może mieć różne reguły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8938-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="e8938-114">Każda reguła zawiera kombinację adresu IP frontonu i portu oraz adresu IP zaplecza i portu, które są powiązane z maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="e8938-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="e8938-115">Sond — sond Włącz możesz tookeep track hello kondycji wystąpień maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="e8938-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="e8938-116">W przypadku niepowodzenia sondy kondycji hello wystąpienia maszyny Wirtualnej zostanie wykluczony z cyklu automatycznie.</span><span class="sxs-lookup"><span data-stu-id="e8938-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="e8938-117">Zasady translacji NAT ruchu przychodzącego — Definiowanie reguł NAT hello ruch przychodzący przepływających przez hello IP frontonu i ponownie rozproszonej toohello zakończenia IP.</span><span class="sxs-lookup"><span data-stu-id="e8938-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="e8938-118">Szablony szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="e8938-118">Quickstart templates</span></span>

<span data-ttu-id="e8938-119">Usługa Azure Resource Manager umożliwia tooprovision aplikacji przy użyciu szablonu deklaracyjnego.</span><span class="sxs-lookup"><span data-stu-id="e8938-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="e8938-120">Pojedynczy szablon umożliwia wdrożenie wielu usług wraz z ich zależnościami.</span><span class="sxs-lookup"><span data-stu-id="e8938-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="e8938-121">Użyj hello tego samego szablonu toorepeatedly wdrożenia aplikacji podczas każdego etapu cyklu życia aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="e8938-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="e8938-122">Szablony mogą zawierać definicji dla maszyn wirtualnych, sieci wirtualne zestawów dostępności, interfejsów sieciowych (NIC), konta magazynu, usługi równoważenia obciążenia, grup zabezpieczeń sieci i publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="e8938-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="e8938-123">Przy użyciu szablonów można tworzyć wszystko, czego potrzebujesz złożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="e8938-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="e8938-124">Plik szablonu Hello można sprawdzić w kontroli wersji i współpracy system zarządzania zawartością.</span><span class="sxs-lookup"><span data-stu-id="e8938-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="e8938-125">Dowiedz się więcej na temat szablonów</span><span class="sxs-lookup"><span data-stu-id="e8938-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="e8938-126">Dowiedz się więcej o zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="e8938-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="e8938-127">Szablony szybkiego startu przy użyciu usługi równoważenia obciążenia Azure można znaleźć w [repozytorium GitHub](https://github.com/Azure/azure-quickstart-templates) hosting zestaw szablonów społeczności wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="e8938-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="e8938-128">Przykłady szablonów:</span><span class="sxs-lookup"><span data-stu-id="e8938-128">Examples of templates:</span></span>

* [<span data-ttu-id="e8938-129">2 maszyny wirtualne w moduł równoważenia obciążenia i reguły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e8938-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="e8938-130">2 maszyn wirtualnych w sieci Wirtualnej przy użyciu reguł wewnętrzny moduł równoważenia obciążenia i moduł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e8938-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="e8938-131">2 maszyny wirtualne w moduł równoważenia obciążenia i skonfigurować reguły NAT na powitania równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="e8938-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="e8938-132">Konfigurowanie usługi równoważenia obciążenia Azure za pomocą programu PowerShell lub interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="e8938-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="e8938-133">Wprowadzenie do poleceń cmdlet, narzędzi wiersza polecenia i interfejsów API REST usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8938-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="e8938-134">[Polecenia cmdlet systemu Azure Networking](https://msdn.microsoft.com/library/azure/mt163510.aspx) mogą być używane toocreate modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8938-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="e8938-135">Jak toocreate modułu równoważenia obciążenia przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e8938-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="e8938-136">Przy użyciu hello wiersza polecenia platformy Azure z usługą Azure Resource Management</span><span class="sxs-lookup"><span data-stu-id="e8938-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="e8938-137">Interfejsy API REST usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="e8938-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="e8938-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="e8938-138">Next steps</span></span>

<span data-ttu-id="e8938-139">Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.</span><span class="sxs-lookup"><span data-stu-id="e8938-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="e8938-140">Dowiedz się, jak toomanage [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="e8938-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="e8938-141">Jest to ważne w przypadku, gdy aplikacja wymaga połączenia tookeep aktywności dla serwerów za modułem równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="e8938-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
