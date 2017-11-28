---
title: "aaaPoint nazwę domeny firmy Internet domeny tooa Traffic Manager | Dokumentacja firmy Microsoft"
description: "Ten artykuł pomoże Ci wskaż nazwę domeny firmowej domeny nazwa tooa Menedżera ruchu."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 29822946-2d45-4434-ba47-fc180a445cc3
ms.service: traffic-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/11/2016
ms.author: kumud
ms.openlocfilehash: 84c428f60a1dc70452bf957d98a68c95e0b51715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="point-a-company-internet-domain-tooan-azure-traffic-manager-domain"></a><span data-ttu-id="28953-103">Ustawianie firmowej domeny usługi Azure Traffic Manager tooan domeny Internet</span><span class="sxs-lookup"><span data-stu-id="28953-103">Point a company Internet domain tooan Azure Traffic Manager domain</span></span>

<span data-ttu-id="28953-104">Podczas tworzenia profilu usługi Traffic Manager platforma Azure automatycznie przypisuje nazwę DNS dla danego profilu.</span><span class="sxs-lookup"><span data-stu-id="28953-104">When you create a Traffic Manager profile, Azure automatically assigns a DNS name for that profile.</span></span> <span data-ttu-id="28953-105">toouse nazwę strefy DNS, utworzyć rekord CNAME DNS, który mapuje nazwę domeny profilu usługi Traffic Manager toohello.</span><span class="sxs-lookup"><span data-stu-id="28953-105">toouse a name from your DNS zone, create a CNAME DNS record that maps toohello domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="28953-106">Nazwa domeny usługi Traffic Manager hello można znaleźć w hello **ogólne** sekcji na stronie konfiguracji hello hello profilu usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="28953-106">You can find hello Traffic Manager domain name in hello **General** section on hello Configuration page of hello Traffic Manager profile.</span></span>

<span data-ttu-id="28953-107">Na przykład toopoint nazwy www.contoso.com toohello contoso.trafficmanager.net nazwy DNS Menedżera ruchu, należy utworzyć powitania po rekord zasobu DNS:</span><span class="sxs-lookup"><span data-stu-id="28953-107">For example, toopoint name www.contoso.com toohello Traffic Manager DNS name contoso.trafficmanager.net, you would create hello following DNS resource record:</span></span>

    www.contoso.com IN CNAME contoso.trafficmanager.net

<span data-ttu-id="28953-108">Wszystkie żądania ruchu za*www.contoso.com* uzyskać kierowane za*contoso.trafficmanager.net*.</span><span class="sxs-lookup"><span data-stu-id="28953-108">All traffic requests too*www.contoso.com* get directed too*contoso.trafficmanager.net*.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="28953-109">Nie może wskazywać domeny drugiego poziomu, takich jak *contoso.com*, toohello domeny usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="28953-109">You cannot point a second-level domain, such as *contoso.com*, toohello Traffic Manager domain.</span></span> <span data-ttu-id="28953-110">Standardy protokołu DNS nie zezwalają na ustanawianie rekordów CNAME dla nazw domen drugiego poziomu.</span><span class="sxs-lookup"><span data-stu-id="28953-110">DNS protocol standards do not allow CNAME records for second-level domain names.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28953-111">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="28953-111">Next steps</span></span>

* [<span data-ttu-id="28953-112">Metody routingu w usłudze Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="28953-112">Traffic Manager routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="28953-113">Traffic Manager — wyłączanie, włączanie lub usuwanie profilu</span><span class="sxs-lookup"><span data-stu-id="28953-113">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)
* [<span data-ttu-id="28953-114">Traffic Manager — wyłączanie lub włączanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="28953-114">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)
