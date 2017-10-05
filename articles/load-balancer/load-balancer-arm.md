---
title: "Pomocy technicznej platformy Azure Resource Manager dla usługi równoważenia obciążenia | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="d512c-104">Za pomocą techniczną platformy Azure Resource Manager z usługą równoważenia obciążenia Azure</span><span class="sxs-lookup"><span data-stu-id="d512c-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="d512c-105">Usługa Azure Resource Manager to struktura preferowane dla usług Azure.</span><span class="sxs-lookup"><span data-stu-id="d512c-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="d512c-106">Moduł równoważenia obciążenia Azure mogą być zarządzane przy użyciu usługi Azure Resource Manager na podstawie interfejsów API i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d512c-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="d512c-107">Pojęcia</span><span class="sxs-lookup"><span data-stu-id="d512c-107">Concepts</span></span>

<span data-ttu-id="d512c-108">Usługa Resource Manager modułu równoważenia obciążenia Azure zawiera następujące zasoby podrzędne:</span><span class="sxs-lookup"><span data-stu-id="d512c-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="d512c-109">Konfiguracja IP frontonu — modułu równoważenia obciążenia może zawierać co najmniej jeden adres IP frontonu, znanej także jako wirtualnych adresów IP (VIP).</span><span class="sxs-lookup"><span data-stu-id="d512c-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="d512c-110">Te adresy IP są używane podczas transferu danych przychodzących.</span><span class="sxs-lookup"><span data-stu-id="d512c-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="d512c-111">Pula adresów zaplecza — są to adresy IP skojarzone z maszyny wirtualnej sieci karta sieciowa (NIC) na które będą przesyłane obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d512c-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="d512c-112">Reguły równoważenia obciążenia — właściwości reguły mapuje IP danego frontonu i kombinacja portu do zbioru adresów IP zaplecza i portu kombinacji.</span><span class="sxs-lookup"><span data-stu-id="d512c-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="d512c-113">Moduł równoważenia obciążenia może mieć różne reguły równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d512c-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="d512c-114">Każda reguła zawiera kombinację adresu IP frontonu i portu oraz adresu IP zaplecza i portu, które są powiązane z maszynami wirtualnymi.</span><span class="sxs-lookup"><span data-stu-id="d512c-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="d512c-115">Sond — sond włączyć do śledzenia kondycji wystąpień maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="d512c-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="d512c-116">W przypadku niepowodzenia sondy kondycji wystąpienie maszyny Wirtualnej zostanie wykluczony z cyklu automatycznie.</span><span class="sxs-lookup"><span data-stu-id="d512c-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="d512c-117">Reguły NAT ruchu przychodzącego — Definiowanie ruch przychodzący przepływających przez na wierzch reguł NAT zakończenie IP i dystrybuowane do IP zaplecza.</span><span class="sxs-lookup"><span data-stu-id="d512c-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="d512c-118">Szablony szybkiego startu</span><span class="sxs-lookup"><span data-stu-id="d512c-118">Quickstart templates</span></span>

<span data-ttu-id="d512c-119">Usługa Azure Resource Manager pozwala inicjować obsługę aplikacji za pomocą deklaratywnych szablonów.</span><span class="sxs-lookup"><span data-stu-id="d512c-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="d512c-120">W pojedynczym szablonie możesz wdrożyć wiele usług wraz z ich zależnościami.</span><span class="sxs-lookup"><span data-stu-id="d512c-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="d512c-121">Za pomocą tego samego szablonu możesz wdrażać aplikację na każdym etapie jej cyklu życia.</span><span class="sxs-lookup"><span data-stu-id="d512c-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="d512c-122">Szablony mogą zawierać definicji dla maszyn wirtualnych, sieci wirtualne zestawów dostępności, interfejsów sieciowych (NIC), konta magazynu, usługi równoważenia obciążenia, grup zabezpieczeń sieci i publicznych adresów IP.</span><span class="sxs-lookup"><span data-stu-id="d512c-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="d512c-123">Przy użyciu szablonów można tworzyć wszystko, czego potrzebujesz złożonych aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d512c-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="d512c-124">Plik szablonu może służyć do zarządzania zawartością system kontroli wersji i współpracy.</span><span class="sxs-lookup"><span data-stu-id="d512c-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="d512c-125">Dowiedz się więcej na temat szablonów</span><span class="sxs-lookup"><span data-stu-id="d512c-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="d512c-126">Dowiedz się więcej o zasoby sieciowe</span><span class="sxs-lookup"><span data-stu-id="d512c-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="d512c-127">Szablony szybkiego startu przy użyciu usługi równoważenia obciążenia Azure można znaleźć w [repozytorium GitHub](https://github.com/Azure/azure-quickstart-templates) hosting zestaw szablonów społeczności wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="d512c-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="d512c-128">Przykłady szablonów:</span><span class="sxs-lookup"><span data-stu-id="d512c-128">Examples of templates:</span></span>

* [<span data-ttu-id="d512c-129">2 maszyny wirtualne w moduł równoważenia obciążenia i reguły równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="d512c-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="d512c-130">2 maszyn wirtualnych w sieci Wirtualnej przy użyciu reguł wewnętrzny moduł równoważenia obciążenia i moduł równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="d512c-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="d512c-131">2 maszyny wirtualne w moduł równoważenia obciążenia i skonfigurować reguły NAT na równoważeniem obciążenia</span><span class="sxs-lookup"><span data-stu-id="d512c-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="d512c-132">Konfigurowanie usługi równoważenia obciążenia Azure za pomocą programu PowerShell lub interfejsu wiersza polecenia</span><span class="sxs-lookup"><span data-stu-id="d512c-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="d512c-133">Wprowadzenie do poleceń cmdlet, narzędzi wiersza polecenia i interfejsów API REST usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d512c-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="d512c-134">[Polecenia cmdlet systemu Azure Networking](https://msdn.microsoft.com/library/azure/mt163510.aspx) może służyć do tworzenia modułu równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d512c-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="d512c-135">Jak utworzyć usługę równoważenia obciążenia przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d512c-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="d512c-136">Przy użyciu interfejsu wiersza polecenia platformy Azure w usłudze zarządzania zasobami Azure</span><span class="sxs-lookup"><span data-stu-id="d512c-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="d512c-137">Interfejsy API REST usługi równoważenia obciążenia</span><span class="sxs-lookup"><span data-stu-id="d512c-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="d512c-138">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d512c-138">Next steps</span></span>

<span data-ttu-id="d512c-139">Możesz również [rozpocząć tworzenie internetowy modułu równoważenia obciążenia](load-balancer-get-started-internet-arm-ps.md) i skonfigurować typ [trybu rozkładu](load-balancer-distribution-mode.md) dla zachowania ruchu sieci usługi równoważenia obciążenia określonego.</span><span class="sxs-lookup"><span data-stu-id="d512c-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="d512c-140">Dowiedz się, jak zarządzać [ustawienia limitu czasu protokołu TCP dla usługi równoważenia obciążenia w stanie bezczynności](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="d512c-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="d512c-141">Jest to ważne w przypadku, gdy aplikacja musi podtrzymywania połączenia dla serwerów za modułem równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d512c-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
