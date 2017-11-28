---
title: "aaaInstall Endpoint Protection w Centrum zabezpieczeń Azure | Dokumentacja firmy Microsoft"
description: "Ten dokument przedstawia sposób tooimplement hello zalecenia Centrum zabezpieczeń Azure ** Zainstaluj program Endpoint Protection **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 1599ad5f-d810-421d-aafc-892e831b403f
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: fea891810e042e4d4f6e55094c0cd4de013ba68a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="install-endpoint-protection-in-azure-security-center"></a><span data-ttu-id="5bbe8-103">Zainstaluj program Endpoint Protection w Centrum zabezpieczeń Azure</span><span class="sxs-lookup"><span data-stu-id="5bbe8-103">Install Endpoint Protection in Azure Security Center</span></span>
<span data-ttu-id="5bbe8-104">Centrum zabezpieczeń Azure zaleca się, zainstaluj program endpoint protection na maszynach wirtualnych Azure (maszyny wirtualne), jeśli program endpoint protection nie jest już włączona.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-104">Azure Security Center recommends that you install endpoint protection on your Azure virtual machines (VMs) if endpoint protection is not already enabled.</span></span> <span data-ttu-id="5bbe8-105">To zalecenie odnosi się tylko tooWindows maszyn wirtualnych.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-105">This recommendation applies tooWindows VMs only.</span></span>

> [!NOTE]
> <span data-ttu-id="5bbe8-106">To Przykładowe wdrożenie używa Antimalware firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-106">This example deployment uses Microsoft Antimalware.</span></span> <span data-ttu-id="5bbe8-107">Zobacz [integracji partnerskich w Centrum zabezpieczeń Azure](security-center-partner-integration.md#partners-that-integrate-with-security-center) lista partnerów zintegrowana z Centrum zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-107">See [Partner Integration in Azure Security Center](security-center-partner-integration.md#partners-that-integrate-with-security-center) for a list of partners integrated with Security Center.</span></span>  
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="5bbe8-108">Implementowanie hello zalecenia</span><span class="sxs-lookup"><span data-stu-id="5bbe8-108">Implement hello recommendation</span></span>

> [!NOTE]
> <span data-ttu-id="5bbe8-109">Tym dokumencie przedstawiono hello usługi za pomocą przykładowego wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-109">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="5bbe8-110">Ten dokument nie jest przewodnik krok po kroku.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-110">This document is not a step-by-step guide.</span></span>
>
>

1. <span data-ttu-id="5bbe8-111">W hello **zalecenia** bloku, wybierz opcję **Zainstaluj program Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-111">In hello **Recommendations** blade, select **Install Endpoint Protection**.</span></span>
   <span data-ttu-id="5bbe8-112">![Wybierz Zainstaluj program Endpoint Protection][1]</span><span class="sxs-lookup"><span data-stu-id="5bbe8-112">![Select Install Endpoint Protection][1]</span></span>
2. <span data-ttu-id="5bbe8-113">Witaj **Zainstaluj program Endpoint Protection** zostanie otwarty blok zawierający listę maszyn wirtualnych bez ochrony punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-113">hello **Install Endpoint Protection** blade opens displaying a list of VMs without endpoint protection.</span></span> <span data-ttu-id="5bbe8-114">Wybierz jedną z hello hello listy maszyn wirtualnych, które mają tooinstall programu endpoint protection na i kliknij przycisk **zainstalować na maszynach wirtualnych**.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-114">Select from hello list hello VMs that you want tooinstall endpoint protection on and click **Install on VMs**.</span></span>
   <span data-ttu-id="5bbe8-115">![Wybierz maszyny wirtualne tooinstall Endpoint Protection na][2]</span><span class="sxs-lookup"><span data-stu-id="5bbe8-115">![Select VMs tooinstall Endpoint Protection on][2]</span></span>
3. <span data-ttu-id="5bbe8-116">Witaj **wybierz program Endpoint Protection** tooallow zostanie otwarty blok możesz tooselect hello ochrony punktów końcowych ma toouse.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-116">hello **Select Endpoint Protection** blade opens tooallow you tooselect hello endpoint protection solution you want toouse.</span></span> <span data-ttu-id="5bbe8-117">W tym przykładzie załóżmy wybierz **Microsoft Antimalware**.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-117">In this example, let's select **Microsoft Antimalware**.</span></span>
   <span data-ttu-id="5bbe8-118">![Wybierz program Endpoint Protection][3]</span><span class="sxs-lookup"><span data-stu-id="5bbe8-118">![Select Endpoint Protection][3]</span></span>
4. <span data-ttu-id="5bbe8-119">Dodatkowe informacje na temat ochrony punktów końcowych hello jest wyświetlany.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-119">Additional information about hello endpoint protection solution is displayed.</span></span> <span data-ttu-id="5bbe8-120">Wybierz pozycję **Utwórz**.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-120">Select **Create**.</span></span>
   <span data-ttu-id="5bbe8-121">![Tworzenie rozwiązania do ochrony przed złośliwym oprogramowaniem][4]</span><span class="sxs-lookup"><span data-stu-id="5bbe8-121">![Create antimalware solution][4]</span></span>
5. <span data-ttu-id="5bbe8-122">Wprowadź ustawienia konfiguracji hello wymagane na powitania **dodać rozszerzenie** bloku, a następnie wybierz **OK**.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-122">Enter hello required configuration settings on hello **Add Extension** blade, and then select **OK**.</span></span> <span data-ttu-id="5bbe8-123">toolearn więcej informacji na temat ustawień konfiguracji hello, zobacz [domyślnej i niestandardowej konfiguracji ochrony przed złośliwym kodem](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span><span class="sxs-lookup"><span data-stu-id="5bbe8-123">toolearn more about hello configuration settings, see [Default and Custom Antimalware Configuration](../security/azure-security-antimalware.md#default-and-custom-antimalware-configuration).</span></span>

<span data-ttu-id="5bbe8-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) jest teraz aktywny na powitania wybrane maszyny wirtualne.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-124">[Microsoft Antimalware](../security/azure-security-antimalware.md) is now active on hello selected VMs.</span></span>

## <a name="see-also"></a><span data-ttu-id="5bbe8-125">Zobacz też</span><span class="sxs-lookup"><span data-stu-id="5bbe8-125">See also</span></span>
<span data-ttu-id="5bbe8-126">W tym artykule pokazano, jak tooimplement hello zalecenia Centrum zabezpieczeń "Zainstaluj program Endpoint Protection".</span><span class="sxs-lookup"><span data-stu-id="5bbe8-126">This article showed you how tooimplement hello Security Center recommendation "Install Endpoint Protection."</span></span> <span data-ttu-id="5bbe8-127">toolearn więcej informacji na temat włączania Antimalware firmy Microsoft na platformie Azure, zobacz następujące dokumentu hello:</span><span class="sxs-lookup"><span data-stu-id="5bbe8-127">toolearn more about enabling Microsoft Antimalware in Azure, see hello following document:</span></span>

* <span data-ttu-id="5bbe8-128">[Antimalware firmy Microsoft dla usługi w chmurze i maszyn wirtualnych](../security/azure-security-antimalware.md) — Dowiedz się, jak toodeploy Antimalware firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-128">[Microsoft Antimalware for Cloud Services and Virtual Machines](../security/azure-security-antimalware.md) -- Learn how toodeploy Microsoft Antimalware.</span></span>

<span data-ttu-id="5bbe8-129">toolearn więcej informacji na temat Centrum zabezpieczeń, zobacz hello w następujących dokumentach:</span><span class="sxs-lookup"><span data-stu-id="5bbe8-129">toolearn more about Security Center, see hello following documents:</span></span>

* <span data-ttu-id="5bbe8-130">[Ustawianie zasad zabezpieczeń w Centrum zabezpieczeń Azure](security-center-policies.md) — Dowiedz się, jak tooconfigure zasad zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-130">[Setting security policies in Azure Security Center](security-center-policies.md) -- Learn how tooconfigure security policies.</span></span>
* <span data-ttu-id="5bbe8-131">[Zarządzanie zaleceniami dotyczącymi zabezpieczeń w Centrum zabezpieczeń Azure](security-center-recommendations.md) — Dowiedz się, w jaki sposób zalecenia ułatwiają ochronę zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-131">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) -- Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="5bbe8-132">[Monitorowanie kondycji zabezpieczeń w Centrum zabezpieczeń Azure](security-center-monitoring.md) — Dowiedz się, jak toomonitor hello kondycji zasobów platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-132">[Security health monitoring in Azure Security Center](security-center-monitoring.md) -- Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="5bbe8-133">[Zarządzanie i odpowiada toosecurity alertów w Centrum zabezpieczeń Azure](security-center-managing-and-responding-alerts.md) — Dowiedz się, jak alerty toosecurity toomanage i odpowiada.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-133">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) -- Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="5bbe8-134">[Monitorowanie rozwiązań partnerskich w Centrum zabezpieczeń Azure](security-center-partner-solutions.md) — Dowiedz się, jak toomonitor hello stanu kondycji rozwiązań partnerskich.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-134">[Monitoring partner solutions with Azure Security Center](security-center-partner-solutions.md) -- Learn how toomonitor hello health status of your partner solutions.</span></span>
* <span data-ttu-id="5bbe8-135">[Centrum zabezpieczeń Azure — często zadawane pytania](security-center-faq.md) — często zadawane pytania dotyczące korzystania z usługi hello Znajdź.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-135">[Azure Security Center FAQ](security-center-faq.md) -- Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="5bbe8-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) — wpisy na blogu dotyczące zabezpieczeń platformy Azure i zgodności.</span><span class="sxs-lookup"><span data-stu-id="5bbe8-136">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) -- Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]:./media/security-center-install-endpoint-protection/select-install-endpoint-protection.png
[2]:./media/security-center-install-endpoint-protection/install-endpoint-protection-blade.png
[3]:./media/security-center-install-endpoint-protection/select-endpoint-protection.png
[4]:./media/security-center-install-endpoint-protection/create-antimalware-solution.png
