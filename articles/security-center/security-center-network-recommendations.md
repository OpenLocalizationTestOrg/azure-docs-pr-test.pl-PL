---
title: "aaaProtecting sieci w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten adres dokumentu zalecenia w Centrum zabezpieczeń Azure, które ułatwiają ochronę sieci platformy Azure i są aktualizowane zgodnie z zasadami zabezpieczeń."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 96c55a02-afd6-478b-9c1f-039528f3dea0
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/16/2016
ms.author: terrylan
ms.openlocfilehash: 053738da432edf13b40172fb44d2044702dd8211
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="2554a-103">Ochrona sieci w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="2554a-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="2554a-104">Centrum zabezpieczeń Azure analizuje hello stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2554a-104">Azure Security Center analyzes hello security state of your Azure resources.</span></span> <span data-ttu-id="2554a-105">Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania kontrolek hello potrzebne hello.</span><span class="sxs-lookup"><span data-stu-id="2554a-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through hello process of configuring hello needed controls.</span></span>  <span data-ttu-id="2554a-106">Zalecenia dotyczące zastosować tooAzure typy zasobów: maszynach wirtualnych (VM), sieci, SQL i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="2554a-106">Recommendations apply tooAzure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="2554a-107">W tym artykule opisano zalecenia dotyczące sieci tooyour.</span><span class="sxs-lookup"><span data-stu-id="2554a-107">This article addresses recommendations that apply tooyour network.</span></span>  <span data-ttu-id="2554a-108">Centrum zalecenia dotyczące sieci wokół następnej generacji zapór, grup zabezpieczeń sieci, konfigurowanie reguł ruchu przychodzącego i.</span><span class="sxs-lookup"><span data-stu-id="2554a-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="2554a-109">Użyj hello poniższej tabeli jako toohelp odwołanie zrozumieć hello dostępnej sieci zalecenia i jak każdej z nich działa w przypadku zastosowania.</span><span class="sxs-lookup"><span data-stu-id="2554a-109">Use hello table below as a reference toohelp you understand hello available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="2554a-110">Zalecenia dostępnej sieci</span><span class="sxs-lookup"><span data-stu-id="2554a-110">Available network recommendations</span></span>
| <span data-ttu-id="2554a-111">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="2554a-111">Recommendation</span></span> | <span data-ttu-id="2554a-112">Opis</span><span class="sxs-lookup"><span data-stu-id="2554a-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="2554a-113">Dodawanie zapory nowej generacji</span><span class="sxs-lookup"><span data-stu-id="2554a-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="2554a-114">Zaleca się, że dodasz dalej zapory generacji (NGFW) z tooincrease partnera firmy Microsoft z ochrony zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="2554a-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner tooincrease your security protections.</span></span> |
| [<span data-ttu-id="2554a-115">Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji</span><span class="sxs-lookup"><span data-stu-id="2554a-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="2554a-116">Zaleca się, aby skonfigurować reguły grupy (NSG) zabezpieczeń sieciowych, który wymusza ruch przychodzący tooyour maszyny Wirtualnej za pośrednictwem sieci NGFW.</span><span class="sxs-lookup"><span data-stu-id="2554a-116">Recommends that you configure network security group (NSG) rules that force inbound traffic tooyour VM through your NGFW.</span></span> |
| [<span data-ttu-id="2554a-117">Włączenie grup zabezpieczeń sieci dla podsieci lub maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="2554a-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="2554a-118">Zaleca się włączenie grup NSG dla podsieci lub maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="2554a-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="2554a-119">Ogranicz dostęp za pośrednictwem internetowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="2554a-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="2554a-120">Zaleca się, aby skonfigurować reguły ruchu przychodzącego dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="2554a-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="2554a-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="2554a-121">See also</span></span>
<span data-ttu-id="2554a-122">toolearn więcej informacji na temat zaleceń, które są stosowane tooother typów zasobów platformy Azure, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2554a-122">toolearn more about recommendations that apply tooother Azure resource types, see hello following:</span></span>

* [<span data-ttu-id="2554a-123">Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="2554a-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="2554a-124">Ochrona aplikacji w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="2554a-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="2554a-125">Ochrona usługi Azure SQL w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="2554a-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="2554a-126">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="2554a-126">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="2554a-127">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="2554a-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="2554a-128">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="2554a-128">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="2554a-129">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="2554a-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
