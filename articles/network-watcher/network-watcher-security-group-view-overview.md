---
title: "Wprowadzenie do widoku grupy zabezpieczeń w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera przegląd możliwości widoku zabezpieczeń obserwatora sieciowego"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: ad27ab85-9d84-4759-b2b9-e861ef8ea8d8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 2c581a2d152a6d3f16de8f249e27a426aa9f844f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-network-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="d4d93-103">Wprowadzenie do widoku grupy zabezpieczeń sieci w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="d4d93-103">Introduction to network security group view in Azure Network Watcher</span></span>

<span data-ttu-id="d4d93-104">Na poziomie podsieci lub na poziomie karty Sieciowej skojarzonych grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="d4d93-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="d4d93-105">Gdy skojarzony na poziomie podsieci, dotyczy wszystkich wystąpień maszyn wirtualnych w podsieci.</span><span class="sxs-lookup"><span data-stu-id="d4d93-105">When associated at a subnet level, it applies to all the VM instances in the subnet.</span></span> <span data-ttu-id="d4d93-106">Widok grupy zabezpieczeń sieci zwraca wszystkich skonfigurowanych grup NSG i reguł, które są skojarzone na poziomie podsieci i karty na maszynie wirtualnej, zapewniając wgląd w konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="d4d93-106">Network Security Group view returns all the configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into the configuration.</span></span> <span data-ttu-id="d4d93-107">Ponadto zasady efektywnym elementem systemu zabezpieczeń są zwracane dla każdej z kart sieciowych w maszynie Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d4d93-107">In addition, the effective security rules are returned for each of the NICs in a VM.</span></span> <span data-ttu-id="d4d93-108">Widok przy użyciu grup zabezpieczeń sieci można ocenić maszyny Wirtualnej dla luk w zabezpieczeniach sieci takich jak otwartych portów.</span><span class="sxs-lookup"><span data-stu-id="d4d93-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="d4d93-109">Można również sprawdzić czy grupy zabezpieczeń sieci działa zgodnie z oczekiwaniami, na podstawie [porównanie skonfigurowanego i reguły zabezpieczeń skuteczne](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d4d93-109">You can also validate if your Network Security Group is working as expected based on a [comparison between the configured and the effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="d4d93-110">Przypadek użycia dłuższy jest zabezpieczeń, zgodności i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="d4d93-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="d4d93-111">Przetestowanego zestaw reguł zabezpieczeń można zdefiniować jako model ładu zabezpieczeń w organizacji.</span><span class="sxs-lookup"><span data-stu-id="d4d93-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="d4d93-112">Inspekcja okresowe zgodności można zaimplementować w sposób programowy porównując przetestowanego reguł za pomocą skuteczne reguł dla poszczególnych maszyn wirtualnych w sieci.</span><span class="sxs-lookup"><span data-stu-id="d4d93-112">A periodic compliance audit can be implemented in a programmatic way by comparing the prescriptive rules with the effective rules for each of the VMs in your network.</span></span>

<span data-ttu-id="d4d93-113">W portalu, do którego zasady są podzielone według obowiązującej, podsieci interfejsu sieciowego i domyślne.</span><span class="sxs-lookup"><span data-stu-id="d4d93-113">In the portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="d4d93-114">Zapewnia to prosty widok do zasady zastosowane do maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="d4d93-114">This provides a simple view into the rules applied to a virtual machine.</span></span> <span data-ttu-id="d4d93-115">Można łatwo pobrać wszystkie reguły zabezpieczeń bez względu na karcie do pliku CSV znajduje się przycisk Pobierz.</span><span class="sxs-lookup"><span data-stu-id="d4d93-115">A download button is provided to easily download all the security rules no matter the tab into a CSV file.</span></span>

![Widok grupy zabezpieczeń][1]

<span data-ttu-id="d4d93-117">Zasady można wybrać i otwiera nowy blok do wyświetlenia grupy zabezpieczeń sieci i prefiksy źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="d4d93-117">Rules can be selected and a new blade opens up to show the Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="d4d93-118">Z tego bloku można przejść bezpośrednio do tego zasobu grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="d4d93-118">From this blade you can navigate directly to the Network Security Group resource.</span></span>

![Przechodzenie do szczegółów][2]

### <a name="next-steps"></a><span data-ttu-id="d4d93-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d4d93-120">Next steps</span></span>

<span data-ttu-id="d4d93-121">Dowiedz się, jak inspekcji ustawienia sieciowej grupy zabezpieczeń, odwiedzając [ustawienia inspekcji, grupy zabezpieczeń sieci przy użyciu programu PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d4d93-121">Learn how to audit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









