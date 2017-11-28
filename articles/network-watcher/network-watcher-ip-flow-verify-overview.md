---
title: "Przepływ tooIP aaaIntroduction Sprawdź, czy w obserwatora sieciowego Azure | Dokumentacja firmy Microsoft"
description: "Ta strona zawiera omówienie hello sieci IP obserwatora przepływu Sprawdź możliwości"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: d352fb2d-4b4f-4ac4-9c2e-1cfccf0e7e03
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b648a4816a7ffdc6ca54462944b574e2395e8298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooip-flow-verify-in-azure-network-watcher"></a><span data-ttu-id="0d97f-103">Wprowadzenie tooIP przepływu Sprawdź, czy w obserwatora sieciowego Azure</span><span class="sxs-lookup"><span data-stu-id="0d97f-103">Introduction tooIP flow verify in Azure Network Watcher</span></span>

<span data-ttu-id="0d97f-104">Przepływ IP Sprawdź kontroli, jeśli pakiet jest dozwolony lub odrzucany tooor z maszyny wirtualnej na podstawie informacji 5-elementowej.</span><span class="sxs-lookup"><span data-stu-id="0d97f-104">IP flow verify checks if a packet is allowed or denied tooor from a virtual machine based on 5-tuple information.</span></span> <span data-ttu-id="0d97f-105">Te informacje składa się z kierunku, protokół lokalny adres IP, zdalny adres IP, portu lokalnego i portu zdalnego.</span><span class="sxs-lookup"><span data-stu-id="0d97f-105">This information consists of direction, protocol, local IP, remote IP, local port, and remote port.</span></span> <span data-ttu-id="0d97f-106">Jeśli pakietów hello jest zabroniony przez grupę zabezpieczeń, zwracana jest nazwa hello hello reguła odmowy pakietów hello.</span><span class="sxs-lookup"><span data-stu-id="0d97f-106">If hello packet is denied by a security group, hello name of hello rule that denied hello packet is returned.</span></span> <span data-ttu-id="0d97f-107">Podczas gdy można wybrać dowolny źródłowy lub docelowy adres IP, funkcja ta ułatwia ona administratorom szybkie diagnozowanie problemów z łącznością z lub toohello internet i z lub toohello w środowisku lokalnym.</span><span class="sxs-lookup"><span data-stu-id="0d97f-107">While any source or destination IP can be chosen, this feature helps administrators quickly diagnose connectivity issues from or toohello internet and from or toohello on-premises environment.</span></span>

<span data-ttu-id="0d97f-108">Sprawdź przepływ IP jest przeznaczony dla interfejsu sieciowego maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d97f-108">IP flow verify targets a network interface of a virtual machine.</span></span> <span data-ttu-id="0d97f-109">Przepływ ruchu jest następnie zweryfikować oparte na powitania skonfigurowane ustawienia tooor z tym interfejs sieciowy.</span><span class="sxs-lookup"><span data-stu-id="0d97f-109">Traffic flow is then verified based on hello configured settings tooor from that network interface.</span></span> <span data-ttu-id="0d97f-110">Ta funkcja jest przydatna w potwierdzaniu, jeśli zasada grupy zabezpieczeń sieci blokuje tooor ruch przychodzący lub wychodzący z maszyny wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="0d97f-110">This capability is useful in confirming if a rule in a Network Security Group is blocking ingress or egress traffic tooor from a virtual machine.</span></span>

<span data-ttu-id="0d97f-111">Sprawdź wystąpienie toobe potrzeb obserwatora sieciowego utworzone we wszystkich regionach, że planujesz toorun IP przepływu.</span><span class="sxs-lookup"><span data-stu-id="0d97f-111">An instance of Network Watcher needs toobe created in all regions that you plan toorun IP flow verify.</span></span> <span data-ttu-id="0d97f-112">Obserwatora sieciowego jest usługą regionalnych i może być przeprowadzony tylko na zasobów w hello tego samego regionu.</span><span class="sxs-lookup"><span data-stu-id="0d97f-112">Network Watcher is a regional service and can only be ran against resources in hello same region.</span></span> <span data-ttu-id="0d97f-113">Nie dotyczy to powitalne Sprawdź wyniki przepływu IP jako trasy hello skojarzone z hello kart nadal będą zwracane.</span><span class="sxs-lookup"><span data-stu-id="0d97f-113">This does not affect hello results of IP flow verify as hello route associated with hello NIC will still be returned.</span></span>

![1][1]

## <a name="next-steps"></a><span data-ttu-id="0d97f-115">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="0d97f-115">Next steps</span></span>

<span data-ttu-id="0d97f-116">Odwiedź stronę powitania po toolearn artykułu, jeśli pakiet jest dozwolony lub niedozwolony dla określonej maszyny wirtualnej za pośrednictwem portalu hello.</span><span class="sxs-lookup"><span data-stu-id="0d97f-116">Visit hello following article toolearn if a packet is allowed or denied for a specific virtual machine through hello portal.</span></span> [<span data-ttu-id="0d97f-117">Sprawdź, czy ruch jest dozwolony na maszynie Wirtualnej z przepływem Sprawdź IP przy użyciu portalu hello</span><span class="sxs-lookup"><span data-stu-id="0d97f-117">Check if traffic is allowed on a VM with IP Flow Verify using hello portal</span></span>](network-watcher-check-ip-flow-verify-portal.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png












