---
title: "aaaEnable agenta maszyny Wirtualnej w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** włączyć VM Agent **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 5b431c25-4241-45b7-9556-cf2a1956f3da
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 9bd71e638b020780537da25fd4cf7baf34d3e11a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-vm-agent-in-azure-security-center"></a><span data-ttu-id="23087-103">Włącz agenta maszyny Wirtualnej w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="23087-103">Enable VM Agent in Azure Security Center</span></span>
<span data-ttu-id="23087-104">Witaj maszyny Wirtualnej musi być zainstalowany Agent na maszynach wirtualnych (VM) w kolejności zbyt[Włącz zbieranie danych](security-center-enable-data-collection.md).</span><span class="sxs-lookup"><span data-stu-id="23087-104">hello VM Agent must be installed on virtual machines (VMs) in order too[enable data collection](security-center-enable-data-collection.md).</span></span>  <span data-ttu-id="23087-105">Centrum zabezpieczeń Azure umożliwia toosee możesz maszyny wirtualne wymagające hello agenta maszyny Wirtualnej i zaleca włączenie hello agenta maszyny Wirtualnej na tych maszynach wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="23087-105">Azure Security Center enables you toosee which VMs require hello VM Agent and will recommend that you enable hello VM Agent on those VMs.</span></span>

<span data-ttu-id="23087-106">Witaj agenta maszyny Wirtualnej jest instalowany domyślnie dla maszyn wirtualnych, które zostały wdrożone z hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="23087-106">hello VM Agent is installed by default for VMs that are deployed from hello Azure Marketplace.</span></span> <span data-ttu-id="23087-107">Artykuł Hello [agenta maszyny Wirtualnej i rozszerzenia — część 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) zawiera informacje na temat sposobu tooinstall hello agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23087-107">hello article [VM Agent and Extensions – Part 2](https://azure.microsoft.com/blog/vm-agent-and-extensions-part-2/) provides information on how tooinstall hello VM Agent.</span></span>

> [!NOTE]
> <span data-ttu-id="23087-108">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="23087-108">This document introduces hello service by using an example deployment.</span></span> <span data-ttu-id="23087-109">Nie jest to przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="23087-109">This is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="23087-110">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="23087-110">Implement hello recommendation</span></span>
1. <span data-ttu-id="23087-111">W hello **bloku zalecenia**, wybierz pozycję **włączyć agenta maszyny Wirtualnej**.</span><span class="sxs-lookup"><span data-stu-id="23087-111">In hello **Recommendations blade**, select **Enable VM Agent**.</span></span>
   <span data-ttu-id="23087-112">![Włącz agenta maszyny wirtualnej][1]</span><span class="sxs-lookup"><span data-stu-id="23087-112">![Enable VM Agent][1]</span></span>
2. <span data-ttu-id="23087-113">Spowoduje to otwarcie bloku hello **VM Agent Brak lub nie odpowiada**.</span><span class="sxs-lookup"><span data-stu-id="23087-113">This opens hello blade **VM Agent Is Missing Or Not Responding**.</span></span> <span data-ttu-id="23087-114">Ten blok zawiera hello maszyn wirtualnych, które wymagają hello agenta maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23087-114">This blade lists hello VMs that require hello VM Agent.</span></span> <span data-ttu-id="23087-115">Postępuj zgodnie instrukcje hello na agenta hello bloku tooinstall hello maszyny Wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="23087-115">Follow hello instructions on hello blade tooinstall hello VM agent.</span></span>
   <span data-ttu-id="23087-116">![Brak agenta maszyny Wirtualnej][2]</span><span class="sxs-lookup"><span data-stu-id="23087-116">![VM Agent is missing][2]</span></span>

## <a name="see-also"></a><span data-ttu-id="23087-117">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="23087-117">See also</span></span>
<span data-ttu-id="23087-118">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz następujące hello:</span><span class="sxs-lookup"><span data-stu-id="23087-118">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="23087-119">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md)— Dowiedz się, jak tooconfigure zasad zabezpieczeń dla subskrypcji platformy Azure i grup zasobów.</span><span class="sxs-lookup"><span data-stu-id="23087-119">[Setting security policies in Azure Security Center](security-center-policies.md)--Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="23087-120">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — informacje o tym, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23087-120">[Managing security recommendations in Azure Security Center](security-center-recommendations.md)--Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="23087-121">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md)— Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23087-121">[Security health monitoring in Azure Security Center](security-center-monitoring.md)--Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="23087-122">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md)— Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="23087-122">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md)--Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="23087-123">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="23087-123">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="23087-124">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md)— często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="23087-124">[Azure Security Center FAQ](security-center-faq.md)--Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="23087-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--hello najnowsze zabezpieczeń platformy Azure i informacji.</span><span class="sxs-lookup"><span data-stu-id="23087-125">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/)--Get hello latest Azure security news and information.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-vm-agent/enable-vm-agent.png
[2]: ./media/security-center-enable-vm-agent/vm-agent-is-missing.png
