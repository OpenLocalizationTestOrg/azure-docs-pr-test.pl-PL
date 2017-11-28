---
title: "Ochrona sieci w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 00b715507a7c3a4d784b800e7bf0c700f6ea6ff1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="protecting-your-network-in-azure-security-center"></a><span data-ttu-id="ab857-103">Ochrona sieci w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ab857-103">Protecting your network in Azure Security Center</span></span>
<span data-ttu-id="ab857-104">Centrum zabezpieczeń Azure analizuje stan zabezpieczeń zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab857-104">Azure Security Center analyzes the security state of your Azure resources.</span></span> <span data-ttu-id="ab857-105">Jeśli Centrum zabezpieczeń zostanie zidentyfikowana potencjalnych luk w zabezpieczeniach, tworzy zaleceń, które przeprowadzają użytkownika przez proces konfigurowania wymaganych elementów sterujących.</span><span class="sxs-lookup"><span data-stu-id="ab857-105">When Security Center identifies potential security vulnerabilities, it creates recommendations that guide you through the process of configuring the needed controls.</span></span>  <span data-ttu-id="ab857-106">Zalecenia dotyczą typów zasobów platformy Azure: maszynach wirtualnych (VM), sieci, SQL i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ab857-106">Recommendations apply to Azure resource types: virtual machines (VMs), networking, SQL, and applications.</span></span>

<span data-ttu-id="ab857-107">W tym artykule opisano zaleceń, które są stosowane do sieci.</span><span class="sxs-lookup"><span data-stu-id="ab857-107">This article addresses recommendations that apply to your network.</span></span>  <span data-ttu-id="ab857-108">Centrum zalecenia dotyczące sieci wokół następnej generacji zapór, grup zabezpieczeń sieci, konfigurowanie reguł ruchu przychodzącego i.</span><span class="sxs-lookup"><span data-stu-id="ab857-108">Network recommendations center around next generation firewalls, Network Security Groups, configuring inbound traffic rules, and more.</span></span>  <span data-ttu-id="ab857-109">Użyj poniższej tabeli jako odwołanie ułatwią zrozumienie zalecenia dotyczące dostępnych sieci i jak każdą z nich działa w przypadku zastosowania.</span><span class="sxs-lookup"><span data-stu-id="ab857-109">Use the table below as a reference to help you understand the available network recommendations and what each one does if you apply it.</span></span>

## <a name="available-network-recommendations"></a><span data-ttu-id="ab857-110">Zalecenia dostępnej sieci</span><span class="sxs-lookup"><span data-stu-id="ab857-110">Available network recommendations</span></span>
| <span data-ttu-id="ab857-111">Zalecenie</span><span class="sxs-lookup"><span data-stu-id="ab857-111">Recommendation</span></span> | <span data-ttu-id="ab857-112">Opis</span><span class="sxs-lookup"><span data-stu-id="ab857-112">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="ab857-113">Dodawanie zapory nowej generacji</span><span class="sxs-lookup"><span data-stu-id="ab857-113">Add a Next Generation Firewall</span></span>](security-center-add-next-generation-firewall.md) |<span data-ttu-id="ab857-114">Zaleca się dodanie dalej zapory generacji (NGFW) z partnerem firmy Microsoft, aby zwiększyć z ochrony zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="ab857-114">Recommends that you add a Next Generation Firewall (NGFW) from a Microsoft partner to increase your security protections.</span></span> |
| [<span data-ttu-id="ab857-115">Kierowanie ruchu sieciowego tylko za pośrednictwem zapory następnej generacji</span><span class="sxs-lookup"><span data-stu-id="ab857-115">Route traffic through NGFW only</span></span>](security-center-add-next-generation-firewall.md#route-traffic-through-ngfw-only) |<span data-ttu-id="ab857-116">Zaleca się, aby skonfigurować reguły grupy (NSG) zabezpieczeń sieciowych, który wymusza ruch przychodzący do maszyny Wirtualnej za pośrednictwem sieci NGFW.</span><span class="sxs-lookup"><span data-stu-id="ab857-116">Recommends that you configure network security group (NSG) rules that force inbound traffic to your VM through your NGFW.</span></span> |
| [<span data-ttu-id="ab857-117">Włączenie grup zabezpieczeń sieci dla podsieci lub maszyny wirtualne</span><span class="sxs-lookup"><span data-stu-id="ab857-117">Enable Network Security Groups on subnets or virtual machines</span></span>](security-center-enable-network-security-groups.md) |<span data-ttu-id="ab857-118">Zaleca się włączenie grup NSG dla podsieci lub maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="ab857-118">Recommends that you enable NSGs on subnets or VMs.</span></span> |
| [<span data-ttu-id="ab857-119">Ogranicz dostęp za pośrednictwem internetowy punkt końcowy</span><span class="sxs-lookup"><span data-stu-id="ab857-119">Restrict access through Internet facing endpoint</span></span>](security-center-restrict-access-through-internet-facing-endpoints.md) |<span data-ttu-id="ab857-120">Zaleca się, aby skonfigurować reguły ruchu przychodzącego dla grup NSG.</span><span class="sxs-lookup"><span data-stu-id="ab857-120">Recommends that you configure inbound traffic rules for NSGs.</span></span> |

## <a name="see-also"></a><span data-ttu-id="ab857-121">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="ab857-121">See also</span></span>
<span data-ttu-id="ab857-122">Aby dowiedzieć się więcej na temat zaleceń, które są stosowane do innych typów zasobów platformy Azure, zobacz następujące tematy:</span><span class="sxs-lookup"><span data-stu-id="ab857-122">To learn more about recommendations that apply to other Azure resource types, see the following:</span></span>

* [<span data-ttu-id="ab857-123">Ochrona maszyn wirtualnych w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ab857-123">Protecting your virtual machines in Azure Security Center</span></span>](security-center-virtual-machine-recommendations.md)
* [<span data-ttu-id="ab857-124">Ochrona aplikacji w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ab857-124">Protecting your applications in Azure Security Center</span></span>](security-center-application-recommendations.md)
* [<span data-ttu-id="ab857-125">Ochrona usługi Azure SQL w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="ab857-125">Protecting your Azure SQL service in Azure Security Center</span></span>](security-center-sql-service-recommendations.md)

<span data-ttu-id="ab857-126">Aby dowiedzieć się więcej na temat Centrum zabezpieczeń, zobacz następujące artykuły:</span><span class="sxs-lookup"><span data-stu-id="ab857-126">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="ab857-127">[Ustawianie zasad zabezpieczeń w usłudze Azure Security Center](security-center-policies.md) — informacje na temat konfigurowania zasad zabezpieczeń dla subskrypcji i grup zasobów na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="ab857-127">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="ab857-128">[Reagowanie na alerty zabezpieczeń i zarządzanie nimi w usłudze Azure Security Center](security-center-managing-and-responding-alerts.md) — informacje na temat reagowania na alerty zabezpieczeń i zarządzania nimi.</span><span class="sxs-lookup"><span data-stu-id="ab857-128">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="ab857-129">[Azure Security Center — często zadawane pytania](security-center-faq.md) — odpowiedzi na często zadawane pytania dotyczące korzystania z usługi.</span><span class="sxs-lookup"><span data-stu-id="ab857-129">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using the service.</span></span>
