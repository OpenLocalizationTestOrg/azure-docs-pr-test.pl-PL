---
title: Widok grupy toosecurity aaaIntroduction w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft
description: "Ta strona zawiera omówienie hello możliwości widoku zabezpieczeń obserwatora sieciowego"
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
ms.openlocfilehash: c2f6dbbffd0aedbb9db4b69d1758f2e66dd7abb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toonetwork-security-group-view-in-azure-network-watcher"></a><span data-ttu-id="782d6-103">Widok grupy zabezpieczeń toonetwork wprowadzenie w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="782d6-103">Introduction toonetwork security group view in Azure Network Watcher</span></span>

<span data-ttu-id="782d6-104">Na poziomie podsieci lub na poziomie karty Sieciowej skojarzonych grup zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="782d6-104">Network Security groups are associated at a subnet level or at a NIC level.</span></span> <span data-ttu-id="782d6-105">Skojarzone na poziomie podsieci, zastosowanie wystąpień maszyn wirtualnych hello tooall w hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="782d6-105">When associated at a subnet level, it applies tooall hello VM instances in hello subnet.</span></span> <span data-ttu-id="782d6-106">Widok grupy zabezpieczeń sieci zwraca wszystkie grupy NSG hello skonfigurowane i reguł, które są skojarzone na poziomie podsieci i karty na maszynie wirtualnej, zapewniając wgląd w konfiguracji hello.</span><span class="sxs-lookup"><span data-stu-id="782d6-106">Network Security Group view returns all hello configured NSGs and rules that are associated at a NIC and subnet level for a virtual machine providing insight into hello configuration.</span></span> <span data-ttu-id="782d6-107">Ponadto zasady efektywnym elementem systemu zabezpieczeń hello są zwracane dla każdej z kart sieciowych hello na maszynie wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="782d6-107">In addition, hello effective security rules are returned for each of hello NICs in a VM.</span></span> <span data-ttu-id="782d6-108">Widok przy użyciu grup zabezpieczeń sieci można ocenić maszyny Wirtualnej dla luk w zabezpieczeniach sieci takich jak otwartych portów.</span><span class="sxs-lookup"><span data-stu-id="782d6-108">Using Network Security Group view, you can assess a VM for network vulnerabilities such as open ports.</span></span> <span data-ttu-id="782d6-109">Można również sprawdzić czy grupy zabezpieczeń sieci działa zgodnie z oczekiwaniami, na podstawie [porównanie hello skonfigurowane i hello reguły efektywnym elementem systemu zabezpieczeń](network-watcher-nsg-auditing-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="782d6-109">You can also validate if your Network Security Group is working as expected based on a [comparison between hello configured and hello effective security rules](network-watcher-nsg-auditing-powershell.md).</span></span>

<span data-ttu-id="782d6-110">Przypadek użycia dłuższy jest zabezpieczeń, zgodności i inspekcji.</span><span class="sxs-lookup"><span data-stu-id="782d6-110">A more extended use case is in security compliance and auditing.</span></span> <span data-ttu-id="782d6-111">Przetestowanego zestaw reguł zabezpieczeń można zdefiniować jako model ładu zabezpieczeń w organizacji.</span><span class="sxs-lookup"><span data-stu-id="782d6-111">You can define a prescriptive set of security rules as a model for security governance in your organization.</span></span> <span data-ttu-id="782d6-112">Inspekcja okresowe zgodności można zaimplementować w sposób programowy porównując hello przetestowanego reguły z hello skuteczne reguły dla poszczególnych maszyn wirtualnych hello w sieci.</span><span class="sxs-lookup"><span data-stu-id="782d6-112">A periodic compliance audit can be implemented in a programmatic way by comparing hello prescriptive rules with hello effective rules for each of hello VMs in your network.</span></span>

<span data-ttu-id="782d6-113">W hello portalu reguły są podzielone według obowiązującej, podsieci interfejsu sieciowego i domyślne.</span><span class="sxs-lookup"><span data-stu-id="782d6-113">In hello portal rules are divided by Effective, Subnet, Network Interface, and Default.</span></span> <span data-ttu-id="782d6-114">Zapewnia to prosty widok do maszyny wirtualnej tooa zasady stosowane hello.</span><span class="sxs-lookup"><span data-stu-id="782d6-114">This provides a simple view into hello rules applied tooa virtual machine.</span></span> <span data-ttu-id="782d6-115">Przycisk Pobierz jest udostępniane tooeasily Pobierz wszystkie reguły zabezpieczeń hello bez względu na karcie hello w postaci pliku CSV.</span><span class="sxs-lookup"><span data-stu-id="782d6-115">A download button is provided tooeasily download all hello security rules no matter hello tab into a CSV file.</span></span>

![Widok grupy zabezpieczeń][1]

<span data-ttu-id="782d6-117">Zasady można wybrać i otwiera nowy blok hello tooshow prefiksy sieciowej grupy zabezpieczeń i źródłowym i docelowym.</span><span class="sxs-lookup"><span data-stu-id="782d6-117">Rules can be selected and a new blade opens up tooshow hello Network Security Group and source and destination prefixes.</span></span> <span data-ttu-id="782d6-118">Z tego bloku można przejść bezpośrednio toohello zasób grupy zabezpieczeń sieci.</span><span class="sxs-lookup"><span data-stu-id="782d6-118">From this blade you can navigate directly toohello Network Security Group resource.</span></span>

![Przechodzenie do szczegółów][2]

### <a name="next-steps"></a><span data-ttu-id="782d6-120">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="782d6-120">Next steps</span></span>

<span data-ttu-id="782d6-121">Dowiedz się, jak tooaudit zabezpieczenia sieci grupy ustawień, odwiedzając [ustawienia inspekcji sieciowej grupy zabezpieczeń przy użyciu programu PowerShell](network-watcher-nsg-auditing-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="782d6-121">Learn how tooaudit your Network Security Group settings by visiting [Audit Network Security Group settings with PowerShell](network-watcher-nsg-auditing-powershell.md)</span></span>

[1]: ./media/network-watcher-security-group-view-overview/securitygroupview.png
[2]: ./media/network-watcher-security-group-view-overview/figure1.png









